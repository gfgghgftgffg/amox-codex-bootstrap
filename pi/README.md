# Pi configuration files

These files capture the current personal Pi configuration without credentials or runtime history. Follow [../setup_for_pi.md](../setup_for_pi.md), not a blind copy of this directory.

| Repository file | Installation target |
| --- | --- |
| [AGENTS.md](AGENTS.md) | `<agent-dir>/AGENTS.md`, after substituting verified Conda/Python paths |
| [settings.json](settings.json) | Merge into `<agent-dir>/settings.json`; omit machine-generated `lastChangelogVersion` |
| [open-tui.json](open-tui.json) | `<agent-dir>/open-tui.json` |
| [pi-btw.json](pi-btw.json) | `<agent-dir>/pi-btw.json` |
| [subagents.json](subagents.json) | `<agent-dir>/subagents.json`; strict role dispatch, agent-file checks, and native lean workflows |
| [routing.toml](routing.toml) | Stable Task Router source configuration passed with `--config`; do not copy generated agents from another host |

`<agent-dir>` is `PI_CODING_AGENT_DIR`, otherwise `~/.pi/agent`.

JSON plugin configurations are copies of this computer's non-sensitive settings. The package list uses unversioned sources to install the latest releases. The AGENTS template differs only in its two local path placeholders. The router configuration matches this computer's generated role map; it does not change the normal Pi startup model.

Skill installation and the required `disable-model-invocation: true` setting are covered in [setup_for_pi.md](../setup_for_pi.md). Neither global AGENTS template automatically triggers a grilling interview.

Install the lean subagent/web/todo facades listed in settings without separately loading their upstream engines. Task Router uses flat `agents/tr_*.md` and the lean `web_access` tool; generate roles with its current Pi installer.

Do not commit `sub2api.json`, `auth.json`, API keys, session logs, model caches, missions, installation manifests, backup history, or generated verification artifacts. Keep credentials local and configure them using the provider's documented secure method. No local package-source patches are included or required by this snapshot.
