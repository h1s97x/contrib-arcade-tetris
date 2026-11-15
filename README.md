# contrib-arcade-tetris

> **Read-only distribution channel.** This repository is generated from
> [`contrib-core`](https://github.com/h1s97x/contrib-core) by the release pipeline. Please open issues
> and pull requests in the core repository, not here.

**Status: ready** — this game is implemented in core and usable today.

Falling pieces line up with the contribution grid.

CNB: `h1s97x/plugins/contrib-arcade-tetris`. GitHub mirror: `h1s97x/contrib-arcade-tetris`. Create this mirror separately to use the shell as a GitHub Action.
`action.yml` points at the core mirror `h1s97x/contrib-core`, which must exist before
this shell's workflow can run.

This repository is a **thin shell**. It contains no game code: it fixes
`renderer: tetris` and forwards every other input to the shared
[core](https://github.com/h1s97x/contrib-core). The core owns the contribution data sources, the 53×7
grid, palettes, all renderers, the CLI, the GitHub Action and the CNB plugin.

## Usage

```yaml
- uses: h1s97x/contrib-arcade-tetris@main
  with:
    github_user_name: ${{ github.repository_owner }}
    outputs: |
      tetris.svg
      tetris-dark.svg?palette=github-dark
```

Everything else from the core Action works here too: `platform`, `user_name`,
`github_token` and the per-output query options (`palette`, `color_dots`,
`color_snake`, `renderer`). See the [core README](https://github.com/h1s97x/contrib-core#readme).

## Why a separate repository

One repo per game means its own issues, README, preview, release cadence and
maintainers. Someone can be given write access to just this game's shell
without touching the other seven. Upgrades still happen once, in the core.

## Forking

Fork this repo to change branding, default outputs, issue templates or
maintainers without touching game logic. To use your own core, edit the `uses:`
line in `action.yml` from `h1s97x/contrib-core@main` to your fork and ref.

To change how the game actually plays, open a PR against the core renderer in
[h1s97x/contrib-core](https://github.com/h1s97x/contrib-core) instead — every shell picks up the change
automatically.

## Regenerating

This shell was produced by `bun run scaffold` in the core repo. To keep all
shells in sync, change `templates/shell/` there and re-run it, rather than
editing generated files by hand.

## License

MIT. See [LICENSE](./LICENSE).
