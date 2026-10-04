# amox-codex-bootstrap

Give this file or repository to Codex on a new computer and ask:

> Read setup.md, configure this computer accordingly, verify the installation, and report the results.

This is a task brief for Codex on Windows, macOS, and Linux. Choose commands based on the actual OS, CPU architecture, shell, and current upstream documentation. Complete the setup rather than handing the user a list of commands to run.

## General Approach

- Check before installing. Reuse compatible installations and repair incomplete ones. Repeated runs should not duplicate environments, Skills, or instructions.
- Preserve existing Codex settings, credentials, unrelated Skills, and user instructions. Back up existing files before editing them.
- Prefer user-level installation. Request input only for missing credentials, required permissions, or decisions that cannot be resolved from the existing configuration; continue independent work meanwhile.
- Keep secrets out of this repository, global instructions, and reports. Limit upstream installation actions to the capabilities requested below.

## 1. Conda and Python

Find an existing Conda installation by checking PATH, the active environment, and common installation locations. A missing shell command alone does not mean Conda is absent.

If Conda is missing, install a compatible Miniforge release from its official source, verify the download, and use a user-owned installation directory. Select the correct OS and architecture without replacing system Python. Report unsupported platforms clearly.

Reuse the Conda environment named `codex`, or create it with Python 3.12 if absent. Keep an existing Python version if it satisfies the required tools.

**Install all Python libraries, Python CLI tools, and future Python dependencies for this setup into the `codex` environment.** Do not install them into system Python, Conda base, or with `pip --user`. Use the environment's interpreter for pip and scripts, for example `conda run -n codex python -m pip ...`.

Check whether `pypdf` imports successfully in this environment. Install it if missing and verify the import afterward.

For other dependencies, inspect the upstream requirements first. Reuse compatible Node.js, Git, and other non-Python tools. If missing, prefer installing them into the `codex` environment through Conda, falling back to an appropriate user-level installation when necessary. Install only what the projects below require.

## 2. Projects and Skills

Read each project's current README and installation instructions. Check for an existing installation, then install using a method supported by the current Codex version. Include referenced scripts, reference documents, and other runtime resources, not just `SKILL.md`.

Respect `CODEX_HOME` and existing global Skill locations. Avoid registering the same Skill in multiple directories. Keep required source checkouts in a stable user-owned directory so installation does not depend on this setup file or a temporary download folder remaining in place.

| Project / Skill | Source | Installation Notes |
| --- | --- | --- |
| codex-task-router | https://github.com/gfgghgftgffg/codex-task-router | Use the native installer for roles, profile, global entry, and the `task-routing` Skill. Copying the Skill alone is insufficient. |
| meeting-summary-html | https://github.com/gfgghgftgffg/meeting-summary-html | Include its scripts and references. Run Python helpers through the `codex` environment. |
| shuorenhua | https://github.com/MrGeDiao/shuorenhua | Follow its Codex installation instructions and include the full Skill and reference files. |
| humanizer | https://github.com/blader/humanizer | Install the complete Skill and its referenced resources. |
| taste-skill | https://github.com/Leonxlnx/taste-skill | Install the primary frontend design Skill, currently named `design-taste-frontend` in its frontmatter under `skills/taste-skill/`, with its referenced resources. Select this Skill explicitly; the repository also contains optional variants that are not required by this setup. |
| grilling | https://github.com/mattpocock/skills/blob/main/docs/productivity/grilling.md | This URL is documentation. Locate the actual Skill, currently `skills/productivity/grilling/`. |
| grill-me | https://github.com/mattpocock/skills/blob/main/docs/productivity/grill-me.md | This URL is documentation. Install the actual Skill, currently `skills/productivity/grill-me/`, together with its `grilling` dependency. |

### Task Router

Check the required Node.js version and dependencies. Follow the upstream check, preview, and installation workflow, retaining its backup and conflict protections.

Verify that the configured models, providers, and reasoning levels are compatible with this Codex installation. Do not assume the user has access to upstream default models or silently replace existing model preferences. Reuse compatible settings when available; otherwise complete independent setup steps and report the model information still needed.

The upstream profile currently starts with `codex -p task-routing`. Global installation does not automatically activate routing in every session. Follow current upstream documentation and host capabilities, and distinguish installed configuration from an active profile.

### Meeting Summary

Check the helpers' actual dependencies; the current preparation scripts use the Python standard library.

Text input requires no ASR credentials. Audio/video transcription requires `DASHSCOPE_API_KEY`. If absent, report transcription as pending configuration without blocking text summaries or other installations. Do not upload real media or make paid requests just to test the installation.

## 3. Minimal Global AGENTS.md

Locate the global instructions used by this Codex installation, normally under `CODEX_HOME` or `~/.codex`. Check whether `AGENTS.override.md` or host-specific settings affect which file is loaded.

Keep global instructions as short as possible. Do not list or describe Skills that Codex already discovers through its Skill catalog, or repeat their paths, triggers, or workflows. Do not add a bootstrap managed block, start/end markers, or installation history. Preserve unrelated user instructions and the Task Router installer's own entry.

Record only environment conventions and entry points that are otherwise missing:

- Python: use the `codex` Conda environment for Python execution and dependency installation; include the working Conda and interpreter paths. Note briefly that `pypdf` is installed.
- Skill exceptions: only if a required entry is not exposed by the host, add a minimal pointer. For example, if `grill-me` is not exposed, retain a single line for user-requested plan questioning with its local path and its `grilling` dependency. Do not add this exception when the host already provides the entry.
- Task Router: its local entry or configuration path and the required profile activation, unless the upstream installer already supplies that information.

Leave detailed behavior in the Skills themselves and installation status in the final report. Remove redundant Skill inventory entries previously added by this setup, while preserving user-specific instructions and necessary exceptions. Do not duplicate Task Router instructions already written by its installer.

## 4. Global config.toml

Locate the global `config.toml` under the effective `CODEX_HOME` (normally `~/.codex`). Back up an existing file, then merge the following requested settings into its top-level `[features]` and `[agents]` tables. Create the file or tables if missing. Update these keys in place, preserving unrelated settings, provider credentials, profiles, and agent role definitions; do not append duplicate TOML tables or keys.

```toml
[features]
memories = true
prevent_idle_sleep = true
multi_agent = true
multi_agent_v2 = false

[agents]
max_concurrent_threads_per_session = 30
default_subagent_model = "gpt-6-luna"
default_subagent_reasoning_effort = "medium"
```

**Windows only:** also set `daemon_auto_start = false` inside `[features]`. On macOS and Linux, do not add or change that key as part of this setup.

These values are explicitly requested defaults and should replace existing values for the listed keys. Keep `gpt-6-luna` and `medium` as specified. Check support in the installed Codex version and report unsupported settings or unavailable models instead of silently substituting alternatives. If an active profile or Task Router role overrides these defaults, report the effective difference without rewriting its role configuration.

## 5. Verification and Report

Verify the following after installation:

1. Python runs from the `codex` environment and can import `pypdf`; confirm the interpreter's location.
2. All seven project / Skill entries and required resources are present, and `grill-me` can find `grilling`.
3. Task Router's installation checks pass. Distinguish static configuration checks, host support, and live model verification; do not make paid model calls for this check.
4. The meeting preparation helper processes a temporary text fixture locally without credentials or media uploads.
5. Global instructions are in the effective location, preserve user-specific content, and do not repeat automatically discovered Skills. Keep only the environment convention and necessary entry-point exceptions alongside the upstream Task Router entry.
6. Global `config.toml` parses successfully, contains the requested settings without duplicate tables or keys, and preserves unrelated configuration. Confirm the Windows-only setting was applied only on Windows. Distinguish saved values from settings actually supported and effective in the current host.

Report each item as newly installed, reused, pending configuration, or failed. Include key paths, sources, and installed versions or commit IDs. Explain any required new session, reload, or profile activation. For failures, give the specific cause and next step; do not report partial completion as full success.
