# Flutter Package Version Lock Strategy

**📦 Dependency Management & Version Control | Version 1.0.0 | Updated: Oct 17, 2025**

---

## 📖 Introduction

This document defines the version management strategy for Flutter packages used across Agency Agent projects. The strategy balances stability, security, and access to new features while minimizing breaking changes and ensuring reproducible builds.

### Why Lock Package Versions?

1. **Stability**: Prevent unexpected breaking changes from automatic updates
2. **Reproducibility**: Ensure consistent builds across all environments (dev, CI, production)
3. **Quality**: Allow thorough testing of specific package versions before adoption
4. **Team Alignment**: Ensure all developers work with same package versions
5. **Security**: Control when and how security updates are applied

### Version Management Principles (2025)

- **Caret Constraints**: Use `^X.Y.Z` for most dependencies (allows compatible updates)
- **Lock Files**: Always commit `pubspec.lock` to version control
- **Flutter SDK Management**: Use FVM to pin Flutter SDK versions per project
- **Regular Reviews**: Check for updates monthly with `flutter pub outdated`
- **Test Before Upgrade**: Never upgrade packages without comprehensive testing

---

## 🔒 Locked Packages (Strict Version Control)

These packages have **exact version constraints** due to breaking changes, API instability, or critical project dependencies.

### shadcn_flutter
**Current Version**: As specified in PACKAGES_REFERENCE.md  
**Constraint**: Exact version (no caret)  
**Reason**: Breaking changes in minor versions; UI library affects entire app appearance  
**Upgrade Policy**: Manual upgrade only, requires full UI regression testing  
**Migration Required**: Yes, for any version change

**pubspec.yaml**:
```yaml
dependencies:
  shadcn_flutter: 0.x.x  # Exact version, check PACKAGES_REFERENCE.md
```

**Upgrade Checklist**:
- [ ] Review shadcn_flutter changelog for breaking changes
- [ ] Test all screens for UI regressions
- [ ] Update design system if component APIs changed
- [ ] Run widget tests for all screens
- [ ] Get UX approval for any visual changes

---

## ✅ Safe-to-Upgrade Packages (Semantic Versioning)

These packages follow semantic versioning strictly and can be safely upgraded within major version constraints.

### flutter_bloc
**Constraint**: `^8.1.6`  
**Reason**: Stable BLoC library with strong semver compliance  
**Upgrade Policy**: Auto-upgrade for minor/patch (^), manual for major versions  
**Testing Required**: Run bloc_test suite after upgrade

### injectable
**Constraint**: `^2.5.2`  
**Reason**: DI code generator, semver compliant  
**Upgrade Policy**: Auto-upgrade with `flutter pub upgrade injectable`  
**Testing Required**: Regenerate DI code with `build_runner`, verify injections work

### auto_route
**Constraint**: `^9.2.2`  
**Reason**: Routing library with stable API  
**Upgrade Policy**: Minor/patch auto-upgrade, major requires migration  
**Testing Required**: Verify navigation flows, regenerate routes

### get_it
**Constraint**: `^8.0.0`  
**Reason**: Service locator with stable API  
**Upgrade Policy**: Auto-upgrade within major version  
**Testing Required**: Verify dependency resolution works

### hive_ce
**Constraint**: `^2.6.0`  
**Reason**: Local storage with stable API  
**Upgrade Policy**: Auto-upgrade within major version  
**Testing Required**: Verify data persistence, no migration needed for minor versions

### biometric_storage
**Constraint**: `^5.2.2`  
**Reason**: Secure storage with stable platform APIs  
**Upgrade Policy**: Auto-upgrade, test on all platforms  
**Testing Required**: Verify biometric prompts work on iOS and Android

### Firebase Packages (Analytics, Crashlytics, Auth, etc.)
**Constraint**: `^X.Y.Z` (caret for all Firebase packages)  
**Reason**: Google maintains strong semver compliance  
**Upgrade Policy**: Coordinate all Firebase package upgrades together  
**Testing Required**: Verify Firebase initialization, no deprecation warnings

---

## 📋 Upgrade Testing Checklist

Before upgrading any package, complete this checklist:

### Pre-Upgrade

- [ ] Review package changelog for breaking changes
- [ ] Check GitHub issues for known upgrade problems
- [ ] Verify Flutter SDK compatibility
- [ ] Create backup branch for rollback

### Upgrade Process

- [ ] Update `pubspec.yaml` with new version
- [ ] Run `flutter pub get` to resolve dependencies
- [ ] Run `flutter pub outdated` to check for conflicts
- [ ] Regenerate generated code (`build_runner`, `flutter gen-l10n`)
- [ ] Run `flutter analyze` - zero errors required
- [ ] Run `flutter test` - all tests must pass

### Testing

- [ ] Unit tests: All pass, no flaky tests
- [ ] Widget tests: UI renders correctly, no widget errors
- [ ] Integration tests: End-to-end flows work
- [ ] Performance validation: No degradation (60fps, <2s startup)
- [ ] Platform testing: iOS and Android both working

### Deployment

- [ ] Deploy to staging environment
- [ ] Smoke test all critical paths
- [ ] Monitor for errors/crashes (24 hours)
- [ ] Get QA approval (Reality Checker)
- [ ] Deploy to production with monitoring

### Post-Upgrade

- [ ] Monitor crash rates (expect <0.1%)
- [ ] Watch for performance regressions
- [ ] Document any issues encountered
- [ ] Update PACKAGES_REFERENCE.md if needed

---

## 🔄 Breaking Change Migration Guides

### Major Version Upgrade Process

**Example: flutter_bloc 8.x → 9.x**

1. **Research Phase**
   - Read official migration guide: https://pub.dev/packages/flutter_bloc/changelog
   - Review breaking changes and deprecated APIs
   - Estimate effort (hours/days)

2. **Preparation**
   - Create migration branch: `chore/upgrade-flutter-bloc-9`
   - Update `pubspec.yaml`: `flutter_bloc: ^9.0.0`
   - Run `flutter pub get`

3. **Code Migration**
   - Search for deprecated API usage: `grep -r "BlocProvider.of" lib/`
   - Replace with new patterns (use IDE find/replace)
   - Update all cubits to new API patterns
   - Regenerate any generated code

4. **Testing**
   - Run full test suite: `flutter test`
   - Fix failing tests (update test expectations if API changed)
   - Manual testing of all features
   - Performance validation (no regressions)

5. **Review & Deploy**
   - Code review focusing on migration quality
   - QA approval from Evidence QA
   - Staged rollout to production
   - Monitor for issues post-deployment

### Common Breaking Change Patterns

**API Signature Changes**
```dart
// Old (v8)
BlocProvider.of<AuthCubit>(context).signIn();

// New (v9 - example)
context.read<AuthCubit>().signIn();
```

**State Class Requirements**
```dart
// If new version requires different state structure
// Old
class AuthState {}

// New (if pattern changed)
sealed class AuthState extends Equatable {
  const AuthState();
}
```

**Constructor Changes**
```dart
// Check if BlocProvider/BlocListener constructors changed
// Update all usage throughout codebase
```

---

## 🔗 Version Compatibility Matrix

### Core Package Dependencies

| Package | Current Version | Compatible With | Conflicts With |
|---------|----------------|-----------------|----------------|
| flutter_bloc | ^8.1.6 | get_it ^8.0, equatable ^2.0 | flutter_bloc <7.0 |
| injectable | ^2.5.2 | get_it ^8.0 | get_it <7.0 |
| auto_route | ^9.2.2 | flutter_bloc any | - |
| hive_ce | ^2.6.0 | - | hive (original, deprecated) |
| biometric_storage | ^5.2.2 | - | flutter_secure_storage (alternative) |

### Firebase Package Coordination

**All Firebase packages must be upgraded together**:
```yaml
# Always keep these in sync
firebase_core: ^3.8.1
firebase_analytics: ^11.3.4
firebase_auth: ^5.3.3
firebase_crashlytics: ^4.1.4
```

**Reason**: Firebase packages share internal dependencies  
**Upgrade Command**: 
```bash
flutter pub upgrade firebase_core firebase_analytics firebase_auth firebase_crashlytics
```

---

## 🛠️ Flutter SDK Version Management with FVM

### Why Use FVM?

- Pin specific Flutter SDK versions per project
- Switch between Flutter versions instantly
- Ensure team uses same Flutter version
- Test against multiple Flutter versions

### FVM Setup

```bash
# Install FVM
dart pub global activate fvm

# Pin Flutter version for project
fvm use 3.27.0 --force

# Run Flutter commands via FVM
fvm flutter pub get
fvm flutter run
fvm flutter test
```

### Project Configuration

**.fvm/fvm_config.json** (committed to repo):
```json
{
  "flutterSdkVersion": "3.27.0",
  "flavors": {}
}
```

**Team Usage**:
```bash
# New team member setup
fvm install
fvm use

# Everyone uses same Flutter version automatically
```

---

## 📦 pubspec.lock Commitment Strategy

### Lock File Management

**MANDATORY**: Always commit `pubspec.lock` to version control

**Rationale**:
- Ensures identical dependency versions across all environments
- Prevents "works on my machine" dependency issues
- Required for reproducible CI/CD builds
- Critical for debugging dependency-related issues

**Git Configuration**:
```bash
# pubspec.lock should NOT be in .gitignore
# Verify it's tracked:
git ls-files | grep pubspec.lock

# If missing, add it:
git add pubspec.lock
git commit -m "chore: add pubspec.lock for reproducible builds"
```

### When to Update Lock File

- After running `flutter pub get` (adds/updates dependencies)
- After running `flutter pub upgrade` (upgrades dependencies)
- When resolving version conflicts
- After Flutter SDK version change

**Commit Message Convention**:
```bash
git commit -m "chore(deps): upgrade flutter_bloc to 8.1.6"
git commit -m "chore(deps): add new dependency biometric_storage 5.2.2"
git commit -m "chore(deps): upgrade Flutter SDK to 3.27.0"
```

---

## 🚨 Emergency Rollback Procedures

### Quick Rollback Steps

**If upgrade causes critical production issue:**

1. **Immediate Revert**
   ```bash
   # Revert pubspec.yaml and pubspec.lock
   git checkout HEAD~1 -- pubspec.yaml pubspec.lock
   flutter pub get
   
   # Rebuild and redeploy
   flutter build apk
   # Deploy previous working version
   ```

2. **Identify Root Cause**
   - Check package changelog for undocumented breaking changes
   - Review error logs and crash reports
   - Test rollback locally before production deployment

3. **Document Incident**
   - Record package version that caused issue
   - Document symptoms and resolution
   - Update VERSION_LOCK_STRATEGY.md with notes
   - Add to locked packages list if necessary

### Rollback Timeline

- **Critical (Production Down)**: Rollback within 15 minutes
- **Major Bug (Core Feature Broken)**: Rollback within 1 hour
- **Minor Issue (Edge Case)**: Fix in next release or rollback within 24 hours

---

## 🔐 Security Update Policy

### Critical Security Patches

**Override lock strategy for security updates**:

If a package has a critical security vulnerability:

1. **Immediate Action**
   - Assess vulnerability severity (CVSS score)
   - Check if app is affected
   - Plan emergency upgrade if affected

2. **Emergency Upgrade**
   - Upgrade to patched version immediately
   - Run expedited testing (critical paths only)
   - Deploy to production ASAP
   - Full testing post-deployment

3. **Communication**
   - Notify team of security upgrade
   - Document vulnerability and fix
   - Report to stakeholders if user data affected

**Example**:
```bash
# Critical security patch in http package
flutter pub upgrade http
flutter test  # Quick validation
flutter build apk
# Emergency deploy to production
```

---

## 📊 Dependency Review Schedule

### Monthly Dependency Check

**First Monday of each month:**

1. Run `flutter pub outdated`
2. Review available upgrades
3. Prioritize security updates
4. Plan non-critical upgrades for next sprint
5. Update PACKAGES_REFERENCE.md

### Quarterly Dependency Audit

**Every 3 months:**

1. Full dependency tree analysis
2. Identify unused dependencies (remove)
3. Review locked packages (still need locking?)
4. Plan major version upgrades
5. Update version compatibility matrix
6. Test with latest Flutter stable release

### Annual Dependency Strategy Review

**Once per year:**

1. Evaluate all package choices (better alternatives?)
2. Review package maintenance status (abandoned packages?)
3. Plan deprecation of old packages
4. Update lock strategy based on learnings
5. Benchmark against community best practices

---

## 📚 Related Resources

- **[PACKAGES_REFERENCE.md](./PACKAGES_REFERENCE.md)**: Current package versions and details
- **[Flutter Versioning Guide](https://docs.flutter.dev/tools/pubspec#version)**: Official pubspec documentation
- **[Dart Pub Versioning](https://dart.dev/tools/pub/dependencies)**: Semantic versioning in Dart
- **[FVM Documentation](https://fvm.app/)**: Flutter Version Management tool

---

**Version**: 1.0.0 | **Last Updated**: October 17, 2025 | **Review Schedule**: Monthly

