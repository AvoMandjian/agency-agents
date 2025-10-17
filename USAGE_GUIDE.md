# Flutter Agency Agents - Usage Guide

## 📖 Introduction

Welcome to the Flutter Agency Agents system! This guide will help you effectively use 51 specialized AI agents to accelerate your Flutter development workflow.

### What Are Flutter Agency Agents?

Flutter Agency Agents are specialized AI assistants, each with deep expertise in a specific aspect of Flutter development. Instead of using a generalist AI that knows a little about everything, you can work with agents that have:

- **Specialized Knowledge**: Deep expertise in their domain (UI, backend, testing, etc.)
- **Proven Patterns**: Access to your project conventions and best practices
- **Workflow Integration**: Seamless integration with Mason bricks, BLoC, Serverpod
- **Quality Focus**: Built-in knowledge of Flutter performance and architecture standards

### Why Use Specialized Agents?

1. **Higher Quality Output**: Specialized agents provide more accurate, context-aware solutions
2. **Faster Development**: Agents know your conventions and patterns, reducing iteration time
3. **Consistent Patterns**: All agents follow the same architectural standards
4. **Learning Curve**: Each agent teaches best practices in their domain
5. **Team Coordination**: Agents simulate real team workflows (PM → Dev → QA)

---

## 🚀 Quick Start

### Step 1: Access Agents in Cursor IDE

1. Open your Flutter project in Cursor IDE
2. Open the chat panel (⌘+L or Ctrl+L)
3. Type `@` to see available agents
4. Type `@agency-agents/` to filter to Flutter agents

### Step 2: Choose the Right Agent

Use the agent selector pattern:
```
@agency-agents/[division]/[agent-name].md
```

**Examples**:
- `@agency-agents/engineering/engineering-frontend-developer.md` - For UI development
- `@agency-agents/testing/testing-evidence-qa.md` - For testing and QA
- `@agency-agents/engineering/engineering-backend-architect.md` - For Serverpod backend

💡 **Tip**: See [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) for a complete agent selector cheat sheet.

### Step 3: Provide Context

Give agents access to your project context:
```
@memory_bank_dual/rules/memory-bank.mdc - Project specifications
@agency-agents/.templates/flutter-patterns.md - Code patterns
```

### Step 4: Make Your Request

Be specific and clear:

✅ **Good Request**:
```
@agency-agents/engineering/engineering-frontend-developer.md

I need to create a product list screen that:
- Displays products from Serverpod API
- Uses BLoC pattern with sealed states
- Implements pull-to-refresh
- Shows loading, success, error states
- Follows our repository pattern with injected NetworkService

Target: Android and iOS, Flutter 3.27+
```

❌ **Poor Request**:
```
@agency-agents/engineering/engineering-frontend-developer.md
Make a product screen
```

### Step 5: Review and Iterate

1. Review the agent's response
2. Check code compiles and follows conventions
3. Ask follow-up questions for clarification
4. Request adjustments if needed

---

## 💼 Common Scenarios

### Scenario 1: Building a New Feature End-to-End

**Goal**: Create a complete feature from requirements to deployment

**Workflow**:
```
1. @project-management/project-manager-senior.md
   → Define requirements and create task breakdown

2. @design/design-ux-architect.md
   → Design user flows and screen layouts

3. @engineering/engineering-frontend-developer.md
   → Implement UI with BLoC pattern

4. @engineering/engineering-backend-architect.md
   → Create Serverpod endpoints and database schema

5. @testing/testing-evidence-qa.md
   → Validate functionality with comprehensive tests

6. @testing/testing-performance-benchmarker.md
   → Verify performance meets targets (60fps, <2s startup)
```

**Example Prompt** (Step 1):
```
@agency-agents/project-management/project-manager-senior.md

I need to add a shopping cart feature to our e-commerce app.

Requirements:
- Users can add/remove products from cart
- Cart persists across app sessions (using hive_ce)
- Real-time cart total calculation
- Cart badge on bottom navigation
- Integration with existing product catalog

Please create a detailed task breakdown with acceptance criteria.
```

---

### Scenario 2: Performance Optimization

**Goal**: Improve app performance to meet production standards

**Agent**: `@testing/testing-performance-benchmarker.md`

**Example Prompt**:
```
@agency-agents/testing/testing-performance-benchmarker.md
@memory_bank_dual/rules/memory-bank.mdc

My product list screen is experiencing frame drops when scrolling through 500+ items.

Current implementation:
- ListView.builder with ProductCard widgets
- Each card loads product image from network
- BlocBuilder rebuilds entire list on state changes

Performance targets:
- Maintain 60fps scrolling
- <100ms frame rendering time
- <150MB memory usage

Please analyze and provide optimization recommendations.
```

**Expected Output**:
- Performance profiling analysis
- Specific optimization strategies (lazy loading, cached_network_image, buildWhen)
- Code examples for implementing fixes
- Before/after performance metrics

---

### Scenario 3: Rapid MVP Development (2 Weeks)

**Goal**: Build and launch MVP as quickly as possible

**Agent**: `@engineering/engineering-rapid-prototyper.md`

**Example Prompt**:
```
@agency-agents/engineering/engineering-rapid-prototyper.md

I need to build a task management MVP in 2 weeks.

Core features:
- User authentication (email/password, Google sign-in)
- Create/edit/delete tasks
- Task categories and due dates
- Push notifications for reminders
- Offline support with sync

Tech stack:
- Flutter (Android + iOS)
- Serverpod + PostgreSQL backend
- Firebase Auth + Analytics + Crashlytics

Please provide:
1. Project initialization commands (Mason bricks)
2. Feature development timeline
3. Critical path items for 2-week delivery
```

**Expected Workflow**:
```bash
# Day 1: Project setup
mason make flutter_init --projectName task_manager

# Days 2-3: Auth with Serverpod Firebase Auth
mason make new_screen --screenName login
mason make new_cubit --cubitName auth

# Days 4-7: Core task features
# Days 8-10: Offline sync with hive_ce
# Days 11-12: Push notifications
# Days 13-14: Testing and polish
```

---

### Scenario 4: Testing and Quality Validation

**Goal**: Ensure feature quality before production release

**Agent**: `@testing/testing-evidence-qa.md`

**Example Prompt**:
```
@agency-agents/testing/testing-evidence-qa.md

I've completed the user profile feature. Please help me create comprehensive tests.

Feature scope:
- User can view/edit profile information
- Profile photo upload with image picker
- Email validation and password change
- Bio text with character limit (200 chars)

Current files:
- lib/screens/profile_screen.dart
- lib/cubits/profile_cubit.dart
- lib/repositories/profile_repo.dart

Please provide:
1. Unit tests for ProfileCubit (all state transitions)
2. Widget tests for ProfileScreen (validation, interactions)
3. Integration test for complete profile update flow
4. Edge case coverage (network errors, validation failures)
```

**Expected Output**:
- Complete test files for unit, widget, and integration tests
- Test coverage report expectations (>80% for cubit)
- Mock setup for dependencies (MockProfileRepo, MockNetworkService)
- Edge case validation (empty fields, network errors, concurrent updates)

---

### Scenario 5: UI/UX Design and Implementation

**Goal**: Create beautiful, accessible UI following design system

**Workflow**:
```
1. @design/design-ux-architect.md
   → Design user flows and wireframes

2. @design/design-visual-storyteller.md
   → Define visual style and brand alignment

3. @engineering/engineering-frontend-developer.md
   → Implement with Shadcn Flutter and Material Design 3
```

**Example Prompt** (Step 1):
```
@agency-agents/design/design-ux-architect.md

Design the onboarding flow for our fitness tracking app.

User goals:
- Understand app value proposition
- Set fitness goals (weight loss, muscle gain, maintenance)
- Connect wearable devices (optional)
- Complete profile setup
- See sample workout plan

Constraints:
- Must complete in <2 minutes
- 3-5 onboarding screens maximum
- Skip option for returning users
- Accessibility: WCAG AA compliance

Please provide user flow diagram and screen specifications.
```

---

### Scenario 6: API and Backend Development

**Goal**: Create scalable Serverpod endpoints with proper data modeling

**Agent**: `@engineering/engineering-backend-architect.md`

**Example Prompt**:
```
@agency-agents/engineering/engineering-backend-architect.md

I need to create API endpoints for a social feed feature.

Requirements:
- Get user feed (paginated, 20 posts per page)
- Create new post (text, optional image)
- Like/unlike posts
- Comment on posts
- Get post details with comments

Database considerations:
- Efficient pagination for large datasets
- Real-time updates for likes/comments (optional)
- Image storage with CDN integration
- User privacy controls (public/friends/private)

Tech stack:
- Serverpod 2.x
- PostgreSQL
- Firebase Storage for images

Please provide:
1. Database schema (tables, relationships, indexes)
2. Serverpod endpoint definitions
3. Flutter repository pattern implementation
4. Performance optimization strategies
```

**Expected Output**:
- Complete Serverpod protocol definitions
- PostgreSQL schema with indexes for performance
- Flutter repository with injected NetworkService
- Pagination implementation
- Error handling patterns

---

### Scenario 7: State Management Refactoring

**Goal**: Migrate from setState to BLoC pattern

**Agent**: `@engineering/engineering-frontend-developer.md`

**Example Prompt**:
```
@agency-agents/engineering/engineering-frontend-developer.md
@agency-agents/.templates/flutter-patterns.md

I need to refactor the checkout screen from setState to BLoC pattern.

Current implementation:
- StatefulWidget with setState for cart updates
- Direct API calls in widget
- Error handling with dialogs
- No loading states

Target implementation:
- CheckoutCubit with sealed states (Initial, Loading, Success, Error)
- CheckoutRepo with injected NetworkService
- GetIt/Injectable dependency injection
- GlobalSnackbar for user feedback
- Proper error handling with ErrorMessages

Current file: lib/screens/checkout_screen.dart (attached)

Please provide:
1. CheckoutState sealed class definition
2. CheckoutCubit implementation
3. CheckoutRepo with repository pattern
4. Refactored CheckoutScreen with BlocListener
```

---

### Scenario 8: Marketing and Launch Preparation

**Goal**: Prepare app for successful launch with marketing materials

**Agent**: `@marketing/marketing-marketing-director.md`

**Example Prompt**:
```
@agency-agents/marketing/marketing-marketing-director.md

Launching our productivity app in 2 weeks. Need comprehensive launch strategy.

App details:
- Name: TaskFlow
- Category: Productivity / Task Management
- Target audience: Remote workers, freelancers, small teams
- Key differentiators: AI-powered task prioritization, beautiful UX
- Platforms: iOS, Android, Web (later)

Current state:
- App development complete, in beta testing
- No marketing materials yet
- No social media presence
- Budget: $5,000 for initial launch

Please provide:
1. App Store optimization (ASO) strategy
2. Launch timeline and key milestones
3. Marketing channel recommendations
4. App Store listing content (description, screenshots, keywords)
5. Pre-launch buzz generation tactics
```

**Expected Output**:
- Complete ASO strategy with keywords and descriptions
- 2-week launch timeline with daily tasks
- Social media content calendar
- App Store assets requirements and examples
- PR and influencer outreach plan

---

### Scenario 9: Bug Fix Workflow

**Goal**: Diagnose, fix, and validate bug resolution

**Workflow**:
```
1. @testing/testing-evidence-qa.md
   → Reproduce bug and document steps

2. @engineering/engineering-frontend-developer.md (or appropriate agent)
   → Implement fix with proper error handling

3. @testing/testing-evidence-qa.md
   → Validate fix and create regression test
```

**Example Prompt** (Step 1):
```
@agency-agents/testing/testing-evidence-qa.md

Bug report from production:
- Issue: App crashes when user tries to upload profile photo
- Frequency: 15% of upload attempts
- Platform: iOS only (Android works fine)
- Error: "Invalid image format" even with JPEG files

Steps to reproduce (suspected):
1. Open profile screen
2. Tap profile photo
3. Select "Take Photo" (not "Choose from Library")
4. Take photo with camera
5. Confirm photo selection
6. App crashes

Please help me:
1. Create reliable reproduction steps
2. Document expected vs actual behavior
3. Identify root cause (iOS camera HEIC format?)
4. Suggest fix approach
```

---

### Scenario 10: Documentation Creation

**Goal**: Create comprehensive technical documentation

**Agent**: `@product/product-technical-writer.md`

**Example Prompt**:
```
@agency-agents/product/product-technical-writer.md

Need to create developer documentation for our app's architecture.

Scope:
- Project structure and organization
- State management patterns (BLoC with sealed classes)
- Repository pattern with NetworkService
- Dependency injection (GetIt/Injectable)
- Navigation with AutoRoute
- Local storage (hive_ce, biometric_storage)
- Testing strategies (unit, widget, integration)

Audience:
- New developers joining the team
- External contributors (open source)
- Technical decision makers (CTOs evaluating our stack)

Format: Markdown with code examples and diagrams

Please create documentation outline and sample sections.
```

---

## 🗣️ Agent Communication Best Practices

### How to Write Effective Prompts

#### 1. Be Specific About Requirements

✅ **Good**:
```
Optimize this ListView to maintain 60fps when scrolling through 1000 product items.
Each ProductCard has an image, title, price, and "Add to Cart" button.
```

❌ **Bad**:
```
Make my list faster.
```

#### 2. Provide Context

✅ **Good**:
```
Flutter 3.27.0, targeting Android 12+ and iOS 15+
Using flutter_bloc 8.1.6 with sealed classes
Repository pattern with injected NetworkService
```

❌ **Bad**:
```
I'm using Flutter.
```

#### 3. Reference Existing Patterns

✅ **Good**:
```
Follow the repository pattern from @agency-agents/.templates/flutter-patterns.md
Use @lazySingleton annotation and inject NetworkService
Create class-based constants (GlobalApiUrls, ProductApiMethods, ProductBodyApi)
```

❌ **Bad**:
```
Use whatever pattern you think is best.
```

#### 4. Ask for Rationale

✅ **Good**:
```
Please explain why you chose BlocProvider over BlocConsumer for this screen.
What are the trade-offs?
```

❌ **Bad**:
```
Just give me the code.
```

#### 5. Request Complete Examples

✅ **Good**:
```
Provide a complete, compilable example including:
- State definition with sealed classes
- Cubit implementation with error handling
- Repository with injected NetworkService
- Screen with BlocListener for user feedback
```

❌ **Bad**:
```
Show me how to do it.
```

---

### What NOT to Do

1. ❌ **Vague Requests**: "Make it better", "Fix this"
2. ❌ **Missing Requirements**: No acceptance criteria or success metrics
3. ❌ **No Context**: Not mentioning Flutter version, target platforms, or constraints
4. ❌ **Multiple Unrelated Tasks**: "Also add authentication and fix the bug"
5. ❌ **Assuming Agent Knowledge**: "You know what I mean"
6. ❌ **No Reference to Conventions**: Ignoring established patterns
7. ❌ **Demanding Without Reasoning**: "Just do it this way" without explaining why

---

## 🔧 Troubleshooting

### Issue 1: Agent Provides Generic Advice

**Symptom**: Agent suggests common patterns without project-specific context

**Cause**: Agent doesn't have access to your conventions

**Solution**:
```
# Include memory bank context
@memory_bank_dual/rules/memory-bank.mdc
@agency-agents/.templates/flutter-patterns.md

# Be explicit about conventions
"Use our repository pattern with injected NetworkService and class-based constants"
"Follow our DI setup with GetIt/Injectable (@lazySingleton for repos)"
```

**Prevention**: Always reference project patterns and memory bank

---

### Issue 2: Agent Suggests Wrong Pattern

**Symptom**: Agent recommends pattern that contradicts your conventions

**Example**: Agent suggests `SharedPreferences` when you use `hive_ce`

**Solution**:
```
# Correct the agent with specific reference
"According to @agency-agents/.templates/flutter-patterns.md,
we use biometric_storage for sensitive data (tokens, passwords)
and hive_ce for non-sensitive data.
Please update the implementation to use hive_ce for user preferences."
```

**Prevention**: Reference flutter-patterns.md in initial request

---

### Issue 3: Agent Misunderstands Requirements

**Symptom**: Agent delivers solution that doesn't match your needs

**Cause**: Ambiguous or incomplete requirements

**Solution**:
```
# Provide clear acceptance criteria
Requirements:
1. User can select product quantity (1-10)
2. Cart total updates in real-time
3. "Add to Cart" button disabled if quantity = 0
4. Success toast shown after adding to cart
5. Cart icon badge shows item count

Non-requirements:
- No guest checkout (users must be logged in)
- No product reviews on this screen
```

**Prevention**: Write explicit acceptance criteria upfront

---

### Issue 4: Agent Suggests Outdated Packages

**Symptom**: Agent recommends deprecated or outdated dependencies

**Solution**:
```
# Ask agent to verify with Context7
"Please verify the current version of flutter_bloc using Context7
and update the implementation to use the latest stable version."

# Reference PACKAGES_REFERENCE.md
@agency-agents/.templates/PACKAGES_REFERENCE.md
```

**Prevention**: Reference PACKAGES_REFERENCE.md for locked versions

---

### Issue 5: Code Doesn't Compile

**Symptom**: Generated code has compilation errors

**Cause**: Agent used outdated API or made syntax error

**Solution**:
```
# Request validation
"The code doesn't compile. Error message:
'The method 'showSnackBar' isn't defined for the type 'BuildContext'.'

Please validate against Flutter 3.27.0 API and update to use ScaffoldMessenger.of(context).showSnackBar()."
```

**Prevention**: Always specify exact Flutter version in initial request

---

## 📚 Next Steps

### Continue Learning

- **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)**: Fast agent selector cheat sheet
- **[TESTING_VALIDATION_GUIDE.md](./TESTING_VALIDATION_GUIDE.md)**: Quality assurance procedures
- **[AGENT_WORKFLOWS.md](./AGENT_WORKFLOWS.md)**: Multi-agent coordination patterns
- **[flutter-patterns.md](./.templates/flutter-patterns.md)**: Complete pattern library

### Get Help

- Review agent-specific documentation in `agency-agents/[division]/`
- Check `TROUBLESHOOTING.md` for common issues
- See `SUCCESS_STORIES.md` for real-world examples

---

## 🎯 Success Metrics

You're using agents effectively when you see:

1. **Faster Development**: Features complete 2-3x faster than manual coding
2. **Higher Quality**: Code follows conventions consistently (>95% compliance)
3. **Fewer Iterations**: First-pass approval rate >85%
4. **Better Tests**: Test coverage >80% for business logic
5. **Team Efficiency**: Clear handoffs between agent roles (PM → Dev → QA)
6. **Learning Curve**: New team members productive in days, not weeks

---

**Last Updated**: October 17, 2025
**Version**: 1.0.0
**Maintainer**: Flutter Agency Agents Team

