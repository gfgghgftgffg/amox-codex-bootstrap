# amox-codex-bootstrap

Personal Codex setup instructions for Windows, macOS, and Linux. Give Codex [setup.md](setup.md) and let it check the computer, install missing dependencies, and configure your tools and Skills.

## Usage

Install Codex first, then send it this prompt:

```text
Read https://github.com/gfgghgftgffg/amox-codex-bootstrap/blob/main/setup.md
and follow it to configure this computer. Complete the installation,
verify the results, and report anything that still needs my input.
```

You can also download or clone this repository and ask Codex to follow the local `setup.md`.

## Included

- Conda detection and Miniforge installation when needed.
- A shared `codex` environment for Python dependencies, including `pypdf`.
- Task routing: `codex-task-router`.
- Meeting summaries: `meeting-summary-html`.
- Writing: `shuorenhua` and `humanizer`.
- Frontend design: `taste-skill` (`design-taste-frontend`).
- Plan questioning: `grilling` and `grill-me`.
- Minimal global `AGENTS.md` entries for capabilities, local paths, and the Python environment.
- Global `config.toml` settings for memories, idle-sleep prevention, and multi-agent defaults (30 concurrent threads, `gpt-6-luna`, `medium` effort), with the requested Windows-only daemon setting. See [setup.md](setup.md) for exact values.

Codex chooses platform-appropriate commands, reuses compatible installations, and preserves existing configuration. Task routing requires compatible models and profile activation; meeting audio/video transcription requires `DASHSCOPE_API_KEY`. Text-only meeting preparation needs no ASR key.

Edit [setup.md](setup.md) to customize the setup.
