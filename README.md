# 🎭 The Flutter Agency: 51 Flutter-Specialized AI Agents

> **A complete Flutter development agency at your fingertips** - From Flutter UI developers to Serverpod backend architects, from Flutter QA specialists to app store optimizers. Each agent is a Flutter-specialized expert with deep knowledge of BLoC patterns, Mason bricks, and cross-platform development.

[![GitHub stars](https://img.shields.io/github/stars/msitarzewski/agency-agents?style=social)](https://github.com/msitarzewski/agency-agents)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

---

## 🚀 What Is This?

**The Flutter Agency** is a collection of 51 meticulously crafted Flutter-specialized AI agent personalities. Each agent is:

- **🎯 Flutter-Specialized**: Deep expertise in Flutter/Dart, BLoC patterns, Mason bricks, and cross-platform development
- **🧠 Personality-Driven**: Unique voice, communication style, and Flutter-focused approach
- **📋 Deliverable-Focused**: Real Flutter/Dart code, BLoC patterns, Mason brick workflows, and measurable outcomes
- **✅ Production-Ready**: Battle-tested Flutter development workflows and success metrics

**Think of it as**: Assembling your dream Flutter development team, except they're AI specialists who master BLoC, know every pub.dev package, and deliver production-ready Flutter apps.

---

## ⚡ Quick Start

### Step 1: Choose Your Agent

Use the **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)** one-page agent selector to find the right agent for your task.

### Step 2: Learn Agent Usage

Read **[USAGE_GUIDE.md](./USAGE_GUIDE.md)** for:
- How to work with agents in Cursor IDE
- 10+ real-world usage scenarios
- Best practices for effective prompts
- Troubleshooting common issues

### Step 3: Use Pre-Defined Workflows

Check **[AGENT_WORKFLOWS.md](./AGENT_WORKFLOWS.md)** for:
- MVP Development (2 weeks, 7 agents)
- Feature Development (1 week, 5 agents)
- Performance Optimization (2-3 days, 4 agents)
- Testing & Validation (3-5 days, 6 agents)
- Marketing Campaign (1-2 weeks, 5-8 agents)

### Step 4: Reference Patterns & Conventions

Use **[.templates/flutter-patterns.md](./.templates/flutter-patterns.md)** for:
- BLoC pattern with sealed classes
- Repository pattern with injected NetworkService
- GetIt/Injectable dependency injection
- GlobalSnackbar user notifications
- ErrorMessages standardization
- Storage patterns (hive_ce, biometric_storage)

---

## 📚 Complete Documentation

### Essential Guides
- **[USAGE_GUIDE.md](./USAGE_GUIDE.md)** - How to use agents effectively (10+ scenarios)
- **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)** - One-page agent selector cheat sheet
- **[TESTING_VALIDATION_GUIDE.md](./TESTING_VALIDATION_GUIDE.md)** - Quality assurance procedures
- **[TROUBLESHOOTING.md](./TROUBLESHOOTING.md)** - Common issues and solutions

### Workflow & Teams
- **[AGENT_WORKFLOWS.md](./AGENT_WORKFLOWS.md)** - 5 mermaid workflow diagrams
- **[AGENT_COMBINATIONS.md](./AGENT_COMBINATIONS.md)** - Pre-defined agent teams (MVP Squad, Feature Factory, etc.)
- **[SUCCESS_STORIES.md](./SUCCESS_STORIES.md)** - Real-world usage examples

### Technical References
- **[.templates/flutter-patterns.md](./.templates/flutter-patterns.md)** - Complete Flutter pattern library
- **[.templates/PACKAGES_REFERENCE.md](./.templates/PACKAGES_REFERENCE.md)** - All packages with migration guides
- **[.templates/VERSION_LOCK_STRATEGY.md](./.templates/VERSION_LOCK_STRATEGY.md)** - Version management
- **[.templates/PERFORMANCE_BASELINES.md](./.templates/PERFORMANCE_BASELINES.md)** - Performance standards
- **[.templates/ERROR_HANDLING_GUIDE.md](./.templates/ERROR_HANDLING_GUIDE.md)** - Error handling patterns

### Operations
- **[MASON_BRICK_RESPONSIBILITIES.md](./MASON_BRICK_RESPONSIBILITIES.md)** - Brick ownership and maintenance
- **[INDEX.md](./INDEX.md)** - Complete documentation map

---

## 🧱 Mason Brick Integration

All engineering and PM agents integrate with Mason bricks for rapid development:

### Available Bricks

1. **flutter_init** - Complete Flutter + Serverpod project
   - Full-stack setup with backend
   - Firebase Analytics + Crashlytics
   - BLoC pattern pre-configured
   - **Usage**: `mason make flutter_init --projectName my_app`

2. **flutter_init_no_backend** - Flutter-only project
   - Frontend architecture without Serverpod
   - Local auth simulation
   - **Usage**: `mason make flutter_init_no_backend --projectName my_app`

3. **new_screen** - Screen + Cubit + AutoRoute
   - Generates screen file
   - Creates cubit with sealed states
   - Updates AutoRoute navigation
   - **Usage**: `mason make new_screen --screenName product_detail`

4. **new_cubit** - BLoC cubit with sealed states
   - Sealed state classes
   - Equatable integration
   - **Usage**: `mason make new_cubit --cubitName user_profile`

### Brick Usage by Agent

- **Frontend Developer**: Uses `new_screen`, `new_cubit` for rapid feature development
- **Mobile App Builder**: Uses `flutter_init_no_backend` for cross-platform projects
- **Rapid Prototyper**: PRIMARY user of `flutter_init` for 2-week MVPs
- **Backend Architect**: Serverpod structure from `flutter_init` provides foundation
- **Senior PM**: References brick workflows for realistic timeline estimation

### Generated Code Examples

**After `mason make new_screen --screenName login`**:
```
lib/
├── screens/
│   └── login_screen.dart           # Screen with BlocProvider
├── cubits/
│   └── app_cubits/
│       └── login_cubit/
│           ├── cubit.dart          # Cubit with business logic
│           └── state.dart          # Sealed state classes
└── routes/
    └── app_router.dart             # Updated with LoginRoute
```

**Post-Generation Workflow**:
1. Run `dart run build_runner build` (generates routes, DI)
2. Implement repository for data layer
3. Add API integration
4. Customize UI with shadcn_flutter components
5. Test with `flutter test`

### Brick Maintenance

See **[MASON_BRICK_RESPONSIBILITIES.md](./MASON_BRICK_RESPONSIBILITIES.md)** for:
- Brick ownership matrix
- Maintenance workflows
- Quality standards
- Update procedures

---

## 🎯 FAQ

### Q: Which agent should I use for building a new Flutter screen?

**A**: Use **Flutter Frontend Developer** (`engineering-frontend-developer.md`). This agent specializes in:
- Building screens with BLoC pattern and sealed states
- Integrating shadcn_flutter components
- AutoRoute navigation setup
- GlobalSnackbar user feedback
- Repository pattern with injected NetworkService

### Q: How do I coordinate multiple agents for a complex project?

**A**: Use **Agents Orchestrator** (`specialized/agents-orchestrator.md`) or follow pre-defined workflows in **[AGENT_WORKFLOWS.md](./AGENT_WORKFLOWS.md)**. For example, MVP development uses 7 agents in sequence.

### Q: What if an agent provides incorrect or outdated guidance?

**A**: Reference **[TROUBLESHOOTING.md](./TROUBLESHOOTING.md)** for common issues. Always provide agents with:
- `@agency-agents/.templates/flutter-patterns.md` for conventions
- `@memory_bank_dual/rules/memory-bank.mdc` for project context
- Specific Flutter version and package versions

### Q: How do I ensure agent-generated code follows my project conventions?

**A**: Always reference **[.templates/flutter-patterns.md](./.templates/flutter-patterns.md)** in your prompts. This contains all standardized patterns:
- BLoC with sealed classes
- Repository with @lazySingleton and injected NetworkService
- GetIt/Injectable DI
- GlobalSnackbar + ErrorMessages
- Storage patterns (hive_ce, biometric_storage)

### Q: Can I modify agents for my team's specific needs?

**A**: Yes! All agents are open-source (MIT License). Fork the repository and customize agent personalities, workflows, and technical patterns for your team. See **[CONTRIBUTING.md](./CONTRIBUTING.md)** for guidelines.

### Q: How do Mason bricks integrate with agents?

**A**: Engineering agents reference Mason bricks for rapid code generation. See **[MASON_BRICK_RESPONSIBILITIES.md](./MASON_BRICK_RESPONSIBILITIES.md)** for complete brick usage, maintenance, and agent ownership.

---

## Option 1: Use with Cursor IDE (Recommended)

```bash
# Reference agents using @ mention in Cursor:
@agency-agents/engineering/engineering-frontend-developer.md
@agency-agents/.templates/flutter-patterns.md

# Provide context:
@memory_bank_dual/rules/memory-bank.mdc

# Make your request:
"Create a product list screen following our BLoC patterns..."
```

### Option 2: Use as Reference

Each agent file contains:
- Identity & personality traits
- Core mission & workflows
- Technical deliverables with Flutter/Dart code examples
- Success metrics & communication style

Browse the agents below and copy/adapt the ones you need!

---

## 🎨 The Agency Roster

### 💻 Engineering Division (7 Agents)

Building Flutter apps across all platforms, one widget at a time.

| Agent | Specialty | When to Use |
|-------|-----------|-------------|
| 🎨 [Flutter UI Developer](engineering/engineering-frontend-developer.md) | Flutter widgets, BLoC state management, Material Design 3 | Cross-platform Flutter apps, pixel-perfect UIs, 60fps performance |
| 🏗️ [Serverpod Backend Architect](engineering/engineering-backend-architect.md) | Serverpod protocols, PostgreSQL, real-time streaming | Type-safe Dart backends, Flutter-server integration, WebSocket streaming |
| 📱 [Flutter App Builder](engineering/engineering-mobile-app-builder.md) | iOS/Android/Web/Desktop Flutter, platform channels | Cross-platform Flutter apps with platform-specific features |
| 🤖 [Flutter AI Engineer](engineering/engineering-ai-engineer.md) | Firebase ML Kit, TensorFlow Lite, on-device AI | ML features in Flutter apps, image recognition, AI chatbots |
| 🚀 [Flutter DevOps Engineer](engineering/engineering-devops-automator.md) | Flutter CI/CD, app store deployment, Codemagic | Automated Flutter builds, App Store/Play Store deployments |
| ⚡ [Flutter Rapid Prototyper](engineering/engineering-rapid-prototyper.md) | Mason bricks, Firebase BaaS, rapid MVPs | Quick Flutter prototypes, 2-3 day MVPs, idea validation |
| 💎 [Flutter Senior Developer](engineering/engineering-senior-developer.md) | Advanced widgets, custom animations, Shadcn Flutter | Premium Flutter implementations, complex animations, polished UX |

### 🎨 Design Division (6 Agents)

Making it beautiful, usable, and delightful.

| Agent | Specialty | When to Use |
|-------|-----------|-------------|
| 🎯 [UI Designer](design/design-ui-designer.md) | Visual design, component libraries, design systems | Interface creation, brand consistency, component design |
| 🔍 [UX Researcher](design/design-ux-researcher.md) | User testing, behavior analysis, research | Understanding users, usability testing, design insights |
| 🏛️ [UX Architect](design/design-ux-architect.md) | Technical architecture, CSS systems, implementation | Developer-friendly foundations, implementation guidance |
| 🎭 [Brand Guardian](design/design-brand-guardian.md) | Brand identity, consistency, positioning | Brand strategy, identity development, guidelines |
| 📖 [Visual Storyteller](design/design-visual-storyteller.md) | Visual narratives, multimedia content | Compelling visual stories, brand storytelling |
| ✨ [Whimsy Injector](design/design-whimsy-injector.md) | Personality, delight, playful interactions | Adding joy, micro-interactions, Easter eggs, brand personality |

### 📢 Marketing Division (8 Agents)

Growing your audience, one authentic interaction at a time.

| Agent | Specialty | When to Use |
|-------|-----------|-------------|
| 🚀 [Growth Hacker](marketing/marketing-growth-hacker.md) | Rapid user acquisition, viral loops, experiments | Explosive growth, user acquisition, conversion optimization |
| 📝 [Content Creator](marketing/marketing-content-creator.md) | Multi-platform content, editorial calendars | Content strategy, copywriting, brand storytelling |
| 🐦 [Twitter Engager](marketing/marketing-twitter-engager.md) | Real-time engagement, thought leadership | Twitter strategy, LinkedIn campaigns, professional social |
| 📱 [TikTok Strategist](marketing/marketing-tiktok-strategist.md) | Viral content, algorithm optimization | TikTok growth, viral content, Gen Z/Millennial audience |
| 📸 [Instagram Curator](marketing/marketing-instagram-curator.md) | Visual storytelling, community building | Instagram strategy, aesthetic development, visual content |
| 🤝 [Reddit Community Builder](marketing/marketing-reddit-community-builder.md) | Authentic engagement, value-driven content | Reddit strategy, community trust, authentic marketing |
| 📱 [App Store Optimizer](marketing/marketing-app-store-optimizer.md) | ASO, conversion optimization, discoverability | App marketing, store optimization, app growth |
| 🌐 [Social Media Strategist](marketing/marketing-social-media-strategist.md) | Cross-platform strategy, campaigns | Overall social strategy, multi-platform campaigns |

### 📊 Product Division (3 Agents)

Building the right thing at the right time.

| Agent | Specialty | When to Use |
|-------|-----------|-------------|
| 🎯 [Sprint Prioritizer](product/product-sprint-prioritizer.md) | Agile planning, feature prioritization | Sprint planning, resource allocation, backlog management |
| 🔍 [Trend Researcher](product/product-trend-researcher.md) | Market intelligence, competitive analysis | Market research, opportunity assessment, trend identification |
| 💬 [Feedback Synthesizer](product/product-feedback-synthesizer.md) | User feedback analysis, insights extraction | Feedback analysis, user insights, product priorities |

### 🎬 Project Management Division (5 Agents)

Keeping the trains running on time (and under budget).

| Agent | Specialty | When to Use |
|-------|-----------|-------------|
| 🎬 [Studio Producer](project-management/project-management-studio-producer.md) | High-level orchestration, portfolio management | Multi-project oversight, strategic alignment, resource allocation |
| 🐑 [Project Shepherd](project-management/project-management-project-shepherd.md) | Cross-functional coordination, timeline management | End-to-end project coordination, stakeholder management |
| ⚙️ [Studio Operations](project-management/project-management-studio-operations.md) | Day-to-day efficiency, process optimization | Operational excellence, team support, productivity |
| 🧪 [Experiment Tracker](project-management/project-management-experiment-tracker.md) | A/B tests, hypothesis validation | Experiment management, data-driven decisions, testing |
| 👔 [Senior Project Manager](project-management/project-manager-senior.md) | Realistic scoping, task conversion | Converting specs to tasks, scope management |

### 🧪 Testing Division (7 Agents)

Breaking things so users don't have to.

| Agent | Specialty | When to Use |
|-------|-----------|-------------|
| 📸 [Evidence Collector](testing/testing-evidence-collector.md) | Screenshot-based QA, visual proof | UI testing, visual verification, bug documentation |
| 🔍 [Reality Checker](testing/testing-reality-checker.md) | Evidence-based certification, quality gates | Production readiness, quality approval, release certification |
| 📊 [Test Results Analyzer](testing/testing-test-results-analyzer.md) | Test evaluation, metrics analysis | Test output analysis, quality insights, coverage reporting |
| ⚡ [Performance Benchmarker](testing/testing-performance-benchmarker.md) | Performance testing, optimization | Speed testing, load testing, performance tuning |
| 🔌 [API Tester](testing/testing-api-tester.md) | API validation, integration testing | API testing, endpoint verification, integration QA |
| 🛠️ [Tool Evaluator](testing/testing-tool-evaluator.md) | Technology assessment, tool selection | Evaluating tools, software recommendations, tech decisions |
| 🔄 [Workflow Optimizer](testing/testing-workflow-optimizer.md) | Process analysis, workflow improvement | Process optimization, efficiency gains, automation opportunities |

### 🛟 Support Division (6 Agents)

The backbone of the operation.

| Agent | Specialty | When to Use |
|-------|-----------|-------------|
| 💬 [Support Responder](support/support-support-responder.md) | Customer service, issue resolution | Customer support, user experience, support operations |
| 📊 [Analytics Reporter](support/support-analytics-reporter.md) | Data analysis, dashboards, insights | Business intelligence, KPI tracking, data visualization |
| 💰 [Finance Tracker](support/support-finance-tracker.md) | Financial planning, budget management | Financial analysis, cash flow, business performance |
| 🏗️ [Infrastructure Maintainer](support/support-infrastructure-maintainer.md) | System reliability, performance optimization | Infrastructure management, system operations, monitoring |
| ⚖️ [Legal Compliance Checker](support/support-legal-compliance-checker.md) | Compliance, regulations, legal review | Legal compliance, regulatory requirements, risk management |
| 📑 [Executive Summary Generator](support/support-executive-summary-generator.md) | C-suite communication, strategic summaries | Executive reporting, strategic communication, decision support |

### 🥽 Spatial Computing Division (6 Agents)

Building the immersive future.

| Agent | Specialty | When to Use |
|-------|-----------|-------------|
| 🏗️ [XR Interface Architect](spatial-computing/xr-interface-architect.md) | Spatial interaction design, immersive UX | AR/VR/XR interface design, spatial computing UX |
| 💻 [macOS Spatial/Metal Engineer](spatial-computing/macos-spatial-metal-engineer.md) | Swift, Metal, high-performance 3D | macOS spatial computing, Vision Pro native apps |
| 🌐 [XR Immersive Developer](spatial-computing/xr-immersive-developer.md) | WebXR, browser-based AR/VR | Browser-based immersive experiences, WebXR apps |
| 🎮 [XR Cockpit Interaction Specialist](spatial-computing/xr-cockpit-interaction-specialist.md) | Cockpit-based controls, immersive systems | Cockpit control systems, immersive control interfaces |
| 🍎 [visionOS Spatial Engineer](spatial-computing/visionos-spatial-engineer.md) | Apple Vision Pro development | Vision Pro apps, spatial computing experiences |
| 🔌 [Terminal Integration Specialist](spatial-computing/terminal-integration-specialist.md) | Terminal integration, command-line tools | CLI tools, terminal workflows, developer tools |

### 🎯 Specialized Division (3 Agents)

The unique specialists who don't fit in a box.

| Agent | Specialty | When to Use |
|-------|-----------|-------------|
| 🎭 [Agents Orchestrator](specialized/agents-orchestrator.md) | Multi-agent coordination, workflow management | Complex projects requiring multiple agent coordination |
| 📊 [Data Analytics Reporter](specialized/data-analytics-reporter.md) | Business intelligence, data insights | Deep data analysis, business metrics, strategic insights |
| 🔍 [LSP/Index Engineer](specialized/lsp-index-engineer.md) | Language Server Protocol, code intelligence | Code intelligence systems, LSP implementation, semantic indexing |

---

## 🎯 Real-World Use Cases

### Scenario 1: Building a Flutter Startup MVP

**Your Team**:
1. ⚡ **Flutter Rapid Prototyper** - Initialize with `mason make flutter_init_no_backend`
2. 🎨 **Flutter UI Developer** - Build screens with BLoC and Shadcn Flutter
3. 🏗️ **Serverpod Backend Architect** - Set up type-safe Dart backend
4. 🚀 **Flutter Growth Hacker** - Plan app store optimization and user acquisition
5. 🔍 **Flutter Reality Checker** - Ensure quality with device testing before launch

**Result**: Ship cross-platform Flutter MVP in days with Mason brick acceleration and production-ready architecture.

---

### Scenario 2: Marketing Campaign Launch

**Your Team**:
1. 📝 **Content Creator** - Develop campaign content
2. 🐦 **Twitter Engager** - Twitter strategy and execution
3. 📸 **Instagram Curator** - Visual content and stories
4. 🤝 **Reddit Community Builder** - Authentic community engagement
5. 📊 **Analytics Reporter** - Track and optimize performance

**Result**: Multi-channel coordinated campaign with platform-specific expertise.

---

### Scenario 3: Enterprise Feature Development

**Your Team**:
1. 👔 **Senior Project Manager** - Scope and task planning
2. 💎 **Senior Developer** - Complex implementation
3. 🎨 **UI Designer** - Design system and components
4. 🧪 **Experiment Tracker** - A/B test planning
5. 📸 **Evidence Collector** - Quality verification
6. 🔍 **Reality Checker** - Production readiness

**Result**: Enterprise-grade delivery with quality gates and documentation.

---

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### Add a New Agent

1. Fork the repository
2. Create a new agent file in the appropriate category
3. Follow the agent template structure:
   - Frontmatter with name, description, color
   - Identity & Memory section
   - Core Mission
   - Critical Rules (domain-specific)
   - Technical Deliverables with examples
   - Workflow Process
   - Success Metrics
4. Submit a PR with your agent

### Improve Existing Agents

- Add real-world examples
- Enhance code samples
- Update success metrics
- Improve workflows

### Share Your Success Stories

Have you used these agents successfully? Share your story in the [Discussions](https://github.com/msitarzewski/agency-agents/discussions)!

---

## 📖 Agent Design Philosophy

Each agent is designed with:

1. **🎭 Strong Personality**: Not generic templates - real character and voice
2. **📋 Clear Deliverables**: Concrete outputs, not vague guidance
3. **✅ Success Metrics**: Measurable outcomes and quality standards
4. **🔄 Proven Workflows**: Step-by-step processes that work
5. **💡 Learning Memory**: Pattern recognition and continuous improvement

---

## 🎁 What Makes This Special?

### Unlike Generic AI Prompts:
- ❌ Generic "Act as a developer" prompts
- ✅ Deep specialization with personality and process

### Unlike Prompt Libraries:
- ❌ One-off prompt collections
- ✅ Comprehensive agent systems with workflows and deliverables

### Unlike AI Tools:
- ❌ Black box tools you can't customize
- ✅ Transparent, forkable, adaptable agent personalities

---

## 🎨 Agent Personality Highlights

> "I don't just test your code - I default to finding 3-5 issues and require visual proof for everything."
>
> — **Evidence Collector** (Testing Division)

> "You're not marketing on Reddit - you're becoming a valued community member who happens to represent a brand."
>
> — **Reddit Community Builder** (Marketing Division)

> "Every playful element must serve a functional or emotional purpose. Design delight that enhances rather than distracts."
>
> — **Whimsy Injector** (Design Division)

> "Let me add a celebration animation that reduces task completion anxiety by 40%"
>
> — **Whimsy Injector** (during a UX review)

---

## 📊 Stats

- 🎭 **51 Flutter-Specialized Agents** across 9 divisions
- 📝 **15,000+ lines** of Flutter/Dart code examples, BLoC patterns, and Mason brick workflows
- ⏱️ **Transformed for Flutter excellence** with sealed class patterns and clean architecture
- 🌟 **Production-ready** Flutter development patterns and best practices
- 🧱 **Mason Brick Integration** across all engineering and PM agents for rapid development
- 🎯 **Covers all platforms**: iOS, Android, Web, Desktop (Windows, macOS, Linux)

---

## 🗺️ Roadmap

- [ ] Interactive agent selector web tool
- [ ] Multi-agent workflow examples
- [ ] Video tutorials on agent design
- [ ] Community agent marketplace
- [ ] Agent "personality quiz" for project matching
- [ ] Integration examples with popular tools
- [ ] "Agent of the Week" showcase series

---

## 📜 License

MIT License - Use freely, commercially or personally. Attribution appreciated but not required.

---

## 🙏 Acknowledgments

Born from a Reddit discussion about AI agent specialization. Thanks to the community for the feedback, requests, and inspiration.

Special recognition to the 50+ Redditors who requested this within the first 12 hours - you proved there's demand for real, specialized AI agent systems.

---

## 💬 Community

- **GitHub Discussions**: [Share your success stories](https://github.com/msitarzewski/agency-agents/discussions)
- **Issues**: [Report bugs or request features](https://github.com/msitarzewski/agency-agents/issues)
- **Reddit**: Join the conversation on r/ClaudeAI
- **Twitter/X**: Share with #TheAgency

---

## 🚀 Get Started

1. **Browse** the agents above and find specialists for your needs
2. **Copy** the agents to `~/.claude/agents/` for Claude Code integration
3. **Activate** agents by referencing them in your Claude conversations
4. **Customize** agent personalities and workflows for your specific needs
5. **Share** your results and contribute back to the community

---

<div align="center">

**🎭 The Agency: Your AI Dream Team Awaits 🎭**

[⭐ Star this repo](https://github.com/msitarzewski/agency-agents) • [🍴 Fork it](https://github.com/msitarzewski/agency-agents/fork) • [🐛 Report an issue](https://github.com/msitarzewski/agency-agents/issues)

Made with ❤️ by the community, for the community

</div>
