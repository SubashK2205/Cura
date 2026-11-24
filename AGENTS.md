# Antigravity Project Instructions - India Health Link HMIS

This workspace hosts the **India Health Link – Hospital Management Information System (HMIS)** monorepository.

When working in this repository:
1. Always adhere to the 14 architecture and engineering rules defined in [.agent/rules/hmis-development.md](.agent/rules/hmis-development.md).
2. Follow the 7-stage development lifecycle defined in [.agent/workflows/feature-development.md](.agent/workflows/feature-development.md):
   **Inspect → Plan → Review → Implement → Test → Verify → Document**.
3. Strictly preserve multi-tenant isolation: every backend data query must resolve the tenant authoritatively from session context, never client input.
4. Keep TypeScript strict mode enabled without `any`.
5. Run typecheck, lint, and tests before completing tasks.

