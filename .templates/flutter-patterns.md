# Flutter Pattern Templates for Agent Updates

## BLoC State Management Pattern with Sealed Classes

### State Definition Template
```dart
// MANDATORY: Use sealed classes for type-safe state management
sealed class FeatureState extends Equatable {
  const FeatureState();
  
  @override
  List<Object?> get props => [];
}

class FeatureInitial extends FeatureState {}

class FeatureLoading extends FeatureState {}

class FeatureSuccess extends FeatureState {
  final Data data;
  
  const FeatureSuccess(this.data);
  
  @override
  List<Object?> get props => [data];
}

class FeatureError extends FeatureState {
  final String message;
  
  const FeatureError(this.message);
  
  @override
  List<Object?> get props => [message];
}
```

### Cubit Implementation Template
```dart
// MANDATORY: Comprehensive error handling with user-friendly messages
class FeatureCubit extends Cubit<FeatureState> {
  FeatureCubit() : super(FeatureInitial());
  
  Future<void> loadData() async {
    emit(FeatureLoading());
    try {
      final result = await FeatureRepo.fetchData();
      emit(FeatureSuccess(result!));
    } catch (e) {
      emit(FeatureError(_getErrorMessage(e)));
    }
  }
  
  String _getErrorMessage(Object error) {
    if (error.toString().contains('network')) {
      return 'Network error. Please check your connection.';
    }
    if (error.toString().contains('timeout')) {
      return 'Request timed out. Please try again.';
    }
    return 'An unexpected error occurred. Please try again.';
  }
}
```

### BlocBuilder Widget Template
```dart
// MANDATORY: Optimize rebuilds with selective listening
BlocBuilder<FeatureCubit, FeatureState>(
  buildWhen: (previous, current) => current is! FeatureLoading,
  builder: (context, state) {
    return switch (state) {
      FeatureInitial() => const InitialView(),
      FeatureLoading() => const LoadingIndicator(),
      FeatureSuccess(:final data) => SuccessView(data: data),
      FeatureError(:final message) => ErrorView(message: message),
    };
  },
)
```

## Repository Pattern with Injected NetworkService

```dart
// MANDATORY: Repository with injected NetworkService and class-based constants
import 'package:injectable/injectable.dart';
import 'package:stack_trace/stack_trace.dart';
import '../models/api_models/product_body_api.dart';
import '../models/responses/product_response.dart';
import '../services/network_service.dart';
import '../utils/constant.dart';

@lazySingleton
class ProductRepo {
  final NetworkService _networkService;
  
  // Constructor injection via Injectable
  ProductRepo(this._networkService);

  /// Fetch all products
  Future<ProductListResponse?> fetchProducts() async {
    String url = GlobalApiUrls.products; // Endpoint URL constant
    
    final body = ProductBodyApi(
      method: ProductApiMethods.getProducts, // Method name constant
    );

    final response = await _networkService.httpPostRequest(
      stackTrace: Trace.current(), // Stack trace for debugging
      url: url,
      body: body.toJson(),
      fromJsonFactory: (response) => ProductListResponse.fromJson(response),
    );
    return response;
  }
  
  /// Get single product by ID
  Future<ProductResponse?> getProduct({
    required String productId,
  }) async {
    String url = GlobalApiUrls.products;
    
    final body = ProductBodyApi(
      method: ProductApiMethods.getProduct,
      productId: productId,
    );

    final response = await _networkService.httpPostRequest(
      stackTrace: Trace.current(),
      url: url,
      body: body.toJson(),
      fromJsonFactory: (response) => ProductResponse.fromJson(response),
    );
    return response;
  }
  
  /// Create new product
  Future<ProductResponse?> createProduct({
    required String name,
    required double price,
    String? description,
  }) async {
    String url = GlobalApiUrls.products;
    
    final body = ProductBodyApi(
      method: ProductApiMethods.createProduct,
      name: name,
      price: price,
      description: description,
    );

    final response = await _networkService.httpPostRequest(
      stackTrace: Trace.current(),
      url: url,
      body: body.toJson(),
      fromJsonFactory: (response) => ProductResponse.fromJson(response),
    );
    return response;
  }
}

// Class-based constants for type safety
class GlobalApiUrls {
  static const String auth = '/auth';
  static const String products = '/products';
  static const String orders = '/orders';
}

class ProductApiMethods {
  static const String getProducts = 'getProducts';
  static const String getProduct = 'getProduct';
  static const String createProduct = 'createProduct';
  static const String updateProduct = 'updateProduct';
  static const String deleteProduct = 'deleteProduct';
}

class ProductBodyApi {
  final String method;
  final String? productId;
  final String? name;
  final double? price;
  final String? description;

  ProductBodyApi({
    required this.method,
    this.productId,
    this.name,
    this.price,
    this.description,
  });

  Map<String, dynamic> toJson() => {
    'method': method,
    if (productId != null) 'productId': productId,
    if (name != null) 'name': name,
    if (price != null) 'price': price,
    if (description != null) 'description': description,
  };
}

class ProductResponse {
  final bool success;
  final Product? product;
  final String? message;

  ProductResponse({
    required this.success,
    this.product,
    this.message,
  });

  factory ProductResponse.fromJson(Map<String, dynamic> json) => ProductResponse(
    success: json['success'] ?? false,
    product: json['product'] != null 
        ? Product.fromJson(json['product']) 
        : null,
    message: json['message'],
  );
}
```

## User Notification Pattern with GlobalSnackbar

### Why GlobalSnackbar?
GlobalSnackbar provides consistent, transient user feedback across your Flutter app. Use it for success confirmations, error messages, and important notifications that don't require user interaction. Best practices include positioning at screen bottom, reasonable duration (3-5 seconds), and clear, concise messages.

### GlobalSnackbar Utility Class
```dart
// MANDATORY: Centralized user notification system
// Reference: https://api.flutter.dev/flutter/material/ScaffoldMessenger-class.html
import 'package:flutter/material.dart';

class GlobalSnackbar {
  /// Show success toast notification (green background)
  static void showSuccessToast(BuildContext context, String message) {
    ScaffoldMessenger.of(context)
      ..hideCurrentSnackBar()
      ..showSnackBar(
        SnackBar(
          content: Row(
            children: [
              const Icon(Icons.check_circle, color: Colors.white),
              const SizedBox(width: 12),
              Expanded(
                child: Text(
                  message,
                  style: const TextStyle(
                    color: Colors.white,
                    fontSize: 14,
                    fontWeight: FontWeight.w500,
                  ),
                ),
              ),
            ],
          ),
          backgroundColor: Colors.green.shade600,
          duration: const Duration(seconds: 3),
          behavior: SnackBarBehavior.floating,
          action: SnackBarAction(
            label: 'Dismiss',
            textColor: Colors.white,
            onPressed: () {
              ScaffoldMessenger.of(context).hideCurrentSnackBar();
            },
          ),
        ),
      );
  }

  /// Show error/failure toast notification (red background)
  static void showFailureToast(BuildContext context, String message) {
    ScaffoldMessenger.of(context)
      ..hideCurrentSnackBar()
      ..showSnackBar(
        SnackBar(
          content: Row(
            children: [
              const Icon(Icons.error, color: Colors.white),
              const SizedBox(width: 12),
              Expanded(
                child: Text(
                  message,
                  style: const TextStyle(
                    color: Colors.white,
                    fontSize: 14,
                    fontWeight: FontWeight.w500,
                  ),
                ),
              ),
            ],
          ),
          backgroundColor: Colors.red.shade600,
          duration: const Duration(seconds: 4),
          behavior: SnackBarBehavior.floating,
          action: SnackBarAction(
            label: 'Dismiss',
            textColor: Colors.white,
            onPressed: () {
              ScaffoldMessenger.of(context).hideCurrentSnackBar();
            },
          ),
        ),
      );
  }

  /// Show info toast notification (blue background)
  static void showInfoToast(BuildContext context, String message) {
    ScaffoldMessenger.of(context)
      ..hideCurrentSnackBar()
      ..showSnackBar(
        SnackBar(
          content: Row(
            children: [
              const Icon(Icons.info, color: Colors.white),
              const SizedBox(width: 12),
              Expanded(
                child: Text(
                  message,
                  style: const TextStyle(
                    color: Colors.white,
                    fontSize: 14,
                    fontWeight: FontWeight.w500,
                  ),
                ),
              ),
            ],
          ),
          backgroundColor: Colors.blue.shade600,
          duration: const Duration(seconds: 3),
          behavior: SnackBarBehavior.floating,
        ),
      );
  }
}
```

### ErrorMessages Standardization Class
```dart
// MANDATORY: Standardized error messages for consistency
class ErrorMessages {
  // Network errors
  static const String networkError = 
      'Network error. Please check your connection.';
  static const String requestTimeout = 
      'Request timed out. Please try again.';
  static const String serverError = 
      'Server error. Please try again later.';
  
  // Authentication errors
  static const String authenticationFailed = 
      'Invalid email or password.';
  static const String sessionExpired = 
      'Your session has expired. Please sign in again.';
  static const String unauthorizedAccess = 
      'You do not have permission to access this resource.';
  
  // Validation errors
  static const String invalidEmail = 
      'Please enter a valid email address.';
  static const String invalidPassword = 
      'Password must be at least 8 characters.';
  static const String requiredField = 
      'This field is required.';
  
  // Generic fallbacks
  static const String unexpectedError = 
      'An unexpected error occurred. Please try again.';
  static const String noDataAvailable = 
      'No data available.';
  static const String loadingFailed = 
      'Failed to load data. Please try again.';
  
  /// Get user-friendly error message from exception
  static String fromException(Object error) {
    final errorString = error.toString().toLowerCase();
    
    if (errorString.contains('network') || errorString.contains('socket')) {
      return networkError;
    }
    if (errorString.contains('timeout')) {
      return requestTimeout;
    }
    if (errorString.contains('server') || errorString.contains('500')) {
      return serverError;
    }
    if (errorString.contains('auth') || errorString.contains('401')) {
      return authenticationFailed;
    }
    if (errorString.contains('403')) {
      return unauthorizedAccess;
    }
    
    return unexpectedError;
  }
}
```

### BlocListener Integration for User Feedback
```dart
// MANDATORY: Automatic user feedback on state changes
// Reference: https://pub.dev/packages/flutter_bloc
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

@RoutePage()
class LoginScreen extends StatefulWidget implements AutoRouteWrapper {
  const LoginScreen({super.key});

  @override
  Widget wrappedRoute(BuildContext context) {
    return BlocProvider(
      create: (_) => getIt<AuthCubit>(),
      child: this,
    );
  }

  @override
  State<LoginScreen> createState() => _LoginScreenState();
}

class _LoginScreenState extends State<LoginScreen> {
  @override
  Widget build(BuildContext context) {
    return BlocListener<AuthCubit, AuthState>(
      // Listen only to success and error states
      listenWhen: (previous, current) {
        return current is AuthSuccess || current is AuthFailure;
      },
      listener: (context, state) {
        // Show success toast and navigate
        if (state is AuthSuccess) {
          GlobalSnackbar.showSuccessToast(
            context, 
            'Welcome back, ${state.user.name}!',
          );
          // Navigate to home
          context.router.replaceAll([const HomeRoute()]);
        }
        
        // Show error toast
        if (state is AuthFailure) {
          GlobalSnackbar.showFailureToast(context, state.error);
        }
      },
      child: Scaffold(
        appBar: AppBar(title: const Text('Sign In')),
        body: BlocBuilder<AuthCubit, AuthState>(
          builder: (context, state) {
            final isLoading = state is AuthLoading;
            
            return Padding(
              padding: const EdgeInsets.all(16.0),
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  // Email field
                  TextField(
                    decoration: const InputDecoration(
                      labelText: 'Email',
                      prefixIcon: Icon(Icons.email),
                    ),
                    onChanged: (value) {
                      context.read<AuthCubit>().updateEmail(value);
                    },
                  ),
                  const SizedBox(height: 16),
                  
                  // Password field
                  TextField(
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      prefixIcon: Icon(Icons.lock),
                    ),
                    obscureText: true,
                    onChanged: (value) {
                      context.read<AuthCubit>().updatePassword(value);
                    },
                  ),
                  const SizedBox(height: 24),
                  
                  // Sign in button with loading state
                  ElevatedButton(
                    onPressed: isLoading 
                        ? null 
                        : () => context.read<AuthCubit>().signIn(),
                    child: isLoading
                        ? const SizedBox(
                            width: 20,
                            height: 20,
                            child: CircularProgressIndicator(strokeWidth: 2),
                          )
                        : const Text('Sign In'),
                  ),
                ],
              ),
            );
          },
        ),
      ),
    );
  }
}
```

### Cubit Implementation with ErrorMessages
```dart
// MANDATORY: Use ErrorMessages for consistent error handling
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:injectable/injectable.dart';

sealed class AuthState extends Equatable {
  const AuthState();
  @override
  List<Object?> get props => [];
}

class AuthInitial extends AuthState {}
class AuthLoading extends AuthState {}

class AuthSuccess extends AuthState {
  final User user;
  const AuthSuccess(this.user);
  @override
  List<Object?> get props => [user];
}

class AuthFailure extends AuthState {
  final String error;
  const AuthFailure(this.error);
  @override
  List<Object?> get props => [error];
}

@injectable
class AuthCubit extends Cubit<AuthState> {
  final AuthRepo _authRepo;
  
  String _email = '';
  String _password = '';

  AuthCubit(this._authRepo) : super(AuthInitial());

  void updateEmail(String email) => _email = email;
  void updatePassword(String password) => _password = password;

  Future<void> signIn() async {
    // Validate inputs
    if (_email.isEmpty || _password.isEmpty) {
      emit(const AuthFailure(ErrorMessages.requiredField));
      return;
    }
    
    if (!_email.contains('@')) {
      emit(const AuthFailure(ErrorMessages.invalidEmail));
      return;
    }

    emit(AuthLoading());
    
    try {
      final response = await _authRepo.signIn(_email, _password);
      
      if (response != null && response.success) {
        emit(AuthSuccess(response.user!));
      } else {
        emit(AuthFailure(
          response?.message ?? ErrorMessages.authenticationFailed,
        ));
      }
    } catch (e) {
      // Use standardized error messages
      emit(AuthFailure(ErrorMessages.fromException(e)));
    }
  }

  Future<void> signOut() async {
    emit(AuthLoading());
    try {
      await _authRepo.signOut();
      emit(AuthInitial());
      // Note: Success toast shown by BlocListener if needed
    } catch (e) {
      emit(AuthFailure(ErrorMessages.fromException(e)));
    }
  }
}
```

### Best Practices for User Notifications

1. **Transient Feedback**: Use GlobalSnackbar for temporary notifications that auto-dismiss
2. **Consistent Messaging**: Always use ErrorMessages class for standardized error strings
3. **Visual Hierarchy**: Green for success, red for errors, blue for info
4. **Action Buttons**: Provide dismiss action for longer messages (>3 seconds)
5. **BlocListener Pattern**: Automatically show notifications on state changes
6. **Single Notification**: Always hide current SnackBar before showing new one
7. **Duration Guidelines**: 
   - Success: 3 seconds
   - Error: 4 seconds (users need more time to read errors)
   - Info: 3 seconds
8. **Accessibility**: Include icons for visual distinction and screen reader support
9. **Context Awareness**: Only show notifications for user-triggered actions or critical events
10. **Avoid Overuse**: Don't show notifications for every minor state change

## Widget Structure with AutoRoute

```dart
// Complete screen with routing and state management using GetIt DI
@RoutePage()
class FeatureScreen extends StatefulWidget implements AutoRouteWrapper {
  const FeatureScreen({super.key});

  @override
  Widget wrappedRoute(BuildContext context) {
    return MultiBlocProvider(
      providers: [
        BlocProvider(
          create: (_) => getIt<FeatureCubit>()..loadData(),
        ),
      ],
      child: this,
    );
  }

  @override
  State<FeatureScreen> createState() => _FeatureScreenState();
}

class _FeatureScreenState extends State<FeatureScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(AppLocalizations.of(context)!.featureTitle),
      ),
      body: BlocConsumer<FeatureCubit, FeatureState>(
        listener: (context, state) {
          if (state is FeatureError) {
            GlobalSnackbar.showFailureToast(context, state.message);
          }
        },
        builder: (context, state) {
          return switch (state) {
            FeatureInitial() => const Center(child: Text('Ready to load')),
            FeatureLoading() => const Center(child: CircularProgressIndicator()),
            FeatureSuccess(:final data) => _buildSuccessView(data),
            FeatureError() => const Center(child: Text('Error occurred')),
          };
        },
      ),
    );
  }
  
  Widget _buildSuccessView(Data data) {
    return ListView.builder(
      itemCount: data.items.length,
      itemBuilder: (context, index) {
        return ListTile(
          title: Text(data.items[index].name),
        );
      },
    );
  }
}
```

## Testing Patterns

### Unit Test Template
```dart
// MANDATORY: Comprehensive cubit testing
void main() {
  group('FeatureCubit', () {
    late FeatureCubit cubit;
    late MockFeatureRepo mockRepo;

    setUp(() {
      mockRepo = MockFeatureRepo();
      cubit = FeatureCubit();
    });

    tearDown(() {
      cubit.close();
    });

    test('initial state is FeatureInitial', () {
      expect(cubit.state, isA<FeatureInitial>());
    });

    test('loadData emits [Loading, Success] when successful', () async {
      when(() => mockRepo.fetchData())
          .thenAnswer((_) async => Data(items: []));

      await cubit.loadData();

      expect(cubit.state, isA<FeatureSuccess>());
    });

    test('loadData emits [Loading, Error] when fails', () async {
      when(() => mockRepo.fetchData())
          .thenThrow(Exception('Network error'));

      await cubit.loadData();

      expect(cubit.state, isA<FeatureError>());
    });
  });
}
```

### Widget Test Template
```dart
// MANDATORY: UI component testing
void main() {
  testWidgets('FeatureScreen displays data correctly', (tester) async {
    await tester.pumpWidget(
      MaterialApp(
        home: BlocProvider(
          create: (context) => FeatureCubit()..loadData(),
          child: const FeatureScreen(),
        ),
      ),
    );

    // Verify initial state
    expect(find.byType(CircularProgressIndicator), findsOneWidget);
    await tester.pumpAndSettle();

    // Verify success state
    expect(find.byType(ListView), findsOneWidget);
  });
}
```

### Integration Test Template
```dart
// MANDATORY: End-to-end flow testing
void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();

  testWidgets('complete feature flow', (tester) async {
    await tester.pumpWidget(const MyApp());

    // Navigate to feature screen
    await tester.tap(find.text('Feature'));
    await tester.pumpAndSettle();

    // Verify data loads
    expect(find.byType(ListView), findsOneWidget);

    // Interact with UI
    await tester.tap(find.byType(ListTile).first);
    await tester.pumpAndSettle();

    // Verify navigation occurred
    expect(find.byType(DetailScreen), findsOneWidget);
  });
}
```

## Performance Optimization Patterns

### Selective Rebuilds
```dart
// MANDATORY: Optimize rebuilds with selective listening
BlocSelector<FeatureCubit, FeatureState, bool>(
  selector: (state) => state is FeatureLoading,
  builder: (context, isLoading) {
    return isLoading 
      ? const CircularProgressIndicator()
      : const ContentWidget();
  },
)
```

### Memory Management
```dart
// MANDATORY: Proper subscription cleanup
class FeatureCubit extends Cubit<FeatureState> {
  StreamSubscription? _subscription;

  FeatureCubit() : super(FeatureInitial()) {
    _setupRealtimeUpdates();
  }

  void _setupRealtimeUpdates() {
    _subscription = FeatureRepo.watchData().listen(
      (data) => emit(FeatureSuccess(data)),
      onError: (error) => emit(FeatureError(error.toString())),
    );
  }

  @override
  Future<void> close() {
    _subscription?.cancel();
    return super.close();
  }
}
```

## Dependency Injection with GetIt/Injectable

### Package Setup
```yaml
# pubspec.yaml
dependencies:
  get_it: ^8.0.0           # Service locator
  injectable: ^2.5.2       # DI code generator annotations

dev_dependencies:
  injectable_generator: ^2.6.2  # Code generation
  build_runner: ^2.4.0          # Build system
```

### Setup in main.dart
```dart
// MANDATORY: Configure GetIt/Injectable for dependency injection
// Reference: https://pub.dev/packages/injectable
// Reference: https://pub.dev/packages/get_it
import 'package:get_it/get_it.dart';
import 'package:injectable/injectable.dart';
import 'injection.config.dart'; // Generated file

final getIt = GetIt.instance;

@InjectableInit(
  initializerName: 'init', // default
  preferRelativeImports: true, // default
  asExtension: true, // default
)
Future<void> configureDependencies() async => getIt.init();

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  
  // Initialize dependency injection
  await configureDependencies();
  
  // Initialize Firebase
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  
  runApp(const MyApp());
}
```

### Repository with @LazySingleton
```dart
// MANDATORY: Repositories use @lazySingleton annotation
import 'package:injectable/injectable.dart';
import 'package:stack_trace/stack_trace.dart';

@lazySingleton
class ProductRepo {
  final NetworkService _networkService;
  
  ProductRepo(this._networkService); // Constructor injection

  Future<ProductListResponse?> fetchProducts() async {
    String url = GlobalApiUrls.products;
    
    final body = ProductBodyApi(
      method: ProductApiMethods.getProducts,
    );

    final response = await _networkService.httpPostRequest(
      stackTrace: Trace.current(),
      url: url,
      body: body.toJson(),
      fromJsonFactory: (response) => ProductListResponse.fromJson(response),
    );
    return response;
  }
}
```

### Cubit with @Injectable
```dart
// MANDATORY: Cubits use @injectable annotation (factory lifecycle)
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:injectable/injectable.dart';

@injectable
class ProductListCubit extends Cubit<ProductListState> {
  final ProductRepo _productRepo;
  
  ProductListCubit(this._productRepo) : super(ProductListInitial());
  
  Future<void> loadProducts() async {
    emit(ProductListLoading());
    try {
      final response = await _productRepo.fetchProducts();
      if (response != null && response.success) {
        emit(ProductListSuccess(response.products!));
      } else {
        emit(ProductListError(response?.message ?? 'Failed to load'));
      }
    } catch (e) {
      emit(ProductListError('An error occurred'));
    }
  }
}
```

### Service with @Singleton
```dart
// MANDATORY: Services use @singleton or @lazySingleton
import 'package:injectable/injectable.dart';

@singleton
class NetworkService {
  final Dio _dio;
  
  NetworkService(this._dio);
  
  Future<T?> httpPostRequest<T>({
    required StackTrace stackTrace,
    required String url,
    required Map<String, dynamic> body,
    required T Function(Map<String, dynamic>) fromJsonFactory,
    String? token,
  }) async {
    // Implementation
  }
}
```

### Usage in Widgets with getIt
```dart
// Screen using GetIt to resolve dependencies
@RoutePage()
class ProductListScreen extends StatefulWidget implements AutoRouteWrapper {
  const ProductListScreen({super.key});

  @override
  Widget wrappedRoute(BuildContext context) {
    return BlocProvider(
      create: (_) => getIt<ProductListCubit>()..loadProducts(),
      child: this,
    );
  }
}
```

### Code Generation Command
```bash
# Generate Injectable code (requires injectable_generator in dev_dependencies)
# Reference: https://pub.dev/packages/injectable_generator
dart run build_runner build --delete-conflicting-outputs

# Or watch for changes
dart run build_runner watch

# Generated file: injection.config.dart
# This file contains all DI registrations from @injectable annotations
```

### Testing with Injectable
```dart
// Reset GetIt for testing
import 'package:get_it/get_it.dart';

void main() {
  setUp(() {
    // Reset GetIt instance before each test
    getIt.reset();
    
    // Register test mocks
    getIt.registerFactory<ProductRepo>(() => MockProductRepo());
    getIt.registerFactory<ProductListCubit>(() => MockProductListCubit());
  });
  
  test('cubit test with mocked repository', () async {
    final cubit = getIt<ProductListCubit>();
    // Test logic
  });
}
```

## Storage Patterns

### Secure Storage for Sensitive Data
```dart
// MANDATORY: Use biometric_storage for tokens, passwords, and sensitive data
import 'package:biometric_storage/biometric_storage.dart';

class SecureStorageService {
  static const String _tokenKey = 'auth_token';
  static const String _passwordKey = 'user_password';

  /// Store authentication token securely with biometric protection
  Future<void> saveAuthToken(String token) async {
    final storage = await BiometricStorage().getStorage(
      _tokenKey,
      options: StorageFileInitOptions(
        authenticationRequired: true,
        authenticationValidityDurationSeconds: 30,
      ),
    );
    await storage.write(token);
  }

  /// Retrieve authentication token (requires biometric authentication)
  Future<String?> getAuthToken() async {
    try {
      final storage = await BiometricStorage().getStorage(_tokenKey);
      return await storage.read();
    } catch (e) {
      AppLogger.e(error: e);
      return null;
    }
  }

  /// Delete stored token
  Future<void> deleteAuthToken() async {
    final storage = await BiometricStorage().getStorage(_tokenKey);
    await storage.delete();
  }
}
```

### Hive CE for Non-Sensitive Data
```dart
// MANDATORY: Use hive_ce for non-sensitive data storage
import 'package:hive_ce/hive.dart';
import 'package:hive_ce_flutter/hive_flutter.dart';

class LocalStorageService {
  static const String _settingsBox = 'app_settings';
  static const String _cacheBox = 'cache_data';

  /// Initialize Hive storage
  static Future<void> init() async {
    await Hive.initFlutter();
    await Hive.openBox(_settingsBox);
    await Hive.openBox(_cacheBox);
  }

  /// Save user preferences (non-sensitive)
  Future<void> saveUserPreference(String key, dynamic value) async {
    final box = Hive.box(_settingsBox);
    await box.put(key, value);
  }

  /// Get user preference
  T? getUserPreference<T>(String key, {T? defaultValue}) {
    final box = Hive.box(_settingsBox);
    return box.get(key, defaultValue: defaultValue) as T?;
  }

  /// Cache API response data
  Future<void> cacheData(String key, Map<String, dynamic> data) async {
    final box = Hive.box(_cacheBox);
    await box.put(key, data);
  }

  /// Get cached data
  Map<String, dynamic>? getCachedData(String key) {
    final box = Hive.box(_cacheBox);
    return box.get(key) as Map<String, dynamic>?;
  }

  /// Clear all cache
  Future<void> clearCache() async {
    final box = Hive.box(_cacheBox);
    await box.clear();
  }
}
```

## Security Patterns

### Input Validation
```dart
// MANDATORY: Comprehensive input validation
String? validateEmail(String? email) {
  if (email == null || email.isEmpty) {
    return 'Email is required';
  }
  if (!RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$').hasMatch(email)) {
    return 'Invalid email format';
  }
  return null;
}

String? validatePassword(String? password) {
  if (password == null || password.isEmpty) {
    return 'Password is required';
  }
  if (password.length < 8) {
    return 'Password must be at least 8 characters';
  }
  if (!RegExp(r'(?=.*[a-z])(?=.*[A-Z])(?=.*\d)').hasMatch(password)) {
    return 'Password must contain uppercase, lowercase, and number';
  }
  return null;
}
```

### Secure API Integration
```dart
// MANDATORY: Secure header handling
class ApiService {
  static final Map<String, String> _headers = {
    'Content-Type': 'application/json',
    'Accept': 'application/json',
  };

  static Future<T> secureRequest<T>(
    String url, {
    Map<String, dynamic>? body,
  }) async {
    // Validate HTTPS usage
    assert(url.startsWith('https://'), 'Only HTTPS requests allowed');

    final response = await http.post(
      Uri.parse(url),
      headers: _headers,
      body: jsonEncode(body),
    );

    if (response.statusCode >= 400) {
      throw ApiException(
        message: 'Request failed',
        statusCode: response.statusCode,
      );
    }

    return _parseResponse<T>(response);
  }
}
```

## Mason Brick Integration Snippets

### Project Initialization
```bash
# Complete Flutter project with backend
mason make flutter_init --projectName my_awesome_app

# Flutter project without backend
mason make flutter_init_no_backend --projectName my_app
```

### Feature Development
```bash
# Generate new screen with routing and state management
mason make new_screen --screenName user_profile

# Generate new cubit with sealed state classes
mason make new_cubit --cubitName user_settings
```

### Generated Structure
```
lib/
├── cubits/
│   └── app_cubits/
│       └── user_profile_cubit/
│           ├── cubit.dart
│           └── state.dart
├── screens/
│   └── user_profile_screen.dart
├── routes/
│   └── app_router.dart (updated)
└── repositories/
    └── user_repo.dart
```

## Navigation with AutoRoute

```dart
// Navigate to new screen
context.pushRoute(const UserProfileRoute());

// Navigate with parameters
context.pushRoute(ProductDetailRoute(productId: '123'));

// Replace current route
context.replaceRoute(const HomeRoute());

// Pop current route
context.popRoute();

// Navigate and clear stack
context.replaceRoute(const LoginRoute());
```

## Common Flutter Widgets Pattern

```dart
// Responsive layout pattern
LayoutBuilder(
  builder: (context, constraints) {
    if (constraints.maxWidth < 600) {
      return const MobileLayout();
    } else if (constraints.maxWidth < 1200) {
      return const TabletLayout();
    } else {
      return const DesktopLayout();
    }
  },
)

// Theme-aware widgets
Container(
  color: Theme.of(context).colorScheme.primary,
  child: Text(
    'Themed Text',
    style: Theme.of(context).textTheme.headlineMedium,
  ),
)

// Localized text
Text(AppLocalizations.of(context)!.welcomeMessage)
```

## Animation Patterns

```dart
// Hero animation for screen transitions
Hero(
  tag: 'product-${product.id}',
  child: Image.network(product.imageUrl),
)

// Animated container for smooth transitions
AnimatedContainer(
  duration: const Duration(milliseconds: 300),
  curve: Curves.easeInOut,
  height: isExpanded ? 200 : 100,
  child: child,
)

// Custom implicit animation
TweenAnimationBuilder<double>(
  duration: const Duration(milliseconds: 500),
  tween: Tween(begin: 0.0, end: 1.0),
  builder: (context, value, child) {
    return Opacity(
      opacity: value,
      child: child,
    );
  },
  child: YourWidget(),
)
```

## Error Handling Best Practices

```dart
// Global error handler
void setupErrorHandlers() {
  FlutterError.onError = (details) {
    AppLogger.e(
      error: details.exception,
      stackTrace: details.stack,
    );
    Sentry.captureException(
      details.exception,
      stackTrace: details.stack,
    );
  };
  
  PlatformDispatcher.instance.onError = (error, stack) {
    AppLogger.e(error: error, stackTrace: stack);
    Sentry.captureException(error, stackTrace: stack);
    return true;
  };
}

// Try-catch in business logic
Future<void> performOperation() async {
  try {
    final result = await repository.fetchData();
    emit(SuccessState(result!));
  } on NetworkException catch (e) {
    emit(ErrorState('Network error: ${e.message}'));
  } on AuthException catch (e) {
    emit(ErrorState('Authentication failed: ${e.message}'));
  } catch (e) {
    AppLogger.e(error: e, stackTrace: StackTrace.current);
    emit(ErrorState('An unexpected error occurred'));
  }
}
```

## Success Metrics for Flutter Development

### Performance Metrics
- App startup time: < 2 seconds (cold start), < 1 second (warm start)
- Frame rate: Consistent 60fps (90fps on capable devices)
- Widget rebuild count: Optimized with selective rebuilds
- Memory usage: < 150MB for typical app usage
- Bundle size: < 20MB (Android APK), < 50MB (iOS IPA)

### Code Quality Metrics
- `flutter analyze`: Zero errors, < 5 warnings
- Test coverage: > 80% for business logic, > 60% for widgets
- Build success rate: > 99% on CI/CD
- Code review approval: First-pass approval > 85%

### User Experience Metrics
- App crash rate: < 0.1%
- ANR (Application Not Responding) rate: < 0.05%
- User rating: > 4.5 stars
- Session duration: Optimized for engagement
- Feature adoption: > 40% within first week

## Flutter-Specific Communication Patterns

### Performance-Focused
- "Optimized widget rebuilds from 100/sec to 5/sec using BlocBuilder with buildWhen"
- "Reduced app startup time from 3.2s to 1.8s through lazy initialization"
- "Achieved consistent 60fps scrolling with ListView.builder optimization"

### Architecture-Focused
- "Implemented clean architecture with BLoC pattern and sealed state classes"
- "Separated business logic into repositories with injected NetworkService and class-based constants"
- "Created reusable widget library with Shadcn Flutter components"

### Mason Brick Integration
- "Generated feature scaffold using mason make new_screen in 30 seconds"
- "Initialized project with mason make flutter_init including full backend integration"
- "Created 5 new cubits with mason make new_cubit maintaining pattern consistency"

### Testing-Focused
- "Achieved 85% test coverage with unit, widget, and integration tests"
- "All cubits tested with bloc_test ensuring state transition correctness"
- "Widget tests validate UI behavior across multiple device sizes"

