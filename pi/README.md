# Pi configuration files

These files capture the current personal Pi configuration without credentials or runtime history. Follow [../setup_for_pi.md](../setup_for_pi.md), not a blind copy of this directory.

| Repository file | Installation target |
| --- | --- |
| [AGENTS.md](AGENTS.md) | `<agent-dir>/AGENTS.md`, after substituting verified Conda/Python paths |
| [settings.json](settings.json) | Merge into `<agent-dir>/settings.json`; omit machine-generated `lastChangelogVersion` |
| [open-tui.json](open-tui.json) | `<agent-dir>/open-tui.json` |
| [pi-btw.json](pi-btw.json) | `<agent-dir>/pi-btw.json` |
| [pi-rtk-optimizer/config.json](pi-rtk-optimizer/config.json) | `<agent-dir>/extensions/pi-rtk-optimizer/config.json` (configuration only, not a second extension) |
| [rpiv-ask-user-question/config.json](rpiv-ask-user-question/config.json) | Effective `rpiv-ask-user-question/config.json` under `$XDG_CONFIG_HOME`, otherwise `~/.config` |
| [routing.toml](routing.toml) | Stable Task Router source configuration passed with `--config`; do not copy generated agents from another host |

`<agent-dir>` is `PI_CODING_AGENT_DIR`, otherwise `~/.pi/agent`. The question tool's XDG configuration is separate from this directory, including on Windows.

JSON plugin configurations are exact copies of this computer's non-sensitive files. The AGENTS template differs only in its two local path placeholders. The router configuration matches this computer's generated role map; it does not change the normal Pi startup model.

The question guidance is intentional: clarify material ambiguity in design-tree rounds, investigate facts rather than asking the user to look them up, use the user's language, preserve custom-answer/cancellation behavior, and obtain shared-understanding confirmation before implementing an interviewed task. Install the full JSON verbatim, not a summary or a few extracted guidelines. It does not require separate `grill-me` or `grilling` Skills.

Do not commit `sub2api.json`, `auth.json`, API keys, session logs, model caches, missions, installation manifests, backup history, or generated verification artifacts. Keep credentials local and configure them using the provider's documented secure method. No local package-source patches are included or required by this snapshot.
