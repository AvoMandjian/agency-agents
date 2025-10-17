# Flutter Agency Agents - Troubleshooting Guide

**🔧 Common Issues & Solutions | Version 1.0.0 | Updated: Oct 17, 2025**

---

## 📖 Introduction

This guide addresses common issues encountered when working with Flutter Agency Agents, including agent misunderstandings, incorrect guidance, missing context, and convention conflicts.

---

## ⚠️ Common Agent Issues

### Issue 1: Agent Provides Generic/Outdated Advice

**Symptom**: Agent suggests patterns that don't match your conventions

**Example**:
- Agent suggests `SharedPreferences` when you use `hive_ce`
- Agent recommends `Provider` when you use `flutter_bloc`
- Agent suggests static repository methods when you use injected NetworkService

**Solution**:
```
Correct the agent with specific references:

"According to @agency-agents/.templates/flutter-patterns.md,
we use:
- biometric_storage for sensitive data (tokens, passwords)
- hive_ce for non-sensitive data
- Repository pattern with @lazySingleton and injected NetworkService

Please update the implementation to follow our conventions."
```

**Prevention**:
- Always reference `@agency-agents/.templates/flutter-patterns.md` in initial prompt
- Include `@memory_bank_dual/rules/memory-bank.mdc` for project context
- Specify exact Flutter version and package versions

---

### Issue 2: Agent Misunderstands Requirements

**Symptom**: Agent delivers solution that doesn't match your needs

**Cause**: Ambiguous or incomplete requirements

**Example**:
- You asked for "shopping cart" and got full checkout flow with payment
- You wanted basic list and got paginated infinite scroll
- You expected simple screen and got complex multi-step wizard

**Solution**:
```
Provide explicit acceptance criteria:

"Requirements:
1. User can add product to cart (quantity 1-10)
2. Cart icon shows item count badge
3. 'Add to Cart' shows success toast
4. Cart persists using hive_ce

Non-requirements (out of scope):
- No checkout flow
- No payment integration
- No cart page (just badge counter)

Please implement exactly these requirements, nothing more."
```

**Prevention**:
- Write SMART acceptance criteria (Specific, Measurable, Achievable, Relevant, Time-bound)
- Explicitly state what's NOT in scope
- Provide wireframes or examples when possible

---

### Issue 3: Agent Code Doesn't Compile

**Symptom**: Generated code has compilation errors

**Common Errors**:
- Import errors: Package not in pubspec.yaml
- API errors: Using deprecated or incorrect APIs
- Type errors: Incorrect generic types
- Syntax errors: Invalid Dart syntax

**Solutions**:

**Import Errors**:
```
"The code doesn't compile. Error:
'package:injectable/injectable.dart' not found

Please add injectable to pubspec.yaml dependencies and regenerate the code."
```

**API Errors**:
```
"The code uses deprecated API ScaffoldMessenger.showSnackBar.
Please update to use ScaffoldMessenger.of(context).showSnackBar() 
as per Flutter 3.27 documentation."
```

**Prevention**:
- Always specify exact Flutter version in prompt
- Request agent to verify against Context7 documentation
- Ask agent to validate code compiles before providing

---

### Issue 4: Agent Ignores Established Patterns

**Symptom**: Agent creates code that doesn't match project architecture

**Example**:
- Agent uses StatefulWidget with setState instead of BLoC
- Agent creates repository with static methods instead of Injectable instance
- Agent doesn't include proper error handling

**Solution**:
```
"This implementation doesn't follow our architecture.

Required patterns from @agency-agents/.templates/flutter-patterns.md:
1. BLoC/Cubit for state management (not setState)
2. Repository with @lazySingleton and injected NetworkService
3. GlobalSnackbar for user feedback via BlocListener
4. ErrorMessages class for standardized errors

Please refactor to follow these established patterns."
```

**Prevention**:
- Reference flutter-patterns.md in every engineering request
- Use "MANDATORY" language for non-negotiable patterns
- Request agent to quote conventions before implementing

---

### Issue 5: Missing Context for Decision

**Symptom**: Agent asks questions or makes assumptions without enough context

**Cause**: Agent doesn't have access to project memory or previous decisions

**Solution**:
```
Provide comprehensive context upfront:

@memory_bank_dual/rules/memory-bank.mdc
@agency-agents/.templates/flutter-patterns.md
@agency-agents/.templates/PACKAGES_REFERENCE.md

Current architecture:
- Flutter 3.27+, Dart 3.6+
- State management: flutter_bloc with sealed classes
- Backend: Serverpod + PostgreSQL
- DI: GetIt/Injectable
- Storage: hive_ce (non-sensitive), biometric_storage (sensitive)

Now implement [your request]
```

**Prevention**:
- Always attach memory bank and pattern files
- Establish project context in first message
- Use Agents Orchestrator for complex multi-agent workflows

---

### Issue 6: Agent Selection Mistakes

**Symptom**: Wrong agent for the task

**Examples**:
- Using Backend Architect for UI design questions
- Using Evidence QA for marketing strategy
- Using Rapid Prototyper for production optimization

**Solution**:
```
Use QUICK_REFERENCE.md to select correct agent:

UI Design → @design/design-ux-architect.md
Backend APIs → @engineering/engineering-backend-architect.md  
Testing → @testing/testing-evidence-collector.md
Marketing → @marketing/marketing-social-media-strategist.md
```

**Prevention**:
- Consult [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) task-to-agent mapping
- Use [AGENT_WORKFLOWS.md](./AGENT_WORKFLOWS.md) for multi-step tasks
- Use Agents Orchestrator for complex workflows

---

### Issue 7: Convention Conflicts

**Symptom**: Agent suggests pattern that contradicts your existing code

**Example**:
- Existing code uses hive_ce, agent suggests shared_preferences
- Existing code uses getIt<T>(), agent suggests manual instantiation
- Existing code uses GlobalSnackbar, agent suggests direct SnackBar

**Solution**:
```
Point agent to existing code:

"Our existing code uses this pattern:
[paste relevant code snippet from your project]

Please follow this exact pattern for consistency."
```

**Prevention**:
- Document all conventions in memory_bank_dual
- Update flutter-patterns.md when new patterns established
- Reference existing code examples in prompts

---

## 🚨 Emergency Troubleshooting

### Agent Completely Off-Track

**When to Escalate**:
- Multiple iterations without progress
- Agent fundamentally misunderstands requirements
- Agent provides dangerous or insecure code

**Actions**:
1. **Switch Agents**: Try different agent for fresh perspective
2. **Use Orchestrator**: Let Agents Orchestrator coordinate multi-agent approach
3. **Simplify Request**: Break complex request into smaller parts
4. **Provide Examples**: Show exact code you want as template
5. **Manual Override**: Implement manually if agent approaches aren't working

### Code Quality Red Flags

**Stop and clarify if agent**:
- ❌ Hardcodes secrets or credentials
- ❌ Suggests SQL injection-vulnerable code
- ❌ Ignores error handling
- ❌ Violates security best practices
- ❌ Suggests deprecated/abandoned packages
- ❌ Creates untestable code

**Response**:
```
"STOP. This implementation has security concerns:
[List specific issues]

Please revise following security best practices:
- Never hardcode credentials
- Always validate and sanitize inputs
- Implement proper error handling
- Use maintained, secure packages"
```

---

## 📚 Resolution Resources

### Quick Fixes

| Problem | Quick Solution | Reference |
|---------|---------------|-----------|
| Agent doesn't know conventions | Attach flutter-patterns.md | [flutter-patterns.md](./.templates/flutter-patterns.md) |
| Agent suggests wrong pattern | Quote correct pattern from docs | [flutter-patterns.md](./.templates/flutter-patterns.md) |
| Code doesn't compile | Request Context7 validation | Use Context7 MCP |
| Wrong agent selected | Check agent selector | [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) |
| Complex workflow unclear | Use workflow diagrams | [AGENT_WORKFLOWS.md](./AGENT_WORKFLOWS.md) |
| Agent overwhelmed | Break into smaller tasks | [USAGE_GUIDE.md](./USAGE_GUIDE.md) |

---

**Version**: 1.0.0 | **Last Updated**: October 17, 2025 | **Common Issues**: 7 Categories

