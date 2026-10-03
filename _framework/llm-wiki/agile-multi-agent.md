# Agile Multi-Agent (AgileCoder)

## What
Multi-agent framework mimicking Agile/Scrum methodology. Dynamic sprints instead of fixed roles.

## Architecture
- **ChatChain**: Top-level orchestrator. Executes phases sequentially with sprint looping.
- **ChatEnv**: Shared environment/state. Holds task_prompt, backlogs, codes, review comments, test reports.
- **Phase**: Base unit. Two-agent conversation (RolePlaying) with turn limits.
- **ComposedPhase**: Loop of SimplePhases with early-break conditions.

## Agent Roles (Agile Config)
| Role | Job |
|------|-----|
| User | Client. Specifies requirements. |
| Product Owner | Manages backlog. Aligns with customer. |
| Programmer | Writes code. |
| Code Reviewer | Reviews code. 10-point regulation check. |
| Test Engineer | Designs tests. Runs test programs. |
| Development Team | Composite: Programmer + Reviewer + Tester. |

## Workflow (Agile Chain)
```
1. DemandAnalysis (PO ↔ User)
2. LanguageChoose (PO ↔ User)
3. ProductBacklogCreating (PO ↔ User)
4. ProductBacklogUpdate (DevTeam ↔ PO, review + modify)
5. SprintCompletion (loop ≤10×):
   a. SprintBacklogCreating
   b. SprintBacklogUpdate
   c. CodeAndFormat (Coding + Formatting)
   d. CodeReview (3 cycles: comment → modify → format)
   e. Test (plan → error summary → fix, 3 cycles)
   f. SprintReview (PO ↔ DevTeam)
6. EnvironmentDoc
7. Manual
```

## Key Patterns
1. **Role-Playing**: Every phase = structured 2-agent conversation. Ends on `<INFO>` marker.
2. **Self-Reflection**: If no clear conclusion → reflection step extracts answer.
3. **Early Break**: ComposedPhases break on condition (e.g., reviewer says "Finished", no bugs found).
4. **Inherit Coding**: Sprint 2+ uses InheritCoding (extend existing) vs Coding (from scratch).
5. **Dynamic Sprint Looping**: SprintCompletion repeats until `<INFO> DONE.` from NextSprintBacklogCreating.

## Code Parsing
Multiple fallback regex strategies for extracting code from LLM output:
1. FILENAME format
2. FILENAME: format
3. Generic format
4. NormalizedLevenshtein similarity for unmatched code
5. Syntax validation with ast.parse()

## Lessons for Our Framework
- Sprint loop pattern → our build loop (per-task iteration)
- Role-playing → our subagent spawning with specific roles
- Self-reflection → our review step after implementation
- Early break → stop iterating when quality gate passes
- Shared env → our SPEC.md + llm-wiki as persistent state

## Source
- FSoft-AI4Code/AgileCoder (arXiv:2406.11912)
