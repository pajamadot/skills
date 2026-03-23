# /design-system — Guided GDD Authoring

Walk through creating a Game Design Document with all 8 required sections.

## Process

For each section, follow the collaboration protocol:
1. **Ask** clarifying questions about the design intent
2. **Present** 2-3 options with trade-offs
3. **Wait** for user decision
4. **Draft** the section
5. **Get approval** before writing to file

## Required Sections

1. **Overview** — One-paragraph game summary
2. **Player Fantasy** — The intended feeling and experience
3. **Core Mechanics** — Unambiguous rules (specific numbers, not vague)
4. **Formulas** — All math with variables (damage = base * multiplier)
5. **Edge Cases** — Unusual situations handled
6. **Dependencies** — Other systems it interacts with
7. **Tuning Knobs** — Configurable values with defaults and ranges
8. **Acceptance Criteria** — Testable success conditions

## Output

Write the GDD to `games/{game}/GDD.md` in the required format.
After completion, suggest running `/decompose-gdd` to create tasks.
