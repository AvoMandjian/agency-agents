# Flutter Error Handling Guide

**🛡️ Comprehensive Error Handling Strategy | Version 1.0.0 | Updated: Oct 17, 2025**

---

## 📖 Introduction

This guide defines error handling standards for Flutter applications developed by Agency Agents. Proper error handling ensures great user experience, easier debugging, and production reliability.

### Error Handling Philosophy

- **User-Friendly**: Show clear, actionable messages to users
- **Developer-Friendly**: Capture detailed context for debugging
- **Graceful Degradation**: App continues functioning despite errors
- **Observable**: All errors logged and monitored
- **Preventable**: Validate inputs and handle edge cases proactively

---

## 🎯 Error Categorization Strategy

### 1. Network Errors

**Common Scenarios**:
- No internet connection
- Request timeout
- Server error (500)
- API rate limiting

**User Message**: `ErrorMessages.networkError`  
**Logging**: Full stack trace + network details  
**Recovery**: Retry mechanism, offline mode

### 2. Authentication Errors

**Common Scenarios**:
- Invalid credentials
- Session expired
- Unauthorized access (403)

**User Message**: `ErrorMessages.authenticationFailed`  
**Logging**: Auth attempt details (no passwords!)  
**Recovery**: Redirect to login, refresh token

### 3. Validation Errors

**Common Scenarios**:
- Invalid email format
- Password too short
- Required field empty

**User Message**: Field-specific validation messages  
**Logging**: Input validation failures  
**Recovery**: Show inline error, focus field

### 4. Unexpected Errors

**Common Scenarios**:
- Null pointer exceptions
- Parse errors
- Unknown exceptions

**User Message**: `ErrorMessages.unexpectedError`  
**Logging**: Full stack trace + context  
**Recovery**: Graceful fallback, report to Sentry

---

## 🔔 GlobalSnackbar Integration

### Pattern Reference

See complete implementation in [flutter-patterns.md](./flutter-patterns.md#user-notification-pattern-with-globalsnackbar)

### Usage in Cubits

```dart
@injectable
class ProductCubit extends Cubit<ProductState> {
  final ProductRepo _repo;
  
  ProductCubit(this._repo) : super(ProductInitial());
  
  Future<void> loadProducts() async {
    emit(ProductLoading());
    try {
      final response = await _repo.fetchProducts();
      if (response != null && response.success) {
        emit(ProductSuccess(response.products!));
      } else {
        // Server returned error response
        emit(ProductError(
          response?.message ?? ErrorMessages.loadingFailed,
        ));
      }
    } catch (e) {
      // Network or unexpected error
      emit(ProductError(ErrorMessages.fromException(e)));
      
      // Log to Sentry
      Sentry.captureException(e, stackTrace: StackTrace.current);
    }
  }
}
```

### Usage in Screens

```dart
@override
Widget build(BuildContext context) {
  return BlocListener<ProductCubit, ProductState>(
    listenWhen: (previous, current) {
      return current is ProductError || current is ProductSuccess;
    },
    listener: (context, state) {
      if (state is ProductSuccess) {
        GlobalSnackbar.showSuccessToast(
          context,
          'Products loaded successfully',
        );
      }
      if (state is ProductError) {
        GlobalSnackbar.showFailureToast(context, state.message);
      }
    },
    child: BlocBuilder<ProductCubit, ProductState>(
      builder: (context, state) {
        // Build UI based on state
      },
    ),
  );
}
```

---

## 📊 Sentry/Crashlytics Integration

### Setup in main.dart

```dart
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  
  // Initialize Firebase
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  
  // Initialize Sentry
  await SentryFlutter.init(
    (options) {
      options.dsn = 'YOUR_SENTRY_DSN';
      options.environment = const String.fromEnvironment('ENV', defaultValue: 'production');
      options.tracesSampleRate = 0.1;  // 10% of transactions
    },
    appRunner: () => runApp(const MyApp()),
  );
  
  // Global error handlers
  setupErrorHandlers();
}

void setupErrorHandlers() {
  // Flutter errors
  FlutterError.onError = (details) {
    AppLogger.e(error: details.exception, stackTrace: details.stack);
    FirebaseCrashlytics.instance.recordFlutterFatalError(details);
    Sentry.captureException(details.exception, stackTrace: details.stack);
  };
  
  // Dart errors
  PlatformDispatcher.instance.onError = (error, stack) {
    AppLogger.e(error: error, stackTrace: stack);
    FirebaseCrashlytics.instance.recordError(error, stack, fatal: true);
    Sentry.captureException(error, stackTrace: stack);
    return true;
  };
}
```

### Error Capture in Business Logic

```dart
try {
  final result = await repository.performOperation();
  emit(SuccessState(result!));
} on NetworkException catch (e, stack) {
  // Network-specific error
  emit(ErrorState(ErrorMessages.networkError));
  Sentry.captureException(e, stackTrace: stack);
} on AuthException catch (e, stack) {
  // Auth-specific error
  emit(ErrorState(ErrorMessages.authenticationFailed));
  Sentry.captureException(e, stackTrace: stack);
} catch (e, stack) {
  // Unexpected error
  emit(ErrorState(ErrorMessages.unexpectedError));
  Sentry.captureException(e, stackTrace: stack);
  AppLogger.e(error: e, stackTrace: stack);
}
```

---

## 📝 Error Logging Standards

### AppLogger Utility

```dart
class AppLogger {
  static void d(String message, {Map<String, dynamic>? data}) {
    if (kDebugMode) {
      print('[DEBUG] $message ${data ?? ''}');
    }
  }
  
  static void e({
    required Object error,
    StackTrace? stackTrace,
    Map<String, dynamic>? context,
  }) {
    if (kDebugMode) {
      print('[ERROR] $error');
      if (stackTrace != null) print(stackTrace);
      if (context != null) print('Context: $context');
    }
    
    // Always log to crashlytics/sentry in production
    FirebaseCrashlytics.instance.recordError(
      error,
      stackTrace,
      reason: context?.toString(),
    );
  }
}
```

### Error Context Enrichment

```dart
try {
  final result = await operation();
} catch (e, stack) {
  // Add context for better debugging
  Sentry.captureException(
    e,
    stackTrace: stack,
    withScope: (scope) {
      scope.setTag('feature', 'checkout');
      scope.setUser(SentryUser(id: userId));
      scope.setContext('operation_context', {
        'product_id': productId,
        'quantity': quantity,
        'timestamp': DateTime.now().toIso8601String(),
      });
    },
  );
}
```

---

## ✅ Error Handling Checklist

### Cubit Implementation

- [ ] All async operations wrapped in try-catch
- [ ] Network errors caught and handled with ErrorMessages
- [ ] Auth errors caught and handled appropriately
- [ ] Unexpected errors logged to Sentry
- [ ] Error states emit user-friendly messages
- [ ] No stack traces shown to users

### Screen Implementation

- [ ] BlocListener shows GlobalSnackbar on errors
- [ ] Error states display appropriate UI
- [ ] User has clear recovery path (retry button, etc.)
- [ ] Loading states prevent duplicate submissions
- [ ] Network errors show offline indicator

### Repository Implementation

- [ ] NetworkService errors caught and transformed
- [ ] HTTP status codes handled appropriately
- [ ] Timeouts configured and handled
- [ ] Response validation before returning
- [ ] Detailed error context for debugging

---

## 🚨 Production Error Monitoring

### Monitoring Strategy

**Firebase Crashlytics**:
- Fatal crashes (app termination)
- Non-fatal errors (handled exceptions)
- Custom logs for debugging context

**Sentry**:
- Error grouping and deduplication
- Release tracking
- Performance monitoring (optional)
- User feedback integration

**Firebase Analytics**:
- Error events with context
- User journey before error
- Error frequency and patterns

### Alerting Thresholds

**Trigger alerts when**:
- Crash rate >0.1% (>1 crash per 1000 sessions)
- Error rate >1% (>10 errors per 1000 sessions)
- New error type appears (never seen before)
- Error spike (3x normal rate)

---

**Version**: 1.0.0 | **Last Updated**: October 17, 2025 | **Integration**: GlobalSnackbar + ErrorMessages + Sentry + Firebase

