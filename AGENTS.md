# AGENTS.md — plugin-door

> **Start at the roadmap and board on [lemonfiber.app](https://lemonfiber.app),
> rendered from the report of where every unreleased version stands. Then the
> rules** every repository shares:
> [working in the repositories](https://github.com/lemonfiber/spec/blob/main/50-governance/working-in-the-repositories.md)
> and [the rules for agents](https://github.com/lemonfiber/spec/blob/main/50-governance/ai-contributors.md).
> This file holds only what is true of this repository.

## What this repo is

A bundled part: Door, as the stack lemonfiber ships carries it. The
[bundle contract](https://github.com/lemonfiber/spec/blob/main/20-architecture/contracts/bundle.md)
says how the catalogue pins it and how lemonfiber carries it.

## The rules you cannot break

- **The plugin id is the service's id** (`ARCH-R266`). The container, the
  configuration directory, the settings and the journal keep their names.
- **One service, speaking `stream.guard@1` as its own upstream** (`ARCH-R344`,
  ADR-0056), on its contract port 8081 apart from the household's 8096 and 8920
  (`ARCH-R343`). It declares `replaces` naming its own id, which is how it takes the
  id, the port and the hostname the bundle reserves for it (`ARCH-R222`).
- **Its proofs' recordings sit under `recordings/door/`**, its conformance
  recordings under `conformance/stream.guard@1/`, and it has no starting files: the
  core writes its envelope's key and its certificate into `/config` (`ARCH-R271`).
- **Every service declares `reaches` and `asks_for`** (`ARCH-R270`).
- **No Python here.** The reader is spec's `first-party-plugin` workflow's.
- **The image is built in `lemonfiber-door`** (`OPS-R93`) and runs under the posture
  this manifest's main declares (`ARCH-R250`); `posture/prepare` gives the image's
  check there the certificate lemonfiber writes at install. Its pin moves here on the
  release app's rolling pull request from there, so a change to the posture or
  `posture/prepare` is proved there on that repository's next run.
