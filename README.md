# lib-gh — generated handl SDK for the GitHub CLI

The committed source of truth is the spec, `specs/gh.clispec.yaml` (a
resolved `*.clispec.yaml` command tree for `gh`). Everything under
`generated/` is a **gitignored build artifact** emitted by sdkgen-cli:

- `generated/gh/gh.hnl` — the port (types + arrow signatures),
- `generated/gh-cli-host/gh.hnl` — the adapter over `lib-cli`'s `cli-c`
  (posix_spawnp, no shell).

Regenerate (spec mode — deterministic, no `--help` probing):

```bash
hnl sdkgen cli specs/gh.clispec.yaml --output generated/gh
```

Re-probe `gh` and dump a fresh spec at the same time (writes both the
artifacts and `<cfg emit_spec>`):

```bash
hnl sdkgen cli gh --config sdkgen-probe.yaml --output generated/gh
# sdkgen-probe.yaml:  emit_spec: specs/gh.clispec.yaml
#                     max_depth: 2
```

Gate (`typecheck` + `lint` + `test`, regenerates `generated/` first):

```bash
HNL=../host-cli/target/debug/hnl ./ci.sh        # or scripts/hnl-gate.sh
```

## License

MIT.
