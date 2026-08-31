# Deployment

## Public showcase: GitHub Pages

This repository's `docs/` directory is a static HTML/CSS/JavaScript site. It has no build dependencies and does not run the application.

1. Run `python scripts/check_showcase.py` from the repository root.
2. In GitHub **Settings → Pages**, choose **Deploy from a branch**, branch **main**, folder **/docs**.
3. The public URL is [Distributed File Transfer](https://mayank-vekariya.github.io/Distributed-File-Storage-System/).
4. Push subsequent showcase changes to `main`; check the Pages deployment status before sharing the URL.

The `showcase-check.yml` workflow validates the static page and compiles both POSIX binaries on Linux. It does not test file transfers end to end or run a public server. A Pages deployment may require repository-admin setup; workflow success alone does not prove publishing is enabled.

## Local preview

```sh
python -m http.server 4173 --bind 127.0.0.1 --directory docs
```

## Application hosting

Run the compiled server only on an isolated Linux host or trusted private network with test data. Restrict inbound access at the firewall. Separate the export directory and client output directory. Authentication, TLS, strict path containment, protocol validation and transfer integrity checks are required before an internet-facing deployment. This task publishes only the static project page; it does not launch a file server.

## Publishing checklist

- [ ] HTML/CSS/JavaScript and image references pass the local check.
- [ ] The public page clearly distinguishes illustrations from application output.
- [ ] Project and documentation links resolve.
- [ ] No credentials, private uploads, database files or model weights are included in `docs/`.
- [ ] The Pages deployment finishes successfully.

## Updating and rollback

Keep changes in normal Git commits. To roll back a published showcase, revert only the relevant showcase commit and push the reviewed revert; do not reset unrelated project history. Preserve the résumé's GitHub repository link so visitors can reach both source and showcase.
