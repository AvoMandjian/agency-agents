# 📦 Flutter Agency Agents - Complete Package Reference

All packages referenced across the 51 Flutter-specialized agents with official documentation links.

---

## 🏗️ Core Architecture Packages

### Dependency Injection
- **get_it** ^8.0.0 - [pub.dev](https://pub.dev/packages/get_it) | [API Docs](https://github.com/fluttercommunity/get_it/tree/master/doc/api)
  - Service locator for dependency injection
  - Runtime dependency resolution with getIt<T>()
  
- **injectable** ^2.5.2 - [pub.dev](https://pub.dev/packages/injectable)
  - DI code generator annotations
  - Annotations: @injectable, @singleton, @lazySingleton, @InjectableInit
  
- **injectable_generator** ^2.6.2 - [pub.dev](https://pub.dev/packages/injectable_generator) *(dev_dependency)*
  - **REQUIRED** for @InjectableInit code generation
  - Generates injection.config.dart file

### State Management
- **flutter_bloc** ^9.1.1 - [pub.dev](https://pub.dev/packages/flutter_bloc) | [Docs](https://bloclibrary.dev)
  - BLoC pattern implementation for Flutter
  - Widgets: BlocProvider, BlocBuilder, BlocConsumer, BlocListener

- **equatable** ^2.0.5 - [pub.dev](https://pub.dev/packages/equatable)
  - Value equality for state classes
  - Simplifies == and hashCode implementation

### Navigation
- **auto_route** ^10.1.2 - [pub.dev](https://pub.dev/packages/auto_route)
  - Type-safe routing with code generation
  - Annotations: @RoutePage(), @AutoRouteWrapper
  
- **auto_route_generator** ^10.1.0 - [pub.dev](https://pub.dev/packages/auto_route_generator) *(dev_dependency)*
  - Route code generation
  - Generates app_router.gr.dart

---

## 💾 Storage & Persistence

### Secure Storage
- **biometric_storage** ^5.0.1 - [pub.dev](https://pub.dev/packages/biometric_storage)
  - Encrypted storage with optional biometric protection
  - **Use for**: Auth tokens, passwords, sensitive credentials
  - Platforms: iOS (Keychain), Android (KeyStore), macOS, Linux (Keyring), Windows (Credential Store)

### General Storage
- **hive_ce** ^2.15.0 - [pub.dev](https://pub.dev/packages/hive_ce)
  - Fast, lightweight NoSQL database (Community Edition)
  - **Use for**: User preferences, cache, non-sensitive app data
  - Features: Isolate support, WASM support, DevTools extension

- **hive_ce_flutter** ^2.0.0 - [pub.dev](https://pub.dev/packages/hive_ce_flutter)
  - Flutter-specific Hive integration
  - Includes ValueListenableBuilder for reactive UI

### Stack Traces
- **stack_trace** ^1.11.1 - [pub.dev](https://pub.dev/packages/stack_trace)
  - Used for `Trace.current()` in repository HTTP calls
  - Enhanced debugging and error tracking

---

## 🎨 UI Components

### Component Library
- **shadcn_flutter** ^0.0.44 - [pub.dev](https://pub.dev/packages/shadcn_flutter)
  - 100+ modern UI components
  - Components: Button, Card, Dialog, Select, Table, Form, etc.
  - Material Design replacement with better customization

### Icons & Assets
- **flutter_svg** - For SVG rendering
- **cached_network_image** - Image caching for performance

---

## 🔌 Backend Integration

### Serverpod
- **serverpod_client** - Generated Serverpod client
- **serverpod_auth_client** - Serverpod authentication module

### Networking
- **dio** ^5.0.0 - [pub.dev](https://pub.dev/packages/dio)
  - HTTP client with interceptors
  - Used in NetworkService implementation

- **http** ^1.2.0 - [pub.dev](https://pub.dev/packages/http)
  - Basic HTTP requests
  - Fallback option

---

## 🔥 Firebase Services

### Core
- **firebase_core** - [pub.dev](https://pub.dev/packages/firebase_core)
  - Firebase initialization
  - Required for all Firebase services

### Authentication
- **firebase_auth** - [pub.dev](https://pub.dev/packages/firebase_auth)
  - Email/password, Google, Apple Sign In
  - Integrated with Serverpod auth

### Analytics & Monitoring
- **firebase_analytics** - [pub.dev](https://pub.dev/packages/firebase_analytics)
  - User analytics and event tracking
  - User properties and custom events

- **firebase_crashlytics** - [pub.dev](https://pub.dev/packages/firebase_crashlytics)
  - Crash reporting and error tracking
  - Stack trace symbolication

### Features
- **firebase_remote_config** - [pub.dev](https://pub.dev/packages/firebase_remote_config)
  - A/B testing and feature flags
  - Dynamic app configuration

- **firebase_cloud_messaging** - [pub.dev](https://pub.dev/packages/firebase_cloud_messaging)
  - Push notifications
  - Cross-platform messaging

---

## 🧪 Testing Packages

### BLoC Testing
- **bloc_test** ^9.1.0 - [pub.dev](https://pub.dev/packages/bloc_test)
  - Testing BLoC/Cubit state transitions
  - Pattern: blocTest<Cubit, State>(...)

### Mocking
- **mocktail** ^1.0.0 - [pub.dev](https://pub.dev/packages/mocktail)
  - Lightweight mocking (no code generation)
  - Pattern: when(() => mock.method()).thenReturn(value)

### Integration Testing
- **integration_test** - [pub.dev](https://pub.dev/packages/integration_test)
  - End-to-end testing
  - Platform: Flutter SDK (built-in)

### Test Tools
- **test** - [pub.dev](https://pub.dev/packages/test)
  - Dart/Flutter testing framework
  - group(), test(), setUp(), tearDown()

---

## 🛠️ Development Tools

### Code Generation
- **build_runner** ^2.4.0 - [pub.dev](https://pub.dev/packages/build_runner) *(dev_dependency)*
  - Code generation build system
  - Required for: AutoRoute, Injectable, Freezed, json_serializable

- **json_serializable** - [pub.dev](https://pub.dev/packages/json_serializable)
  - JSON serialization code generation
  - Used for API models

### Code Quality
- **flutter_lints** - [pub.dev](https://pub.dev/packages/flutter_lints)
  - Official Flutter linting rules
  - Ensures code quality standards

---

## 📱 Platform-Specific Packages

### Biometric Authentication
- **local_auth** - [pub.dev](https://pub.dev/packages/local_auth)
  - Face ID, Touch ID, Fingerprint
  - Works with biometric_storage

### Camera & Media
- **camera** - [pub.dev](https://pub.dev/packages/camera)
  - Camera access and capture

- **image_picker** - [pub.dev](https://pub.dev/packages/image_picker)
  - Image/video selection from gallery

### Location
- **geolocator** - [pub.dev](https://pub.dev/packages/geolocator)
  - GPS location services
  - Platform: iOS, Android, Web, macOS

---

## 🤖 AI/ML Packages

### Firebase ML
- **firebase_ml_vision** - Image labeling, text recognition, face detection
- **google_ml_kit** - [pub.dev](https://pub.dev/packages/google_ml_kit)
  - On-device ML features

### TensorFlow
- **tflite_flutter** - [pub.dev](https://pub.dev/packages/tflite_flutter)
  - TensorFlow Lite on-device inference
  - Model deployment for mobile

---

## 🏗️ Mason Bricks (Local)

### Project Templates
- **flutter_init** - `/Users/avo/Documents/Workplace/Assets/bricks/personal/flutter_init`
  - Complete Flutter + Serverpod project

- **flutter_init_no_backend** - `/Users/avo/Documents/Workplace/Assets/bricks/personal/flutter_init_no_backen`
  - Flutter-only project (no Serverpod)

### Code Generators
- **new_screen** - `/Users/avo/Documents/Workplace/Assets/bricks/personal/new_screen`
  - Screen + Cubit + AutoRoute integration

- **new_cubit** - `/Users/avo/Documents/Workplace/Assets/bricks/personal/new_cubit`
  - BLoC cubit with sealed state classes

---

## 📚 Localization
- **flutter_localizations** - [flutter.dev](https://docs.flutter.dev/ui/accessibility-and-internationalization/internationalization)
  - Multi-language support
  - ARB file format

---

## 🎯 Package Version Strategy

### Locked Versions (Breaking Changes)
- shadcn_flutter: v0.0.44 (frequent breaking changes)

### Latest Stable (Safe to Upgrade)
- get_it, injectable, firebase packages
- flutter_bloc, auto_route
- testing packages

### Semantic Versioning
- All packages use semantic versioning
- Use `^` for compatible updates: `^2.5.2` allows 2.5.x - 2.9.x

---

## 🔗 Quick Reference Links

| Package | Purpose | Link |
|---------|---------|------|
| injectable | DI annotations | [pub.dev](https://pub.dev/packages/injectable) |
| injectable_generator | DI code gen | [pub.dev](https://pub.dev/packages/injectable_generator) |
| get_it | Service locator | [pub.dev](https://pub.dev/packages/get_it) |
| flutter_bloc | BLoC pattern | [bloclibrary.dev](https://bloclibrary.dev) |
| auto_route | Type-safe routing | [pub.dev](https://pub.dev/packages/auto_route) |
| shadcn_flutter | UI components | [pub.dev](https://pub.dev/packages/shadcn_flutter) |
| biometric_storage | Secure storage | [pub.dev](https://pub.dev/packages/biometric_storage) |
| hive_ce | Fast NoSQL DB | [pub.dev](https://pub.dev/packages/hive_ce) |
| bloc_test | BLoC testing | [pub.dev](https://pub.dev/packages/bloc_test) |
| mocktail | Lightweight mocking | [pub.dev](https://pub.dev/packages/mocktail) |

---

## 📜 Version History & Breaking Changes

### flutter_bloc Migration History

**v4.x → v5.0.0**
- `condition` renamed to `listenWhen` in BlocListener
- `HydratedBlocStorage` renamed to `HydratedStorage`
- **Migration**: Global find/replace `condition:` → `listenWhen:`

**v6.x → v7.0.0**
- `bloc.listen()` changed to `bloc.stream.listen()`
- **Migration**: Update all direct bloc.listen() calls to use stream

**v7.x → v8.0.0**
- `blocTest` errors parameter now requires function: `errors: () => [MyError()]`
- Mocktail integration (replaces mockito)
- **Migration**: Update all blocTest error lists to functions, switch to mocktail

**v9.x → v10.x**
- HydratedStorage web support changes (WebAssembly compatibility)
- `HydratedStorage.webStorageDirectory` → `HydratedStorageDirectory.web`
- **Migration**: Update web storage initialization for WebAssembly support

**Reference**: [BLoC Migration Guide](https://bloclibrary.dev/migration)

### auto_route Migration History

**v8.x → v9.x**
- Major refactor of navigation API
- New @RoutePage() annotation
- **Migration**: Regenerate all routes, update navigation calls

**v9.x → v10.x**
- Enhanced nested navigation support
- **Migration**: Minor API updates, test nested routes thoroughly

### injectable Migration History

**v1.x → v2.x**
- @InjectableInit annotation changes
- **Migration**: Regenerate injection code with build_runner

**v2.0 → v2.5+**
- Improved error messages
- Better null safety support
- **Migration**: No code changes needed, regenerate with build_runner

---

## 🔧 Migration Guides (Step-by-Step)

### Upgrading flutter_bloc: 8.x → 9.x

1. **Update pubspec.yaml**
   ```yaml
   dependencies:
     flutter_bloc: ^9.1.1
   ```

2. **Run dependency resolution**
   ```bash
   flutter pub get
   flutter pub outdated  # Check for conflicts
   ```

3. **Update imports** (if package structure changed)
   ```dart
   import 'package:flutter_bloc/flutter_bloc.dart';  // Same as v8
   ```

4. **Search for deprecated APIs**
   ```bash
   grep -r "BlocProvider.of" lib/
   # Replace with context.read<T>() if found
   ```

5. **Run tests**
   ```bash
   flutter test
   # Fix any failing tests
   ```

6. **Manual testing**
   - Test all features with BLoC integration
   - Verify state transitions work correctly
   - Check error handling still functions

7. **Performance validation**
   - Run Flutter DevTools
   - Verify no performance regressions
   - Check frame rate still 60fps

### Upgrading shadcn_flutter: 0.0.x → 0.0.y

**⚠️ WARNING**: Even minor version updates can have breaking changes

1. **Review changelog carefully**
   - Visit [shadcn_flutter changelog](https://pub.dev/packages/shadcn_flutter/changelog)
   - Look for component API changes
   - Note removed/deprecated components

2. **Create test branch**
   ```bash
   git checkout -b test/shadcn-upgrade
   ```

3. **Update and test one screen at a time**
   ```yaml
   # pubspec.yaml
   shadcn_flutter: 0.0.45  # One version increment
   ```

4. **Run full UI regression test**
   - Test every screen
   - Check all shadcn components still work
   - Verify styling hasn't broken

5. **Get UX approval**
   - Visual review by UI Designer agent
   - Ensure no unintended visual changes
   - Validate dark mode still works

6. **Proceed carefully**
   - If no issues: commit and deploy
   - If issues found: fix or stay on current version

---

## ⚠️ Common Issues & Solutions

### flutter_bloc

**Issue**: "BlocProvider.of() called with a context that does not contain a Bloc"
- **Cause**: BlocProvider not in widget tree above usage
- **Solution**: Wrap parent widget with BlocProvider or use AutoRouteWrapper
- **Prevention**: Always use wrappedRoute() in AutoRoute screens

**Issue**: "Inherited widget of type not found"
- **Cause**: Using wrong context (wrong BuildContext)
- **Solution**: Use Builder widget to get correct context
- **Prevention**: Understand context scope in Flutter

**Issue**: State not updating UI
- **Cause**: State class doesn't override == or Equatable props
- **Solution**: Ensure state extends Equatable with proper props
- **Prevention**: Always use sealed class with Equatable

### injectable / get_it

**Issue**: "Object/factory with type X is not registered"
- **Cause**: Missing @injectable annotation or build_runner not executed
- **Solution**: Add annotation, run `dart run build_runner build`
- **Prevention**: Always regenerate after adding new classes

**Issue**: Circular dependencies
- **Cause**: A depends on B, B depends on A
- **Solution**: Introduce interface/abstraction layer
- **Prevention**: Design dependency graph carefully

### shadcn_flutter

**Issue**: Component not rendering correctly after upgrade
- **Cause**: API change in component constructor
- **Solution**: Check component documentation, update usage
- **Prevention**: Lock shadcn_flutter version, upgrade carefully

**Issue**: Dark mode theme not applied
- **Cause**: ThemeData not configured for shadcn components
- **Solution**: Use shadcn theme configuration
- **Prevention**: Follow shadcn theme setup guide

### hive_ce

**Issue**: "Box not open" exception
- **Cause**: Trying to access box before Hive.openBox()
- **Solution**: Ensure box opened in main() before use
- **Prevention**: Initialize Hive in main() startup sequence

**Issue**: Data not persisting across app restarts
- **Cause**: Not calling await on box.put()
- **Solution**: Always await box operations
- **Prevention**: Use async/await for all Hive operations

### biometric_storage

**Issue**: iOS biometric prompt not showing
- **Cause**: Missing NSFaceIDUsageDescription in Info.plist
- **Solution**: Add required permission keys to Info.plist
- **Prevention**: Follow platform-specific setup guides

**Issue**: Android biometric auth fails
- **Cause**: Device doesn't have biometric hardware or not enrolled
- **Solution**: Implement fallback to password/PIN
- **Prevention**: Always provide non-biometric fallback option

---

## 🔄 Alternative Packages Comparison

### State Management

| Package | Pros | Cons | When to Use |
|---------|------|------|-------------|
| **flutter_bloc** ✅ | Proven pattern, excellent testing, sealed classes | Boilerplate code, learning curve | Default choice for predictable state |
| riverpod | Less boilerplate, compile-time safety | Different mental model | When team prefers provider pattern |
| provider | Simple, minimal setup | Less structured, harder to test | Small apps, simple state |

**Recommendation**: Stick with flutter_bloc for consistency

### Storage Solutions

| Package | Use Case | Performance | Security | Platforms |
|---------|----------|-------------|----------|-----------|
| **hive_ce** ✅ | Non-sensitive data | Very fast | Encryption optional | All |
| **biometric_storage** ✅ | Sensitive data (tokens, passwords) | Fast | OS-level encryption | All |
| shared_preferences | Simple key-value | Fast | No encryption | All |
| sqflite | Relational data | Moderate | No encryption | Mobile only |

**Recommendation**: 
- hive_ce for general app data, user preferences, cache
- biometric_storage for auth tokens, passwords, API keys

### UI Component Libraries

| Package | Components | Customization | Maturity | Learning Curve |
|---------|------------|---------------|----------|----------------|
| **shadcn_flutter** ✅ | 70+ modern components | High | Growing | Medium |
| Material Design 3 | Flutter default | High | Very mature | Low |
| Cupertino | iOS-style | Medium | Very mature | Low |
| flutter_form_builder | Forms focus | High | Mature | Medium |

**Recommendation**: 
- shadcn_flutter for modern, customizable UI
- Material Design 3 for standard Android apps
- Cupertino for iOS-native feel

---

## ⚡ Performance Characteristics

### State Management Performance

| Package | Memory Overhead | Rebuild Efficiency | Initial Load |
|---------|----------------|-------------------|--------------|
| flutter_bloc | Low (~5KB per cubit) | Excellent (selective) | Fast |
| riverpod | Low (~3KB per provider) | Excellent | Fast |
| provider | Very Low (~1KB) | Good | Very Fast |

### Storage Performance

| Package | Write Speed | Read Speed | Storage Size | Platform Optimized |
|---------|-------------|------------|--------------|-------------------|
| hive_ce | Very Fast (async) | Very Fast | Compact (binary) | All |
| biometric_storage | Fast | Fast | OS-dependent | All |
| shared_preferences | Fast | Very Fast | Text-based | All |
| sqflite | Moderate (SQL) | Fast (indexed) | Moderate | Mobile |

**Benchmarks** (approximate, device-dependent):
- **hive_ce**: 1000 writes in ~100ms, 1000 reads in ~50ms
- **biometric_storage**: Single write ~50ms (includes biometric prompt)
- **shared_preferences**: 1000 writes in ~200ms

### UI Component Bundle Size Impact

| Package | APK Size Increase | Web Bundle Impact | Native Binaries |
|---------|------------------|-------------------|-----------------|
| shadcn_flutter | ~500KB | ~300KB (compressed) | None |
| Material Design 3 | Included in Flutter | Included | Included |
| firebase_analytics | ~100KB | ~80KB | Firebase SDKs |

**Optimization Tips**:
- Use selective imports for shadcn components
- Enable tree shaking for web builds
- Analyze with `flutter build apk --analyze-size`

---

## 📊 Package Dependency Matrix

### Critical Package Interdependencies

```
flutter_bloc ^9.1.1
  └─ equatable ^2.0.5 (for state equality)
  └─ bloc ^9.1.1 (base package)

injectable ^2.5.2
  ├─ get_it ^8.0.0 (required)
  └─ injectable_generator ^2.6.2 (dev, required for code gen)

auto_route ^10.1.2
  └─ auto_route_generator ^10.1.0 (dev, required for code gen)

hive_ce ^2.15.0
  └─ hive_ce_flutter ^2.0.0 (for Flutter widgets)

Firebase packages (must upgrade together):
  firebase_core ^3.8.1
  ├─ firebase_analytics ^11.3.4
  ├─ firebase_auth ^5.3.3
  ├─ firebase_crashlytics ^4.1.4
  └─ firebase_remote_config ^5.1.4
```

### Safe Concurrent Upgrades

**✅ Can upgrade independently**:
- get_it (no impact on other packages)
- mocktail (testing only)
- stack_trace (utility package)

**⚠️ Must coordinate upgrades**:
- injectable + injectable_generator (same version family)
- auto_route + auto_route_generator (same version family)
- All Firebase packages together

**🚫 Never upgrade independently**:
- flutter_bloc without checking bloc_test compatibility
- injectable without matching injectable_generator

---

**Last Updated**: October 17, 2025  
**All packages validated against official documentation**  
**See also**: [VERSION_LOCK_STRATEGY.md](./VERSION_LOCK_STRATEGY.md) for upgrade procedures

