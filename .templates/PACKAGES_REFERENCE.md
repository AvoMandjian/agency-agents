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

**Last Updated**: October 17, 2025  
**All packages validated against official documentation**

