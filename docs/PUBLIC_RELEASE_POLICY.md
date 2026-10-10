# Public Release Policy

This repository is the deliberate public boundary for Timurlenk Engine. The private development repository remains the source of truth for unpublished engine work.

## Default rules

1. **No automatic mirroring.** Changes from private development are selected and reviewed before publication.
2. **No secrets.** Never commit API keys, access tokens, credentials, session data, private URLs containing credentials, or `.env` files.
3. **No unreviewed models or data.** Model weights, checkpoints, training corpora, opening books, and benchmark dumps require provenance, license, size, and privacy review before release.
4. **No unsupported strength claims.** Builds, unit tests, UCI smoke tests, performance measurements, fixed-position comparisons, and self-play strength tests are different evidence classes and must be reported separately.
5. **No implied external integration.** A schema or planned adapter is not a working connection. Document an integration as active only after an end-to-end contract test passes.
6. **Keep the boundary small.** Frontend prototypes, audio/visual assets, mobile wrappers, web relays, and unrelated game prototypes remain outside this repository's engine scope.

## Publication checklist

Before publishing a file or release, confirm:

- [ ] It is intended for public distribution.
- [ ] It contains no secrets or personal/private data.
- [ ] Licenses and provenance are understood for third-party code, models, and datasets.
- [ ] Claims are supported by current, reproducible evidence.
- [ ] Links and referenced schemas resolve.
- [ ] Private-only paths, run logs, and internal infrastructure details have been removed or deliberately approved.

## Security reports

Do not file credentials or exploit details in public issues. Until a dedicated private reporting channel is configured, contact the repository owner privately through GitHub's account contact mechanisms.
