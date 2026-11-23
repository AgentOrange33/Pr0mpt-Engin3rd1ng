# Repository Maintenance Rules (`Pr0mpt-Engin3rd1ng`)

## Core Objective
Whenever asked to update `README.md`, synchronize the documentation—specifically the `## Prompt inventory` section—with all `.md` files currently present in the repository root.

## Strict Editing Boundaries
- **ONLY modify `README.md`.** Never edit, rename, reformat, or delete any system prompt files (`*-System-Prompt.md`), `DIY.md`, or `AGENTS.md`.
- **Preserve the repo's voice and structure.** Keep the existing ASCII diagrams, tone ("Serious prompts for defenders. Slightly less serious branding."), `## whoami`, `## Quick start`, `## Design principles`, `## Hard boundaries`, and `## Final transmission` sections intact unless an explicit update is needed.

## How to Sync `## Prompt inventory`
1. **Scan all `.md` files in the repo root** (excluding `README.md` and `AGENTS.md`) and inspect recent git commits (`git log -n 10 --stat`).
2. **Inspect new or modified files.** Read the top header, model name, and intended workload/capabilities inside any newly added `*-System-Prompt.md` or companion guide (such as `DIY.md`) so the description is accurate and grounded in the file's actual content.
3. **Update the `## Prompt inventory` Markdown table:**
   - Ensure every `*-System-Prompt.md` file in the repo has a corresponding row in the table.
   - Format the **Prompt** column cleanly (e.g., `Claude Fable 5.2`, `GPT-6.1 Sol`, `Gemini 4 Argon`) and link it directly to the filename (e.g., `[GPT-6.1 Sol](./GPT-6_1-Sol-System-Prompt.md)`).
   - Write a concise, accurate **Best fit** summary based on the prompt's focus (e.g., deep analysis, high-throughput multimodal, agentic workflows, custom prompt building).
   - Set **Status** to `Production-oriented` (or `Companion guide` for non-system-prompt files like `DIY.md`).
   - Remove table rows only if the corresponding `.md` file was deleted from the repository.
4. **Keep the note below the table intact**, ensuring any newly referenced special-access or frontier model families remain accurately noted without altering the disclaimer.

## Verification Before Finishing
- Verify that every `.md` file in the root directory (except `README.md` and `AGENTS.md`) is accounted for in `README.md`.
- Verify that all relative Markdown links (`./Filename.md`) match the exact case-sensitive filenames in the repository.
