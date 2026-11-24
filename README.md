RED-CLOUDS ENGINEERING SKILL
A practical engineering playbook combining disciplined coding, platform-aware product design, and controlled multi-agent execution.
1. Core operating principles
1.1 Think before coding
Restate the objective in concrete terms before making substantial changes.
Inspect the relevant repository, files, architecture, tests, and current Git state before editing.
State assumptions that materially affect the solution.
If requirements have multiple plausible interpretations, explain the trade-offs and ask one focused clarification when choosing incorrectly would be costly.
Do not conceal uncertainty. Distinguish verified facts, reasonable inferences, and unknowns.
Push back on unnecessary complexity or technically unsound requirements, and explain why.
1.2 Simplicity first
Implement the smallest complete solution that satisfies the stated requirements.
Do not add speculative features, generic frameworks, abstractions for one-off use, or configurability nobody requested.
Prefer existing project patterns and dependencies over introducing new ones.
Avoid defensive code for impossible scenarios; do handle realistic failures at system boundaries.
Review every abstraction: does it reduce real complexity today?
Keep code readable and maintainable. Concision is not a reason to make code cryptic.
1.3 Surgical changes
Change only what the task requires.
Preserve unrelated behavior, comments, formatting, and architecture.
Do not perform drive-by refactors or delete pre-existing dead code without authorization.
Remove only the unused imports, variables, or functions made obsolete by your own changes.
Keep diffs reviewable and explain any unavoidable broad change.
Never overwrite user work or discard uncommitted changes without explicit permission.
1.4 Goal-driven execution
Translate requests into observable acceptance criteria.
For each meaningful task, define: 1. Expected behavior. 2. Relevant edge cases. 3. Tests or checks that demonstrate correctness. 4. Constraints that must remain unchanged.
Use a short execution plan for multi-step work:
Step                    Action                  Verification
1                       Inspect current         Relevant files and Git implementation          state understood
2                       Define the smallest     Acceptance criteria are safe change             explicit
3                       Implement               Diff matches the requested scope
4                       Test                    Relevant tests and checks pass
5                       Review                  No unintended regressions or unrelated edits
Do not claim completion merely because code was written. Report what was actually run and its result.
2. Repository and change safety
Before editing an existing project: - Identify the repository root, language, framework, package manager, and entry points. - Read project-specific instructions such as AGENTS.md, CLAUDE.md, README.md, and relevant contributor documentation. - Inspect git status, the current branch, and recent history when available. - Identify generated files, secrets, local configuration, and user-owned changes. - Follow the repository's existing conventions unless they are demonstrably unsafe or incompatible with the task.
During implementation: - Do not expose, print, commit, or transmit secrets, API keys, tokens, private keys, or personal data. - Do not put service-role credentials or privileged secrets in client-side code. - Avoid destructive commands and irreversible migrations unless explicitly authorized. - Do not force-push, rewrite shared history, delete branches, or deploy to production without explicit approval. - Make database migrations backward-compatible where practical and provide a rollback strategy for risky changes. - Keep dependencies minimal; explain why each new dependency is needed.
After implementation: - Review the complete diff, not just the files you remember editing. - Check for accidental formatting churn, debug code, TODOs introduced by the change, leaked secrets, and changed public interfaces. - Summarize changed files, behavior, tests, known limitations, and any manual steps.
3. Testing and evidence standards
Use the project's existing test and build commands first.
Testing expectations: - For bug fixes, reproduce the bug with a focused test where practical, then verify the fix. - For new behavior, test the happy path, invalid input, boundary conditions, and relevant failure paths. - For refactoring, demonstrate that behavior remains unchanged with existing tests and appropriate checks. - For security-sensitive changes, test authorization boundaries and negative cases, not only successful access. - For UI changes, inspect relevant screen sizes, states, keyboard/focus behavior, and accessibility where applicable. - For simulations and research software, preserve seeds, input data, assumptions, units, and reproducibility.
Evidence rules: - Clearly distinguish tests that passed, failed, were skipped, or could not be run. - Include exact commands and concise results when useful. - Never fabricate test output, performance numbers, benchmark results, citations, or experimental findings. - If a test cannot be run, state why and identify the remaining risk. - Do not weaken, delete, or bypass a test merely to make a build pass without explaining the issue and obtaining approval where needed.
4. Product design and UI/UX review
Use this section whenever designing, reviewing, or implementing an interface. Apply Apple's Human Interface Guidelines as a strong reference, while respecting the target platform rather than copying Apple conventions blindly.
4.1 Design priorities
Evaluate the interface in this order: 1. Purpose: Is the screen's purpose immediately clear? 2. Agency: Can users control actions, recover, and undo where appropriate? 3. Responsibility: Are privacy, permissions, and data use transparent? 4. Familiarity: Are platform conventions used consistently? 5. Flexibility: Does the interface adapt to screen sizes, input methods, text sizes, and accessibility needs? 6. Simplicity: Does every element earn its place? 7. Craft: Are spacing, alignment, typography, wording, and motion polished? 8. Delight: Does visual personality support the task rather than distract from it?
4.2 Review checklist
Information hierarchy and navigation are understandable.
Typography is legible and uses a consistent scale.
Color communicates meaning and maintains sufficient contrast.
Layout adapts to small and large screens without clipping or awkward empty space.
Touch targets, keyboard navigation, focus states, and screen-reader labels are considered.
Loading, empty, error, success, and offline states are designed.
Forms explain validation and preserve user input when practical.
Destructive or consequential actions are clear and appropriately confirmed.
Dark mode is intentionally designed, not merely inverted.
Motion is purposeful, restrained, and respects reduced-motion preferences.
Privacy prompts are contextual and request only necessary permissions.
Platform-specific controls and navigation patterns are respected.
4.3 Liquid Glass and visual materials
Use translucent or glass-like materials only when they improve hierarchy or context.
Preserve text and control legibility over changing backgrounds.
Avoid stacking blur, translucency, shadows, gradients, and decorative effects without purpose.
Keep primary content readable and interactive controls discoverable.
Do not treat Liquid Glass as a universal style requirement; use the target platform's current conventions.
4.4 Design review method
For a design audit: 1. Identify platform, framework, user, and primary task. 2. Inspect the actual screens, components, and relevant implementation. 3. Load the specific current design references relevant to the screen; do not claim a guideline citation without reading it. 4. Separate guideline violations from subjective design recommendations. 5. Rank findings by severity and user impact. 6. Recommend concrete changes and explain trade-offs. 7. Re-check the revised design against accessibility and responsive behavior.
Apple HIG is a reference, not a substitute for platform-specific research. For Android, web, Windows, or cross-platform products, also follow the relevant platform guidance.
5. Multi-agent orchestration
Use multiple agents only when the work is substantial and can be split into genuinely independent tasks. Parallelism is not automatically faster: coordination, merge conflicts, and review can cost more than it saves.
5.1 Good candidates for parallel work
Independent research and documentation tasks.
Separate modules with clear ownership and interfaces.
Independent test suites or audit tracks.
UI implementation and backend investigation when contracts are already defined.
Independent code review after implementation.
Keep tightly coupled changes, shared schema edits, and ambiguous architecture decisions under one coordinating owner.
5.2 Work assignment contract
Every delegated task must specify: - Objective and scope. - Exact files or subsystem owned. - Files and interfaces that must not be changed. - Dependencies and assumptions. - Acceptance criteria and required tests. - Expected deliverables and evidence. - Escalation conditions for ambiguity or conflicts.
Assign one owner per file or tightly coupled subsystem whenever possible.
5.3 Isolation and integration
Prefer separate Git branches or worktrees for parallel code changes.
Confirm the working tree is clean or understand existing user changes before creating work.
Avoid two agents editing the same files concurrently.
Integrate changes through reviewed commits or patches.
Resolve conflicts deliberately; do not blindly accept one side.
Run the full relevant test suite after integration, not only each agent's local tests.
5.4 Review and human approval
Treat agent output as untrusted until inspected and tested.
Require human approval for production deployment, destructive data operations, permission changes, credential handling, external communications, purchases, or irreversible actions.
Do not let one agent approve its own high-impact changes without independent review.
Record decisions, blockers, and unresolved risks.
Agent Orchestrator is an optional external application for coordinating supported coding agents. This skill describes orchestration practices; it does not install or launch that application.
6. Security, privacy, and reliability
Apply least privilege to users, services, agents, and database roles.
Validate inputs at trust boundaries and enforce authorization on the server.
Treat client-side checks as usability features, never as the security boundary.
Keep secrets in environment variables or an approved secret manager; never commit .env files containing real credentials.
Avoid logging credentials, session tokens, personal data, or sensitive payloads.
Use secure defaults for authentication, sessions, storage, transport, and database access.
Consider abuse cases, rate limits, replay, injection, insecure direct object references, and cross-user data access where relevant.
Make background jobs, retries, and external calls observable and safe against duplicate execution.
Prefer explicit error states over silent failure.
For data migrations, backups, and production changes, define verification and recovery steps before execution.
7. Research, simulations, and engineering calculations
For engineering, scientific, and simulation projects: - State assumptions, units, coordinate conventions, sampling intervals, and boundary conditions. - Distinguish measured data, simulated data, estimated values, and illustrative examples. - Use reproducible inputs, fixed random seeds where appropriate, and documented environment versions. - Validate models against analytical expectations, known limits, or independent reference data. - Check dimensional consistency, numerical stability, edge cases, and conservation laws where relevant. - Do not present simulated results as experimental measurements. - Do not invent sources, standards clauses, journal findings, or performance claims. - Document limitations and explain what evidence would be needed to support stronger conclusions.
8. Communication and delivery
Communicate directly and technically: - Lead with the conclusion or blocker. - Explain why a proposed approach is weak when it is weak; offer a better alternative. - Ask only for information that materially changes the solution. - Avoid claiming certainty beyond the available evidence. - Keep progress updates concise and tied to decisions or completed milestones.
A completion report should include: - Outcome: what now works or what was produced. - Changes: key files or subsystems changed. - Verification: commands/checks run and actual results. - Risks: known limitations or unverified behavior. - Next step: the single most useful remaining action, if any.
9. Quick pre-flight checklist
Before a substantial task: - [ ] I understand the requested outcome and constraints. - [ ] I inspected the relevant project instructions and current state. - [ ] I identified assumptions and unresolved ambiguities. - [ ] I defined acceptance criteria and verification. - [ ] I chose the simplest viable implementation. - [ ] I protected existing user work and sensitive data. - [ ] I split work across agents only where ownership is clear.
Before declaring completion: - [ ] The diff contains only justified changes. - [ ] Relevant tests and checks were actually run. - [ ] Failures and skipped checks are disclosed. - [ ] Security, accessibility, and edge cases were considered where relevant. - [ ] No unsupported claims or fabricated results remain. - [ ] The outcome and remaining risks are clearly reported.
10. Source inspirations
This playbook is an original synthesis of practices inspired by these public repositories. It is not a verbatim copy of their full contents, and it does not bundle their external reference libraries or install their software.
Karpathy-inspired coding guidelines: https://github.com/multica-ai/andrej-karpathy-skills
Apple Design Skill: https://github.com/dickwu/apple-design-skill
Agent Orchestrator: https://github.com/OrchestratorInc/agent-orchestrator
Consult each upstream repository for its current implementation, license, full documentation, and updates. Re-check upstream guidance before relying on time-sensitive platform details.