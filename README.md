# Timurlenk Engine Core — Public Surface

> **Repository status: documentation scaffold.** The repository is intended for public-facing documentation and reviewed interface notes; it is not yet a release of the engine implementation.

Timurlenk is an engine project for a chess variant with an 11×10 board and two citadel squares. The project is being organized around a small, independently testable engine core, with user interfaces and game prototypes kept outside the core.

## Repository boundaries

- This public repository is for the project overview, architecture notes, versioned interface/data contracts, sanitized examples, and deliberately approved releases.
- Engine source, private experiments, unreviewed model/checkpoint files, training data, credentials, and internal audit artifacts do not belong here by default.
- The internal engine Persona/search profile is distinct from the separate Persona research system. No live integration between those systems is claimed here.
- Public release decisions are review-gated. Private development content is never copied here automatically.

## Current status

- Public documentation scaffold: prepared.
- Engine source, binary release, and packaged models: not published by this scaffold.
- Variant correctness and engine strength claims: to be documented only with reproducible evidence and clearly scoped test results.

## Planned public contents

1. Project scope and architecture summaries.
2. Stable, reviewed interface and experiment-data contracts.
3. Build/test instructions once reviewed public source or a release is available.
4. Versioned release notes and validation reports that do not expose private data.

## Development principles

- Keep the engine core independent of frontends, mobile packaging, and multiplayer services.
- Preserve reproducible tests and benchmark provenance.
- Separate functional correctness, search speed, fixed-position quality, and playing-strength claims.
- Treat the external Persona adapter as unimplemented until a real schema exchange and end-to-end test prove otherwise.

See [Public Release Policy](docs/PUBLIC_RELEASE_POLICY.md) before proposing changes to this public surface.
