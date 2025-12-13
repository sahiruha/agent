# Codex Agent Configuration

This document defines how coding agents should interact with execution plans in this repository.

## ExecPlan - Execution Planning

When you need to implement a complex feature or system change that requires careful planning and execution, use an **ExecPlan** (Execution Plan).

### When to Use ExecPlans

Use an ExecPlan when:

- The task requires significant research, design, or architecture decisions
- The implementation will take multiple steps or milestones
- You need to verify the approach before beginning implementation
- The work involves touching multiple files or systems
- The feature requires careful coordination of changes
- You need to prototype or validate feasibility before full implementation

### How to Create an ExecPlan

1. Read the entire `PLANS.md` file to understand the requirements
2. Start from the skeleton provided in `PLANS.md`
3. Research thoroughly by reading source code and documentation
4. Fill out all required sections with complete, self-contained information
5. Make the plan readable by a complete novice to the repository
6. Save the plan as a `.md` file (typically in a `plans/` directory)

### How to Execute an ExecPlan

1. Read the entire ExecPlan from top to bottom
2. Follow each step precisely as written
3. Update the `Progress` section after each step
4. Record any surprises or discoveries in the appropriate section
5. Document all design decisions in the `Decision Log`
6. Do not prompt for "next steps" - proceed autonomously
7. Commit frequently and keep the plan synchronized with actual progress
8. At completion, write an `Outcomes & Retrospective` entry

### Important Principles

- **Self-contained**: Every ExecPlan must contain all information needed for implementation
- **Living document**: Keep the plan updated as you work
- **Novice-friendly**: Write for someone with no prior context
- **Observable outcomes**: Focus on behavior that can be verified, not just code changes
- **Comprehensive**: Include all context, decisions, and discoveries

## Directory Structure

When working with ExecPlans, consider organizing them as follows:

```
repository-root/
├── AGENTS.md          # This file
├── PLANS.md           # ExecPlan template and requirements
└── plans/             # Directory for individual execution plans
    ├── feature-x.md
    └── migration-y.md
```

## Additional Agent Guidance

When authoring code:
- Commit frequently with clear messages
- Run tests after each meaningful change
- Keep the working tree clean
- Document non-obvious decisions in code comments
- Refer to ExecPlans in commit messages when working from one
