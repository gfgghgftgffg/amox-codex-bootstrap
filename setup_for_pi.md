# amox-codex-bootstrap — Pi

Give this file or repository to Pi on a new computer and ask:

> Read setup_for_pi.md, configure this computer accordingly, verify the installation, and report the results.

This is a task brief for Windows, macOS, and Linux, based on this computer's installed Pi packages, Skills, global instructions, and non-sensitive configuration. Complete the setup rather than handing the user commands. Read current upstream documentation and select commands for the actual OS, architecture, shell, and installed host version.

## General Approach

- Check before installing; reuse compatible installations. Repeated runs must not duplicate packages, Skills, role definitions, or instruction blocks.
- Back up files before editing. Merge requested settings in place, preserving unrelated user instructions, packages, credentials, and configuration. Do not replace an existing whole agent directory.
- Use user-owned installation locations. Respect `PI_CODING_AGENT_DIR` (default `~/.pi/agent`), `XDG_CONFIG_HOME`, and the effective configuration paths documented by each package.
- Read third-party package manifests and installation instructions before running installation actions. Install only the capabilities requested here; do not enable optional hosted tools or additional permissions.
- Keep secrets local and out of this repository, global instructions, and reports. Do not copy sessions, caches, missions, manifests, backups, or old machine paths.
- Missing credentials or unavailable models must not block independent steps. Report these as pending, not as a working installation. Do not make paid model calls, upload private files, or activate delegation merely to verify setup.
- Fetch all referenced files from this repository if working from a downloaded copy of this document alone. The [pi/ directory](pi/README.md) contains fixed configuration sources, not illustrative snippets to paraphrase.

## 1. Pi, Conda, and Dependencies

Reuse an installed Pi when compatible. If absent, follow the [official Pi installation instructions](https://github.com/earendil-works/pi). The inspected host is **Pi 1.0.2**, requiring Node.js **22.19 or newer**. Prefer an official supported user-level installation; the documented npm alternative is `npm install -g --ignore-scripts @earendil-works/pi-coding-agent`. Do not downgrade or update a working host merely to match this snapshot. Verify `pi --version` and the actual shell used by Pi; on Windows check Git Bash or another currently supported shell.

Find an existing Conda installation through PATH, environment variables, and common installation locations. A missing PATH command alone does not mean Conda is absent. If needed, install the appropriate official Miniforge release, verify its download, and use a user-owned directory without replacing system Python.

Reuse the Conda environment named `codex`, shared with the Codex setup. If absent, create it with Python 3.12; retain an existing compatible Python version. **All Python execution, libraries, CLI tools, and future Python dependencies for this setup must use this environment**, never system Python, base, or `pip --user`. Use its interpreter for scripts and pip, for example `conda run -n codex python -m pip ...`.

Check `pypdf` imports and install it only if missing. Reuse compatible Node.js and Git. For missing non-Python dependencies prefer Conda where supported, otherwise the tool's official user-level installation. Only install tools required by the requested packages and Skills.

## 2. Pi Packages

Install these **9 user-level packages** through Pi's package manager, for example `pi install npm:pi-subagents`, without `--local`. Preserve their relative order when merging with existing package declarations; do not also copy their extension entrypoints into auto-discovery directories.

Install the latest releases of these packages; do not pin versions.

| Package source | Purpose / source |
| --- | --- |
| `npm:@indexyz/pi-provider-sub2api` | Relay provider and model discovery; [source](https://github.com/5aaee9/pi-agent-extensions/tree/main/pi-provider-sub2api) |
| `npm:@narumitw/pi-btw` | Side conversation; [source](https://github.com/narumiruna/pi-extensions/tree/main/packages/pi-btw) |
| `npm:pi-open-tui` | Terminal interface; [source](https://github.com/OldSuns/pi-open-tui) |
| `npm:@narumitw/pi-statusline` | Status line; [source](https://github.com/narumiruna/pi-extensions/tree/main/packages/pi-statusline) |
| `npm:pi-web-access` | Search, fetch, source checking and stored content; [source](https://github.com/nicobailon/pi-web-access) |
| `npm:pi-subagents` | Subagents, council and its own workflows; [source](https://github.com/nicobailon/pi-subagents) |
| `npm:@juicesharp/rpiv-todo` | Task tracking; [source](https://github.com/juicesharp/rpiv-mono/tree/main/packages/rpiv-todo) |
| `npm:@quintinshaw/pi-dynamic-workflows` | Separate Dynamic Workflows engine; [source](https://github.com/QuintinShaw/pi-dynamic-workflows) |
| `npm:@heyhuynhgiabuu/pi-pretty` | Tool/transcript presentation; [source](https://github.com/heyhuynhgiabuu/pi-pretty) |

Use `pi list` to check declarations and inspect installed manifests/resources. A package entry is not proof that its extensions load. Restart Pi after package changes and inspect diagnostics. UI/footer extensions can compete for the same host hooks; preserve the requested packages and configuration, and report actual conflicts rather than removing one without permission.

### External tools and credentials

- `pi-web-access`: follow its current provider setup. Reuse existing search credentials or supported keyless paths; do not manufacture keys or enable every provider. Distinguish tools loaded from authenticated search/fetch capability. Install optional video/browser tooling only if requested, not for the text/setup checks here.
- Sub2API: create or reuse the local provider configuration only with the user's real relay details. Prefer the documented token environment-variable reference, such as `${SUB2API_TOKEN}`, where supported. Keep the provider name `sub2api` to match this snapshot. Never copy this computer's token or service URL into this repository; request missing relay details privately. Do not enable priority/fast, server-hosted tools, or other paid modes as part of setup.

## 3. User Skills and Package-Bundled Skills

Read each project's current installation instructions. Install the complete Skill directory with scripts, references, and assets into `<agent-dir>/skills/`, or reuse an existing discoverable complete copy without registering it twice. Keep needed source checkouts in a stable user-owned location. For a host-neutral Skill, use Pi's documented Skill discovery rather than Codex-specific installation paths.

| User Skill | Source | Requirements |
| --- | --- | --- |
| `design-taste-frontend` | https://github.com/Leonxlnx/taste-skill | Install the primary Skill, currently under `skills/taste-skill/`; use its frontmatter name. Optional variants are not requested. |
| `humanizer` | https://github.com/blader/humanizer | Include the full Skill and referenced resources. |
| `meeting-summary-html` | https://github.com/gfgghgftgffg/meeting-summary-html | Include `scripts/prepare_meeting_input.py` and references. Run helpers with the `codex` interpreter. |
| `shuorenhua` | https://github.com/MrGeDiao/shuorenhua | Include the full Skill and reference files. |
| `task-routing` | https://github.com/gfgghgftgffg/task-router | Generate with the Pi native installer in section 5; copying a Codex Skill is incorrect. |
| `grilling` | https://github.com/mattpocock/skills/blob/main/docs/productivity/grilling.md | Documentation URL; install the actual Skill, currently `skills/productivity/grilling/`, with its resources. |
| `grill-me` | https://github.com/mattpocock/skills/blob/main/docs/productivity/grill-me.md | Documentation URL; install the actual Skill, currently `skills/productivity/grill-me/`, alongside its `grilling` dependency. |

After downloading `grill-me`, `grilling`, and `meeting-summary-html`, add `disable-model-invocation: true` below `description` in each installed `SKILL.md`, inside the opening `---` block. If the field already exists, set it to `true`.

Install `grill-me` and `grilling` as sibling directories so `grill-me/SKILL.md` can read `../grilling/SKILL.md`. In Pi, invoke these Skills explicitly with `/skill:<name>`.

Text meeting preparation requires no ASR key; media transcription requires `DASHSCOPE_API_KEY`. Do not upload real media during verification.

The packages in section 2 also provide **four Skills**: `pi-subagents` and `council-mode` from `pi-subagents`, plus `workflow-authoring` and `workflow-patterns` from Dynamic Workflows. Let the packages expose them through their manifests; do not copy them into the user Skill directory. Verify eleven intended Skills in total (seven user Skills and four package-bundled Skills), allowing preserved unrelated Skills.

## 4. Fixed Settings and Plugin Configurations

Use [pi/settings.json](pi/settings.json) as the requested settings source. Merge its packages by identity, preserving unrelated declarations, avoiding duplicate sources or resource filters that hide required functionality. Set its listed non-package preferences in place, preserving other keys:

- `defaultProvider`: `sub2api`
- `defaultModel`: `gpt-6.1-sol`
- `defaultThinkingLevel`: `medium`
- `enabledModels`: `["sub2api/*"]`
- `tuiMode`: `fullscreen`; `theme`: `dark`

These are intentional personal defaults, not generic provider examples. Preserve them and report unavailable models/providers or unsupported thinking levels. Do not silently substitute another model. The relay must be configured before model discovery can validate them. Explain if the requested `enabledModels` scope hides other existing providers; keep their credentials and configuration intact. Do not copy machine-generated `lastChangelogVersion`.

Back up and apply these fixed non-sensitive plugin configurations, creating parent directories as needed. On a fresh installation copy them verbatim; on an existing installation replace the listed template-owned values, recursively preserving unrelated object keys. JSON arrays from these files are complete requested values, not append-only lists.

| Fixed source | Effective target |
| --- | --- |
| [pi/open-tui.json](pi/open-tui.json) | `<agent-dir>/open-tui.json` |
| [pi/pi-btw.json](pi/pi-btw.json) | `<agent-dir>/pi-btw.json` |

The BTW config intentionally selects `sub2api/gpt-6.1-sol`; verify it separately from the main model. No package-source patch, extra UI locale package, or local evidence bundle is required.

Check supported configuration fields against installed package versions. If an upgrade changes the schema or removes a field, preserve the source template, report the incompatibility, and ask before changing its intended behavior.

## 5. Task Router for Pi

Use https://github.com/gfgghgftgffg/task-router and read its current README and [Pi adapter documentation](https://github.com/gfgghgftgffg/task-router/blob/main/docs/pi.md). Install `pi-subagents` and `pi-web-access` first. Keep the source checkout and a working copy of [pi/routing.toml](pi/routing.toml) in a stable user-owned directory; this file reproduces the installed role-map models, thinking levels, selection hints, 30 requested concurrent children, and five repair follow-ups.

The role map uses `deepseek-flash`, `gpt-6.1-sol`, and `gpt-6-astra`; omitted candidate providers inherit the active parent provider. Verify exact registered model IDs and per-model Pi thinking levels without paid generation. Do not infer that `max` means upstream `ultra`, rely on silent clamping, or replace unavailable candidates. If model evidence is missing, finish independent setup and report it explicitly as unverified/pending.

From the Task Router checkout, using the actual absolute configuration path:

```text
npm ci
node cli.mjs doctor --host pi --config <absolute-routing-config>
node cli.mjs install --host pi --config <absolute-routing-config>
node cli.mjs install --host pi --config <absolute-routing-config> --apply
```

Respect `PI_CODING_AGENT_DIR`, or pass the matching `--pi-home`. Retain installer backup, manifest, concurrency checks, and conflict protection. Do not delete manifests or hand-edit generated role files to bypass conflicts. Generate Pi's `agents/task-routing/*.md`, complete `skills/task-routing/` and references, and the single `pi-task-router` instruction block. Keep Codex and Pi homes and generated bundles separate. Future changes must use the same stable source config and rerun the installer.

`doctor` is static: without a credential-free verified Pi registry snapshot, model existence and thinking support remain `UNVERIFIED`. Supply `--catalog` only when its contents come from actual host metadata, not a fabricated capability list. In Pi, inspect `/subagents-doctor`, `/subagents-models`, and loaded `tr_*` capabilities without dispatching children. Check that background children can load both the provider and all four pi-web-access tools; parent tool availability alone does not prove this. Report Windows runner limitations as documented by the installed version.

After installation restart Pi or `/reload`; activate routing only when explicitly requested with `/skill:task-routing`. Installation itself neither activates routing nor authorizes delegation. Pi's `-p` is print mode, **not** a Codex-style profile flag. The router's recommended orchestrator (`gpt-6-astra`, `medium`) does not change the normal Pi startup default (`gpt-6.1-sol`, `medium`). Report this intentional difference without changing either automatically.

Task Router uses **pi-subagents' own async workflow interface**, not the separately installed Dynamic Workflows engine. Keep both packages installed; do not substitute one execution protocol for the other. A workflow concurrency request is not a Pi-wide session concurrency setting and does not override stricter host limits.

## 6. Fixed Global AGENTS.md

Use [pi/AGENTS.md](pi/AGENTS.md), not the Codex [templates/AGENTS.md](templates/AGENTS.md). It is the actual Pi global instruction text, with only these machine-specific placeholders:

- `{{CONDA_PATH}}`: verified absolute Conda executable path.
- `{{PYTHON_PATH}}`: verified absolute `codex` environment Python interpreter path.

Locate the effective global context file under `<agent-dir>` and check `AGENTS.override.md` and other host context-file precedence. On a fresh installation render the template verbatim after installing dependencies and the router. On an existing installation back up and replace only the corresponding Python, proxy, and router entries, preserving unrelated instructions and exactly one Pi router block. Do not paraphrase, expand it into a Skill inventory, or import the Codex grill-me instruction.

Retain the router install manifest and its managed-block protections. The template's router block matches the inspected upstream Pi installer; if a future release changes that block, report and resolve the discrepancy instead of blindly replacing installer-managed policy. Do not render unresolved paths or claim `pypdf` is installed when the dependency step failed.

The proxy instruction records `127.0.0.1:7897`; use it only when available and network access is failing or slow. Do not force permanent system-wide proxy settings on a different computer.

## 7. Verification and Report

1. Verify Pi/Node/Git and the actual shell; confirm the Conda interpreter location and successful `pypdf` import in `codex`.
2. Verify all 9 package declarations, installed resources, and startup diagnostics. Distinguish installed from loaded and UI hooks from tested rendering.
3. Verify the seven user Skills and four package-bundled Skills with their resources, without duplicate names. Confirm `grill-me` can find `grilling`, and `grill-me`, `grilling`, and `meeting-summary-html` have `disable-model-invocation: true`. Check explicit Skill commands after restart or `/reload`.
4. Run the meeting preparation helper with a temporary text fixture locally; verify a transcript and no ASR use. Do not upload media or make paid requests.
5. Parse every deployed JSON; compare template-owned values against the [pi/ sources](pi/README.md). Static checks are not proof of real UI rendering or model adherence to a Skill; do not make a paid model turn solely for setup.
6. Verify saved model/UI defaults and the BTW model; distinguish registry metadata, authenticated connectivity, and live inference. Missing credentials or unverified model/thinking support must remain pending.
7. Verify Router configuration, generated `tr_*` roles, contracts, references, and a single Pi router block. Distinguish static `doctor` success from background runtime support and real dispatch; do not activate routing or launch agents solely to test.
8. Verify global instructions against the rendered Pi template, no unresolved placeholders, and preserved unrelated instructions. Recheck that rerunning unchanged setup produces no duplicate registrations or instruction blocks.

Report each item as newly installed, reused, pending configuration, or failed. Include effective paths, package versions, Skill/router source commits, saved defaults, meaningful differences from this snapshot, and any restart or activation required. Give specific blockers and next steps. Never describe partial or static-only verification as full operational success.
