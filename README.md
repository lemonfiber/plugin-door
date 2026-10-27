# Door for lemonfiber

**Lets the household reach the media server, and lets an item's stream or picture out only to someone allowed to see it.**
Door is one of the parts the stack lemonfiber ships is built from.
Without it: The media server answers on this machine only, and nothing else in the house can play from it.

## How lemonfiber carries it

The default bundle in
[lemonfiber-plugins](https://github.com/lemonfiber/lemonfiber-plugins) pins this
repository by a revision and the digests of its manifest and its tree, and
lemonfiber compiles that tree in.
lemonfiber assembles Door into the stack it ships as a stack service.
Its image is the Rust service
[lemonfiber-door](https://github.com/lemonfiber/lemonfiber-door) builds, which
speaks lemonfiber's `stream.guard` contract itself and enforces the media
server's declaration lemonfiber applies over it. A commit on that repository's
main that changes the image publishes it and moves the pin here on a rolling
pull request; this repository builds no image, so the bundle pins its revision.

## What is here

| Path | What it is |
| --- | --- |
| `plugin.toml` | The part's manifest |
| `recordings/door/` | The responses its proofs are held to |
| `conformance/stream.guard@1/` | Its answer to each case of the contract it speaks |
| `posture/prepare` | The certificate lemonfiber writes, made for the image's check in lemonfiber-door |
| `targets.toml` | The lemonfiber its checks run against |
| `proofs.json` | What those checks said, committed |

## Checks

The plugin verdict is one job of spec's
[`first-party-plugin`](https://github.com/lemonfiber/spec/blob/main/.github/workflows/first-party-plugin.yml)
workflow: the manifest as the lemonfiber `targets.toml` names reads it, every
claim against its recording, and every pinned digest. This repository holds no
Python of its own. `just ci` runs the gates that need nothing but this tree.
The image is built and run under the posture this manifest's main declares by
spec's
[`first-party-image`](https://github.com/lemonfiber/spec/blob/main/.github/workflows/first-party-image.yml)
workflow in lemonfiber-door, on each of its pull requests and from its main.

## Licence

The data in this repository is under the licence in `LICENSE`, and so is the
image lemonfiber-door builds.
