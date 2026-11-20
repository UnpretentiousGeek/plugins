# Cursor pstack for Codex and Claude Code

Both marketplaces install the same `pstack/` directory from Cursor. The fork adds marketplace manifests and [host-specific model routing](pstack/skills/poteto-mode/references/marketplace-dispatch.md).

## Codex

```sh
codex plugin marketplace add UnpretentiousGeek/plugins
codex plugin add pstack@cursor-pstack-codex
```

## Claude Code

```sh
claude plugin marketplace add UnpretentiousGeek/plugins
claude plugin install pstack@unpretentiousgeek-plugins
```

Start a fresh session and run `/pstack:poteto-mode`. Claude Code uses the signed-in Codex CLI for explicitly selected Codex roles.

## Updates

Merge `upstream/main` from `cursor/plugins` to update pstack and the other Cursor plugins. When Cursor changes the pstack version, use the same version in both marketplace plugin manifests.

Refresh the marketplace with `codex plugin marketplace upgrade cursor-pstack-codex` or `claude plugin marketplace update unpretentiousgeek-plugins`. If the previous 1.16.0 plugin remains installed, remove it and install pstack again from the refreshed marketplace.
