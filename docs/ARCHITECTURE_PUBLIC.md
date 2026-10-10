# Timurlenk Engine — Public Architecture Summary

## Active core responsibilities

- Variant board/state, legality, move generation, and make/unmake.
- APEX search, transposition table, move ordering, and time management.
- Evaluation (HCE and cognitive NNUE) and the engine's internal Persona/Psyche profile.
- UCI protocol adapter.
- Reproducible tests, model-manifest verification, and opt-in experiment logging.

## Deliberately separate components

The web/visual interface, mobile packaging, audio/visual assets, multiplayer relays, and external Persona research system are separate projects. They must not be treated as core engine dependencies.

## External Persona boundary

The internal `PersonaLayer` describes engine-side play-style/search/evaluation behavior. It is not the external Persona research system. A proposed experiment-data contract is not a live integration. Any future connector must be versioned and validated with an end-to-end contract test.

## Evidence policy

Report build status, correctness tests, performance/NPS benchmarks, fixed-position quality tests, and game-strength measurements separately. Passing unit tests does not prove playing-strength gains. Do not make Elo claims without a suitable, repeatable, statistically evaluated match protocol.
