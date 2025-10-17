# Flutter Agency Agents - Workflow Diagrams

**📊 Visual Workflow Reference | Version 1.0.0 | Updated: Oct 17, 2025**

---

## 📖 Note

**Complete workflow diagrams with mermaid visualizations are available in [AGENT_WORKFLOWS.md](./AGENT_WORKFLOWS.md)**.

This file serves as a quick reference index to all available workflow diagrams.

---

## 🗺️ Available Workflow Diagrams

### 1. MVP Development Workflow (2 Weeks)
**Diagram**: [AGENT_WORKFLOWS.md - Workflow 1](./AGENT_WORKFLOWS.md#-workflow-1-mvp-development-2-week-timeline)

**Visualization**: Mermaid flowchart showing:
- 7 agents in sequence: PM → UX → UI → Frontend/Backend (parallel) → QA → Performance → Reality Check → ASO
- 3 quality gates (Quality, Performance, Production)
- Parallel frontend/backend development phase
- Decision points for gate failures

**Use When**: Building complete MVP from scratch

---

### 2. Feature Development Workflow (1 Week)
**Diagram**: [AGENT_WORKFLOWS.md - Workflow 2](./AGENT_WORKFLOWS.md#-workflow-2-feature-development-1-week-sprint)

**Visualization**: Linear workflow with:
- 5 agents: Product Prioritizer → UX → Frontend → QA → Reality Check
- 1 quality gate
- Deploy decision point

**Use When**: Adding feature to existing app

---

### 3. Performance Optimization Workflow (2-3 Days)
**Diagram**: [AGENT_WORKFLOWS.md - Workflow 3](./AGENT_WORKFLOWS.md#-workflow-3-performance-optimization-2-3-days)

**Visualization**: Iterative workflow with:
- 4 agents with feedback loops
- Performance Benchmarker as lead and validator
- Parallel optimization paths (Frontend/Backend)
- Senior Developer escalation path

**Use When**: Fixing performance issues

---

### 4. Testing & Validation Workflow (3-5 Days)
**Diagram**: [AGENT_WORKFLOWS.md - Workflow 4](./AGENT_WORKFLOWS.md#-workflow-4-testing--validation-3-5-days)

**Visualization**: Parallel testing workflow:
- Evidence QA as coordinator
- 3 parallel specialized testers (API, Performance, Widget)
- Test Results Analyzer synthesis
- Reality Checker final gate

**Use When**: Comprehensive QA before release

---

### 5. Marketing Campaign Workflow (1-2 Weeks)
**Diagram**: [AGENT_WORKFLOWS.md - Workflow 5](./AGENT_WORKFLOWS.md#-workflow-5-marketing-campaign-1-2-weeks)

**Visualization**: Hub-and-spoke pattern:
- Social Media Strategist as hub
- Parallel content creation (Content, Visual, ASO)
- Platform distribution to 4 social agents
- Analytics Reporter convergence
- Growth Hacker optimization

**Use When**: App launch or feature promotion

---

## 🎯 Workflow Patterns

### Sequential Execution Pattern
```
Agent A → Agent B → Agent C → Agent D
```
Use when each agent needs complete output from previous agent.

### Parallel Execution Pattern
```
       ┌→ Agent B ┐
Agent A ┤         ├→ Agent D
       └→ Agent C ┘
```
Use when agents can work on independent aspects simultaneously.

### Iterative Pattern with Feedback Loops
```
Agent A → Agent B → Quality Gate
            ↑           |
            └───────────┘ (if fail)
```
Use when validation/approval may require re-work.

### Hub-and-Spoke Pattern
```
         ┌→ Agent B ┐
Agent A ─┼→ Agent C ├→ Agent F
(Hub)    └→ Agent D ┘
```
Use when one agent coordinates multiple parallel agents.

---

## 📚 Complete Workflow Documentation

For complete workflow information including:
- Detailed mermaid diagrams
- Handoff checklists
- Timeline breakdowns
- Success criteria
- Customization guides

**See**: [AGENT_WORKFLOWS.md](./AGENT_WORKFLOWS.md)

---

**Version**: 1.0.0 | **Last Updated**: October 17, 2025 | **Diagrams**: 5 Core Workflows

