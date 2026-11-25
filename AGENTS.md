# lib-gh

Generated handl SDK for the GitHub CLI — the `gh` port (types + arrow
signatures) plus the `gh-cli-host` adapter over `lib-cli`'s `cli-c`
(posix_spawnp, no shell).

## Layout

| path | role |
| --- | --- |
| `specs/gh.clispec.yaml` | committed source of truth — resolved `*.clispec.yaml` command tree |
| `generated/gh/`, `generated/gh/gh-cli-host/` | gitignored codegen output — never committed |
| `src/gh-cli-host.test.hnl` | smoke tests against generated adapters |
| `pkg.hnl` | manifest — `modules: ["gh", "gh-cli-host"]` |
| `scripts/hnl-gate.sh` | regenerates `generated/` from the spec, then gates |
| `workflows/gate.yaml` | CI — shared `handl-gates` campaign |

## Contract

- Edit `specs/gh.clispec.yaml`, not `generated/`; re-emit with
  `hnl codegen cli specs/gh.clispec.yaml --output generated/gh`.
- Same layout/gate pattern as `lib-cli-gen` (one tool, own repo).

## Verification

```bash
HNL=../host-cli/target/debug/hnl scripts/hnl-gate.sh
```

<!-- myco:agent-awareness -->

## Agent awareness

- Session start / any work discussion: run `myco status --prompt`
  before proposing next steps — know the board first.
- User describes new work → offer to capture it (`myco todo add`,
  `issue new`, `proposal new`). Don't wait to be asked.
- Picking up a task: `myco resume <ID>` is the briefing.
- Wrapping up: `myco handoff <ID>` anything resumable; keep statuses
  honest (claimed → in-progress → blocked/done).

<!-- /myco:agent-awareness -->
