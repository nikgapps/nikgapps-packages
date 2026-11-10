# NikGapps package delivery

Verified package files and metadata used by NikGapps App. GitLab remains the canonical publication source; this repository mirrors a complete pinned snapshot after all referenced files pass SHA-256 and size verification.

- JSON metadata lives on `main`. Resolve its commit once and read all documents with that same `ref`.
- `mirror.json` records the canonical source commit and managed metadata paths.
- Immutable binary objects live in `registry-objects-*` prereleases, named by SHA-256. Labels identify their original package paths. Binary files are not committed to Git.
- Artifact URLs in metadata use GitHub's release asset API. NikGapps App sends the signed-in user's GitHub token and `Accept: application/octet-stream`; it verifies checksums before caching or building.
- Metadata uses the Contents API with `Accept: application/vnd.github.raw+json`. Tokens must never be sent to redirected asset storage.
- Historical package versions remain available for saved projects. Release pointers and withdrawal state follow the canonical metadata. SourceForge download links are preserved.

Publication, rollback, SourceForge link synchronization and manual mirror workflows are maintained in [NikGappsOfficial/deploy](https://github.com/NikGappsOfficial/deploy/actions). The manual **Sync GitHub Registry Mirror** workflow backfills or repairs the mirror without rebuilding packages. Publication is serialized and metadata updates are atomic. Repeating an unchanged snapshot reuses assets and does not create a metadata commit.

Treat managed JSON and release assets as generated data. Change the canonical registry and run the workflow rather than editing generated files here.
