# alfred workflow template (rust)

An Alfred workflow whose menu lives in TOML, served by a Rust binary built on
[we-love-alfred](https://github.com/NorthIsUp/north/tree/main/crates/we-love-alfred):
cached menus, keyword and regex routes, SQLite lookups, GitHub, Okta,
Tailscale and self-updates.

- `workflow/workflow.toml`: the menu. See the we-love-alfred README for the format.
- `src/main.rs`: the `alfred` binary. Add Rust behavior with `.feature(…)`,
  `.keyword(…)` or `.provider(…)`.
- `workflow/info.plist`: one Script Filter (keyword `my`) running `./alfred "$1"`,
  connected to a Run Script action that runs the selected item's arg
  (`open …`, `zsh://…` or `copy:…`).

## Make it yours

1. In `Cargo.toml`, set `name`, `description` and `repository`.
2. In `workflow/workflow.toml`, set `cache` and replace the example items.
3. In `workflow/info.plist`, set `bundleid`, `name`, the Script Filter `keyword`
   and `title`, or open the workflow in Alfred and edit it there.

## Develop

```sh
mise install           # rust with the Apple targets, hk, pkl
cargo install cargo-edit
mise run test
mise run install       # build dist/<name>.alfredworkflow and open it in Alfred
```

`mise run build` builds a universal (arm64 + x86_64) binary into
`workflow/alfred`, copies the `Cargo.toml` version into `info.plist`, and zips
`workflow/` into `dist/<name>.alfredworkflow`.

## Release

`mise run bump-patch` (or `-minor`, `-major`), commit, and push to `main`. CI
tags `v<version>` and attaches the `.alfredworkflow` to a GitHub release.
