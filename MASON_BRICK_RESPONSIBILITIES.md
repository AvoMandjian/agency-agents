# Mason Brick Responsibilities & Maintenance

**🧱 Brick Ownership Matrix & Maintenance Workflows | Version 1.0.0 | Updated: Oct 17, 2025**

---

## 📖 Introduction

This document defines agent responsibilities for maintaining and improving the 4 local Mason bricks used across Flutter Agency Agent projects. Clear ownership ensures bricks stay current, generate high-quality code, and evolve with the Flutter ecosystem.

### Purpose

- **Assign Ownership**: Designate primary and contributing agents for each brick
- **Define Maintenance**: Establish procedures for brick updates and improvements
- **Ensure Quality**: Set standards for brick-generated code
- **Enable Evolution**: Support continuous improvement based on usage and feedback

### Mason Bricks Overview

1. **flutter_init**: Complete Flutter + Serverpod project template
2. **flutter_init_no_backend**: Flutter-only project template
3. **new_screen**: Screen + Cubit + AutoRoute integration
4. **new_cubit**: BLoC cubit with sealed state classes

**Location**: `/Users/avo/Documents/Workplace/Assets/bricks/personal/`  
**Documentation**: `/Users/avo/Documents/Workplace/Assets/bricks/docs/`

---

## 👥 Brick Ownership Matrix

| Brick | Primary Owner | Contributing Agents | Maintenance Activities |
|-------|--------------|-------------------|----------------------|
| **flutter_init** | Flutter Rapid Prototyper | Senior PM, Backend Architect, DevOps | Full project template, Serverpod integration, Firebase setup |
| **flutter_init_no_backend** | Flutter Mobile App Builder | Frontend Developer, Senior PM | Frontend-only projects, local auth simulation |
| **new_screen** | Flutter Frontend Developer | UX Architect, UI Designer | Screen scaffolding, BLoC integration, AutoRoute |
| **new_cubit** | Flutter Frontend Developer | Senior Developer | State management, sealed classes, repository pattern |

### Responsibility Breakdown

**Primary Owner**:
- Main point of contact for brick maintenance
- Reviews and approves brick changes
- Ensures brick quality and consistency
- Monitors brick usage and feedback
- Drives brick improvements and evolution

**Contributing Agents**:
- Suggests improvements based on domain expertise
- Reviews brick changes for their specialty area
- Validates generated code meets standards
- Reports issues and enhancement opportunities
- Assists with testing and validation

---

## 🔄 Brick Maintenance Workflows

### 1. Identify Improvement Need

**Triggers**:
- Agent feedback: "Generated code needs manual fixes"
- User feedback: "Brick doesn't follow latest conventions"
- Flutter ecosystem change: "New Flutter version available"
- Pattern evolution: "Better architectural pattern discovered"

**Documentation**:
```
Issue: [Description]
Brick: [flutter_init | flutter_init_no_backend | new_screen | new_cubit]
Reported by: [Agent name]
Impact: [High | Medium | Low]
Proposed Solution: [Brief description]
```

### 2. Design Update

**Primary Owner Reviews**:
- [ ] Assess impact on existing generated projects
- [ ] Design backward-compatible changes if possible
- [ ] Plan breaking changes with version bump
- [ ] Get Senior Developer approval for architectural changes
- [ ] Document design in brick issue/PR

**Design Checklist**:
- [ ] Maintains conventions from `.templates/flutter-patterns.md`
- [ ] Follows Mason best practices
- [ ] Includes test plan
- [ ] Documents migration path (if breaking)

### 3. Implement Update

**Update Process**:

1. **Update brick templates** (`__brick__/` directory)
   ```bash
   cd /Users/avo/Documents/Workplace/Assets/bricks/personal/[brick_name]
   # Edit templates in __brick__/
   ```

2. **Update brick.yaml** (if variables change)
   ```yaml
   name: brick_name
   description: Updated description
   version: 1.1.0  # Bump version (semver)
   vars:
     # Add/update variables
   ```

3. **Update hooks** (if generation logic changes)
   ```dart
   // pre_gen.dart or post_gen.dart
   // Keep hooks idempotent and deterministic
   ```

4. **Update documentation**
   ```bash
   # Update docs in /Users/avo/Documents/Workplace/Assets/bricks/docs/
   ```

### 4. Test Brick Changes

**Testing Checklist**:

- [ ] **Dry-run generation**
  ```bash
  mason make [brick_name] --dry-run
  # Review would-be generated files
  ```

- [ ] **Generate in test directory**
  ```bash
  mkdir /tmp/brick-test
  cd /tmp/brick-test
  mason make [brick_name] --projectName test_app
  ```

- [ ] **Validate generated code**
  ```bash
  cd test_app
  flutter pub get
  flutter analyze  # Must be clean
  flutter test     # All tests must pass
  flutter build apk --debug  # Must compile
  ```

- [ ] **Validate conventions**
  - [ ] Follows BLoC pattern with sealed classes
  - [ ] Uses repository pattern with injected NetworkService
  - [ ] Includes GetIt/Injectable DI setup
  - [ ] AutoRoute navigation configured
  - [ ] Storage patterns (hive_ce, biometric_storage) correct

- [ ] **Integration test with existing project**
  - Generate new feature in real project
  - Verify integrates seamlessly
  - No naming conflicts or import errors

### 5. Deploy Update

**Deployment Checklist**:

- [ ] Update `brick.yaml` version (semantic versioning)
- [ ] Update `CHANGELOG.md` with changes
- [ ] Commit changes with descriptive message
  ```bash
  git add .
  git commit -m "feat(new_screen): add GlobalSnackbar integration to generated screens"
  ```

- [ ] Tag release (for major updates)
  ```bash
  git tag brick/new_screen/v1.1.0
  git push --tags
  ```

- [ ] Update brick in Mason registry (if applicable)
  ```bash
  mason get
  ```

### 6. Document Changes

**Documentation Requirements**:

- [ ] Update brick documentation in `/docs/`
- [ ] Add migration guide (if breaking changes)
- [ ] Update examples with new features
- [ ] Update `README.md` in brick directory
- [ ] Announce changes to team/users

**Documentation Template**:
```markdown
## v1.1.0 - 2025-10-17

### Added
- GlobalSnackbar integration in generated screens
- ErrorMessages class in generated cubits

### Changed
- BlocListener now included by default
- Updated to latest flutter_bloc patterns

### Migration
1. Existing projects: Add GlobalSnackbar manually
2. New projects: Fully integrated automatically
```

---

## ✅ Quality Standards for Brick-Generated Code

### Code Quality Requirements

**MANDATORY for all brick-generated code**:

- [ ] **Compilation**: Code compiles without errors on first generation
- [ ] **Linting**: `flutter analyze` shows zero errors
- [ ] **Conventions**: Follows patterns in `.templates/flutter-patterns.md`
- [ ] **Tests**: Includes unit tests for cubits, basic widget tests for screens
- [ ] **Documentation**: Generated code has clear comments explaining purpose
- [ ] **Null Safety**: Full null safety support, no unsafe operations
- [ ] **Error Handling**: Comprehensive error handling with ErrorMessages
- [ ] **Performance**: Generated code optimized for 60fps, minimal rebuilds

### Architecture Quality

- [ ] **BLoC Pattern**: Sealed state classes, proper state transitions
- [ ] **Repository Pattern**: @lazySingleton annotation, injected NetworkService
- [ ] **Dependency Injection**: Correct @injectable/@lazySingleton usage
- [ ] **Navigation**: AutoRoute integration with type-safe routes
- [ ] **Storage**: Correct use of hive_ce (non-sensitive) and biometric_storage (sensitive)
- [ ] **UI Components**: Uses shadcn_flutter or Material Design 3 appropriately

### Testing Requirements

- [ ] **Unit Tests**: Cubit tests with bloc_test, >80% coverage
- [ ] **Widget Tests**: Basic screen rendering tests
- [ ] **Test Quality**: Meaningful assertions, proper mocks
- [ ] **Test Independence**: Tests don't rely on execution order

---

## 🧪 Brick Testing Procedures

### Pre-Deployment Testing

**Complete before any brick deployment**:

1. **Dry-Run Test**
   ```bash
   mason make [brick] --dry-run
   # Review all files that would be generated
   # Check for template errors or missing variables
   ```

2. **Fresh Generation Test**
   ```bash
   # In clean test directory
   mason make flutter_init --projectName brick_test
   cd brick_test
   
   # Validate project structure
   flutter pub get
   flutter analyze
   flutter test
   ```

3. **Integration Test**
   ```bash
   # In existing project
   mason make new_screen --screenName test_feature
   
   # Verify:
   # - No file conflicts
   # - Routes generated correctly
   # - Imports resolve
   # - Code compiles
   ```

4. **Cross-Platform Test**
   ```bash
   # Test on multiple platforms
   flutter build apk --debug    # Android
   flutter build ios --debug    # iOS (macOS only)
   flutter build web            # Web
   ```

5. **Regression Test**
   - Generate with all previous successful test cases
   - Ensure no previously working functionality broken
   - Compare output with expected results

### Post-Deployment Validation

**After brick is deployed/updated**:

- [ ] Generate in 2-3 different projects
- [ ] Gather feedback from 2-3 agents using the brick
- [ ] Monitor for any issues or complaints
- [ ] Document lessons learned
- [ ] Update testing procedures if gaps found

---

## 📊 Update & Versioning Strategy

### Semantic Versioning for Bricks

**Version Format**: `MAJOR.MINOR.PATCH`

- **MAJOR**: Breaking changes (existing generated code needs migration)
  - Example: Change in file structure, removed variables, different patterns
  - Version: 1.0.0 → 2.0.0

- **MINOR**: New features (backward compatible)
  - Example: Add new optional variables, new generated files
  - Version: 1.1.0 → 1.2.0

- **PATCH**: Bug fixes (no API changes)
  - Example: Fix template syntax, correct imports
  - Version: 1.1.1 → 1.1.2

### Change Categories

**Breaking Changes** (require migration guide):
- File structure changes
- Removed or renamed variables
- Different architectural patterns
- Incompatible with existing generated code

**New Features** (backward compatible):
- New optional variables
- Additional generated files
- Enhanced functionality
- New integrations

**Bug Fixes** (safe updates):
- Template syntax errors
- Incorrect imports
- Typos in generated code
- Performance optimizations

### Changelog Management

**CHANGELOG.md Format** (per brick):
```markdown
# Changelog

## [1.2.0] - 2025-10-17

### Added
- GlobalSnackbar integration for user feedback
- ErrorMessages standardization class

### Changed
- Updated BLoC pattern to include BlocListener by default
- Improved error handling with standardized messages

### Fixed
- Corrected import statements for NetworkService
- Fixed AutoRoute generation for nested routes

### Migration
For existing projects:
1. Add GlobalSnackbar utility class manually
2. Update cubits to use ErrorMessages class
3. Add BlocListener to screens for user feedback
```

---

## 🎯 Agent-Specific Responsibilities

### Flutter Rapid Prototyper

**Primary Owner**: `flutter_init`

**Responsibilities**:
- Keep flutter_init up-to-date with latest Serverpod patterns
- Ensure Firebase integration works out-of-box
- Optimize for speed (2-week MVP timeline)
- Validate generated project compiles immediately
- Maintain documentation for rapid setup

**Key Metrics**:
- Generation time: <2 minutes for full project
- Compile success: 100% on first `flutter run`
- Setup time: <10 minutes from generation to running app

### Flutter Frontend Developer

**Primary Owner**: `new_screen`, `new_cubit`

**Responsibilities**:
- Keep screen/cubit generators aligned with latest BLoC patterns
- Ensure GlobalSnackbar/ErrorMessages integration
- Maintain AutoRoute navigation integration
- Update for new shadcn_flutter components
- Validate UI generation quality

**Key Metrics**:
- Generation time: <30 seconds per screen/cubit
- Convention compliance: >95%
- Manual edits needed: <10% of generated code

### Flutter Mobile App Builder

**Primary Owner**: `flutter_init_no_backend`

**Responsibilities**:
- Maintain frontend-only project template
- Ensure cross-platform compatibility (iOS, Android, Web)
- Keep local auth simulation up-to-date
- Optimize for offline-first architecture

### All Agents (Contributors)

**Can Suggest Improvements**:
- Report brick-generated code that needs frequent manual fixes
- Suggest new features or variables for bricks
- Report broken or outdated patterns
- Validate brick updates during testing

**Feedback Channel**:
- Create issue in brick repository
- Tag primary owner for triage
- Provide specific examples and use cases

---

## 📚 Related Resources

- **Mason Bricks Usage Rule**: See main AI rules for detailed brick policies and allowed operations
- **Brick Documentation**: `/Users/avo/Documents/Workplace/Assets/bricks/docs/`
- **Mason Official Docs**: [docs.brickhub.dev](https://docs.brickhub.dev/)
- **flutter-patterns.md**: Code conventions that bricks must follow

---

## 🔄 Continuous Improvement Process

### Monthly Brick Review

**First Monday of each month**:
1. Review brick usage metrics (how many times each brick used)
2. Collect feedback from agents using bricks
3. Review Flutter ecosystem changes (new patterns, package updates)
4. Identify improvement opportunities
5. Prioritize updates based on impact and effort

### Quarterly Brick Audit

**Every 3 months**:
1. Full brick quality audit against current conventions
2. Test brick generation in fresh projects
3. Validate all documentation is current
4. Review brick versions for major updates
5. Plan major improvements for next quarter

### After Flutter Major Version Release

**When new Flutter stable released**:
1. Test all bricks with new Flutter version
2. Update templates for any deprecated APIs
3. Adopt new best practices from Flutter team
4. Update documentation with Flutter version requirements
5. Release updated bricks within 2 weeks of Flutter release

---

## 📋 Appendix: Quick Reference

### Brick Maintenance Commands

```bash
# Test brick locally
mason make [brick] --dry-run

# Generate for testing
mason make [brick] --projectName test

# Update brick registry
mason get

# List installed bricks
mason list
```

### Brick Quality Checklist

☐ Generated code compiles without errors  
☐ Follows `.templates/flutter-patterns.md` conventions  
☐ `flutter analyze` shows zero errors  
☐ Includes appropriate tests  
☐ Documentation is clear and complete  
☐ Version bumped according to semver  
☐ CHANGELOG.md updated  
☐ Integration tested in real project

---

**Version**: 1.0.0 | **Last Updated**: October 17, 2025 | **Bricks**: 4 | **Owners**: 4 Primary Agents

