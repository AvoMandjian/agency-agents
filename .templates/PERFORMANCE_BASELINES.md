# Flutter Performance Baselines & Standards

**⚡ Performance Targets for Production Flutter Apps | Version 1.0.0 | Updated: Oct 17, 2025**

---

## 📖 Introduction

This document defines performance baselines and targets for Flutter applications developed by Agency Agents. These standards ensure consistent, high-quality user experiences and efficient development workflows.

### Purpose

- Establish measurable performance targets for production apps
- Define validation criteria for Performance Benchmarker agent
- Set quality gates for Reality Checker agent approval
- Guide optimization decisions during development
- Enable performance regression detection

### Performance Philosophy

**User Experience First**: Performance targets based on user perception thresholds  
**Data-Driven**: All targets backed by research and real-world Flutter app data  
**Achievable**: Targets realistic for typical Flutter apps (not theoretical limits)  
**Monitored**: Continuous monitoring in production to maintain standards

**Reference**: Based on 2025 Flutter performance research showing 60fps standard, ~25MB memory baseline, and fast startup capabilities.

---

## 📱 App Performance Targets

### Frame Rate & Rendering

**Target: 60fps (16.67ms per frame) minimum**

- **Scrolling**: Smooth 60fps during ListView/GridView scrolling with 100+ items
- **Animations**: All animations maintain 60fps (no dropped frames)
- **Transitions**: Screen transitions complete smoothly at 60fps
- **Interactions**: Button taps, gestures respond within one frame
- **Stretch Goal**: 90fps on capable devices (120Hz displays)

**Measurement**:
```bash
# Flutter DevTools Timeline
# 1. Open DevTools
flutter run --profile
# 2. Navigate to Performance tab
# 3. Record timeline during interaction
# 4. Verify frame render time <16.67ms (60fps) or <11.11ms (90fps)
```

**Validation Criteria**:
- ✅ No frames >16.67ms during normal usage
- ✅ No jank (frame >100ms) during animations
- ✅ 99th percentile frame time <20ms

### Startup Time

**Targets**:
- **Cold Start**: <2 seconds (app not in memory)
- **Warm Start**: <1 second (app in background)
- **Hot Reload**: <1 second (development only)

**Measurement**:
```bash
# Android
adb shell am start -W [package_name]/[activity_name]
# Look for "TotalTime" value

# iOS
# Use Xcode Instruments → Time Profiler
# Measure time from app launch to first frame rendered

# Flutter DevTools
# Use Performance tab → Timeline
# Measure "Time to First Frame"
```

**Validation Criteria**:
- ✅ 95th percentile cold start <2.5s
- ✅ Average warm start <1s
- ✅ No blocking operations during startup

### Memory Usage

**Targets**:
- **Baseline**: <50MB on app launch (empty state)
- **Typical Usage**: <150MB during normal app usage
- **Peak Usage**: <250MB during heavy operations (image loading, data processing)
- **Memory Leaks**: Zero detectable memory leaks

**Measurement**:
```bash
# Flutter DevTools Memory tab
flutter run --profile
# Navigate to Memory tab
# Monitor memory over 5-minute usage session
# Force GC and check for memory leak patterns
```

**Validation Criteria**:
- ✅ Memory stable over time (no unbounded growth)
- ✅ Memory released after heavy operations complete
- ✅ No memory leaks detected in 10-minute session

### App Size

**Targets**:
- **Android APK**: <20MB (release build)
- **Android App Bundle**: <15MB (with splits)
- **iOS IPA**: <50MB (App Store)
- **Web Bundle**: <5MB initial load (gzipped)

**Measurement**:
```bash
# Android APK size
flutter build apk --release --analyze-size
# Check "app-release.apk" size

# iOS IPA size
flutter build ios --release
# Check .ipa size in Xcode

# Web bundle size
flutter build web --release
# Check build/web/ total size
```

**Validation Criteria**:
- ✅ APK <20MB for standard app
- ✅ Tree shaking eliminates unused code
- ✅ Images optimized (WebP, proper resolutions)

---

## 🛠️ Development Tools Performance

### Static Analysis

**Target**: `flutter analyze` completes in <10 seconds

**Validation**:
```bash
time flutter analyze
# Should complete in <10s for typical project
```

**Criteria**:
- ✅ Zero errors
- ✅ <5 warnings per 1000 lines of code
- ✅ Analysis time <10s for <10K lines

### Testing Performance

**Targets**:
- **Unit Tests**: <60 seconds for 100 tests
- **Widget Tests**: <90 seconds for 50 widget tests
- **Integration Tests**: <5 minutes per test suite
- **Total Test Suite**: <10 minutes for full suite

**Measurement**:
```bash
# Time full test suite
time flutter test
# Should complete in <10min for typical app
```

**Validation Criteria**:
- ✅ Unit tests fast (<1s per test average)
- ✅ Widget tests reasonable (<2s per test average)
- ✅ No flaky tests (100% pass rate consistently)

### Build Performance

**Targets**:
- **Clean Build**: <5 minutes (first time)
- **Incremental Build**: <1 minute (after code change)
- **Hot Reload**: <1 second (during development)
- **CI/CD Full Pipeline**: <10 minutes (analyze, test, build)

**Measurement**:
```bash
# Clean build time
flutter clean
time flutter build apk --debug

# Incremental build (change one file and rebuild)
# Edit file
time flutter build apk --debug
```

**Validation Criteria**:
- ✅ Clean build <5min
- ✅ Incremental build <1min
- ✅ CI/CD pipeline <15min total

---

## 🌐 Network Performance

### API Response Times

**Targets** (p95 percentile):
- **Critical Endpoints** (auth, checkout): <500ms
- **Standard Endpoints** (fetch data): <1s
- **Background Operations** (sync, analytics): <3s

**Measurement**:
```dart
// In NetworkService, log request duration
final stopwatch = Stopwatch()..start();
final response = await _dio.post(url, data: body);
stopwatch.stop();
AppLogger.d('API ${url} took ${stopwatch.elapsedMilliseconds}ms');
```

**Validation Criteria**:
- ✅ p95 response time <500ms for critical paths
- ✅ p99 response time <2s
- ✅ Timeout handling after 10s

### Offline-First Support

**Requirements**:
- **Core Features**: Work offline (cached data)
- **Sync**: Background sync when online
- **User Feedback**: Clear online/offline indicators

**Validation**:
- Enable airplane mode
- Verify core features accessible
- Verify sync occurs when back online

---

## 🏗️ Build & CI/CD Performance

### CI/CD Pipeline Targets

**Total Pipeline Duration**: <10 minutes

**Breakdown**:
- **Checkout Code**: <30s
- **Install Dependencies**: <2min (with caching)
- **Code Analysis**: <1min (`flutter analyze`)
- **Unit Tests**: <3min (`flutter test`)
- **Build APK/IPA**: <5min
- **Deploy**: <1min

**Optimization Strategies**:
- Cache `flutter pub get` dependencies
- Parallelize test execution
- Use faster CI runners for builds
- Skip unnecessary builds (lint-only changes)

---

## 📊 Performance Monitoring

### Production Monitoring

**Track Continuously**:
- App startup time (Firebase Performance Monitoring)
- Frame rendering time (Flutter timeline)
- Memory usage patterns (Firebase Crashlytics)
- API response times (custom instrumentation)
- Crash rate (<0.1% target)
- ANR rate (<0.05% target)

### Alerting Thresholds

**Trigger alerts when**:
- Startup time >3s (p95)
- Frame rate drops below 55fps
- Memory usage >200MB sustained
- API p95 response >1s
- Crash rate >0.2%

---

## 🎯 Performance Validation Checklist

### Pre-Production Validation

Before Reality Checker approval, verify:

☐ **Frame Rate**
  - [ ] 60fps maintained during scrolling
  - [ ] Animations smooth (no dropped frames)
  - [ ] No jank during screen transitions

☐ **Startup Time**
  - [ ] Cold start <2s on mid-range device
  - [ ] Warm start <1s
  - [ ] No blocking operations in main()

☐ **Memory**
  - [ ] Baseline <50MB
  - [ ] Typical usage <150MB
  - [ ] No memory leaks in 10min session

☐ **Network**
  - [ ] Critical APIs <500ms (p95)
  - [ ] Proper timeout handling (10s)
  - [ ] Offline mode functional

☐ **Build Size**
  - [ ] APK <20MB
  - [ ] Code analysis shows no huge dependencies
  - [ ] Tree shaking enabled for web

---

## 🔧 Optimization Strategies

### When Performance Below Target

**Frame Rate Issues** (<60fps):
1. Use Flutter DevTools Timeline to identify bottleneck
2. Check for expensive `build()` methods (use const constructors)
3. Optimize with `buildWhen` in BlocBuilder
4. Use RepaintBoundary for complex widgets
5. Implement lazy loading with ListView.builder

**Startup Time Issues** (>2s):
1. Defer heavy initialization (use lazy loading)
2. Move network calls after first frame
3. Optimize dependency injection initialization
4. Use splash screen effectively

**Memory Issues** (>150MB):
1. Check for memory leaks (unclosed streams, subscriptions)
2. Optimize image loading (use cached_network_image)
3. Dispose controllers and listeners properly
4. Use ListView.builder (not ListView with all items)

**Network Issues** (>500ms):
1. Optimize Serverpod queries (use indexes)
2. Implement caching (hive_ce)
3. Use pagination for large datasets
4. Consider GraphQL for flexible queries

---

**Version**: 1.0.0 | **Last Updated**: October 17, 2025 | **Standards**: Based on 2025 Flutter performance research

