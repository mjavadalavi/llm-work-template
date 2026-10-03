# Prompt Engineering Best Practices

## Core Principles (DAIR.AI Guide)

### Prompt Design
- **Start simple, iterate**: Begin with basic prompts, add complexity gradually
- **Be specific**: Descriptive, detailed prompts → better results. Avoid impreciseness
- **Say what TO DO**: "Write clean code" not "Don't write messy code"
- **Use separators**: `###` between instruction and context
- **Role prompting**: Define identity/behavior ("You are a senior QA engineer")
- **Output indicators**: Specify format ("Output as JSON", "Use this format:")

### Prompt Elements
1. **Instruction** — specific task
2. **Context** — external info to steer responses
3. **Input Data** — the question/input
4. **Output Indicator** — type/format of output

### Advanced Techniques
- **Few-shot prompting**: Provide examples for desired output format
- **Chain-of-thought (CoT)**: Break reasoning into steps for complex tasks
- **Zero-shot CoT**: Add "Let's think step by step"
- **Self-consistency**: Sample multiple reasoning paths, pick most consistent
- **Generated knowledge**: Generate context before answering

### Reliability
- **Provide ground truth**: Include related context to reduce hallucination
- **Configure determinism**: Lower temperature for factual tasks
- **Admit uncertainty**: "Say 'Unsure' if not confident"
- **Balanced exemplars**: Avoid skewed distributions in few-shot

### Applications for Agents
- **Text summarization**: Compress long outputs
- **Information extraction**: Pull specific data from text
- **Classification**: Categorize with specific labels
- **Code generation**: Provide schema + examples
- **Reasoning**: Break into steps, show work

## Spec-Kit Patterns

### Template-Driven Quality
- Templates constrain LLMs for better outcomes
- Prevent premature implementation
- Force uncertainty markers `[NEEDS CLARIFICATION]`
- Structured checklists with compliance gates

### Clarify Command Pattern
- Identify underspecified areas in spec
- Ask up to 5 targeted questions sequentially
- Use ambiguity taxonomy (scope, data model, UX, constraints, etc.)
- Integrate answers into spec under `## Clarifications`

### Initialize Pattern
- `specify init <project>` creates feature structure
- Generates branch name from description
- Creates feature directory with spec template
- Sequential numbering (001-feature-name)

## Key Takeaways for Our Framework
1. Agent prompts should be specific, not vague
2. Use role prompting in agent definitions
3. Provide output format examples
4. Break complex tasks into subtasks (chain-of-thought)
5. Say what TO DO, not what NOT to do
6. Use clear section separators
7. Provide context/ground truth to reduce hallucination
8. Clarifier should ask targeted questions, not just infer

## Sources
- Prompt-Engineering-Guide (DAIR.AI): prompts-intro.md, prompts-basic-usage.md, prompts-advanced-usage.md, prompts-applications.md, prompts-reliability.md
- spec-kit: templates/commands/clarify.md, specify.md, plan.md, tasks.md, implement.md
