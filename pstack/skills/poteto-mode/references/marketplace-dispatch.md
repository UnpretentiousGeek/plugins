# Marketplace dispatch

These instructions apply on Codex and Claude Code. Cursor uses the original skill instructions. Apply the host's delegation and approval rules before launching a worker.

| Use | Codex model | Default effort | Available efforts |
| --- | --- | --- | --- |
| Implementation, debugging, and performance | `gpt-6.2-sol` | max | low, medium, high, xhigh, max, ultra |
| Architecture and demanding review | `gpt-6.2-astra` | max | low, medium, high, xhigh, max, ultra |
| Routine independent work | `gpt-6-luna` | high | low, medium, high, xhigh, max |

Map old GPT-5.6 Sol, GPT-6 Sol, and GPT-6.1 Sol choices to GPT-6.2 Sol. Map GPT-6 Astra and GPT-6.1 Astra choices to GPT-6.2 Astra. Keep their reasoning effort when the target supports it. Honor explicit role choices where the host supports them.

- **Codex.** Use the host's agent tool for Cursor `Task` calls. Pass the model ID and reasoning effort separately. Preserve the worker's brief, access constraints, and output location. For a read-only worker, use the host's read-only mode when available. If the host cannot enforce the required access, handle the work in the parent under its existing permissions.
- **Claude Code.** Use its native agent tool for native Claude roles. For an explicitly selected Codex role, check `codex debug models` for the available IDs and efforts, then launch the signed-in Codex CLI. For example, from the task directory, run `codex -a never exec --sandbox read-only --model gpt-6.2-astra -c 'model_reasoning_effort="max"' - < "$brief_file"` with the worker brief in a local file. For authorized implementation, use `--sandbox workspace-write` from the worker's assigned checkout. If Codex or the requested model is unavailable, report the unavailable lane.
- **Panels.** On Codex, use Astra and Sol for local review roles where supported. They are from the same provider. Count only an independently available provider as a cross-provider reviewer, and report any missing seats. Preserve any worker independence and isolation the workflow requires.
- **Setup.** On marketplace hosts, use the table as defaults and keep explicit role overrides in a user or project instruction file that the host reads. Verify IDs and reasoning levels against the host before saving them. On Codex, check the agent tool's accepted models and efforts. For the external CLI, use `codex debug models`. Use separate model and effort fields in the role instructions. For `inherit-parent` and `auto`, omit the model override.

When a Cursor-specific tool has no host equivalent, use the available host tool that preserves the operation's constraints or report the unavailable step. Apply this reference to every routed skill, including when invoked directly.
