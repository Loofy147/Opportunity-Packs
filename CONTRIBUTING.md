# Contributing

1. Make changes on a topic branch.
2. Add or update the appropriate regression test before fixing behavior.
3. Run the CI commands from `.github/workflows/validate.yml` locally.
4. Validate workflow/bootstrap/test JSON with the Opscotch schema validators.
5. Preserve explicit `NOT_RUN` status for any runtime validation you did not execute.
6. Update the pack README, manifest, validation report, and checksums when source content changes.
7. Do not publish or deploy candidate packs until all release gates in `docs/VERIFICATION_POLICY.md` pass.
