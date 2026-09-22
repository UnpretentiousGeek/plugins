# pstack for Codex

This fork keeps Cursor's original `pstack/` directory and adds a Codex marketplace entry at `.agents/plugins/marketplace.json`. The installable Codex plugin lives at `plugins/pstack/`.

The Codex plugin is adapted from [open-pstack 1.4.1](https://github.com/ericlitman/open-pstack/tree/de67e6b40511814171e5e4c8ad7af3b79f07c9ee/plugins/pstack), which ports Lauren Tan's original pstack workflows. Its `LICENSE`, `NOTICE.md`, `CHANGES.md`, and `UPSTREAM.md` are included with the plugin. The copied port tracks Cursor pstack through commit `f8abeddd1862dc73704e3d719dd73df0d51b8c71` (pstack 0.15.1); this fork's original `pstack/` is currently at 0.15.2. These are separate trees so a Git merge of Cursor's updates does not silently change the Codex plugin.

## Install

```sh
codex plugin marketplace add UnpretentiousGeek/plugins --ref main
codex plugin add pstack@cursor-pstack-codex
```

Start a new Codex task after installation. Ask Codex to use `pstack:poteto-mode` for a task. The full multi-model workflows need the external model CLIs described in the plugin's setup skill; the core skills can be read without those tools.

## Update from Cursor

In a clone of this fork, configure the original repository once:

```sh
git remote add upstream https://github.com/cursor/plugins.git
```

To receive Cursor changes:

```sh
git fetch upstream
git merge upstream/main
git push origin main
```

That updates `pstack/` and the other original Cursor plugins. It does **not** port the new pstack behavior to `plugins/pstack/`. Review the changes to `pstack/` since the commit recorded in `plugins/pstack/UPSTREAM.md`, adapt them in `plugins/pstack/`, update the provenance and version, validate the Codex plugin, then push. This review is necessary because Cursor-specific tools, model names, and automations need Codex equivalents.

After pushing an updated Codex plugin, refresh the marketplace with `codex plugin marketplace upgrade cursor-pstack-codex` and start a new task.
