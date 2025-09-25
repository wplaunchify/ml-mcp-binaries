# ML-MCP-Binaries

This repository contains the bridge source and CI workflow used to produce native bridge binaries for the ML Claude Desktop connector.

Purpose
- Produce prebuilt native executables (macOS x86_64 & arm64, Windows x64) for inclusion in MCPB/DXT bundles.
- Publish those binaries as GitHub Release assets so the WordPress plugin (ML Claude Connector) can fetch them automatically.

How to use
1. Add this repo to your GitHub account (owner/repo: e.g., wplaunchify/ML-MCP-Binaries).
2. Push the files and create a tag (e.g., `v1.0.0`). The workflow `.github/workflows/build-binaries.yml` triggers on new tags, builds native executables, and uploads them as release assets.
3. In your WordPress admin, on the plugin's "Binaries" page, enter this repo and the release tag to auto-fetch release assets (or upload ZIPs manually).
4. Generate your MCPB/DXT bundle in the plugin — the plugin will include the correct binaries for darwin & win32.

Security / checksums
- After a release completes, publish SHA256 checksums for each artifact in the release notes or as a separate file in the release assets. That helps verify integrity.

Notes about signing/notarization
- For wide distribution you should sign/notarize macOS and sign Windows binaries. That is outside the scope of the CI by default (you must provide private signing keys/certs), but the produced artifacts can be signed in a follow-up step.

Building locally (if needed)
- Ensure you have Go installed (1.20+ recommended).
- Build commands (examples):
  - macOS (amd64): `GOOS=darwin GOARCH=amd64 go build -o server-darwin main.go`
  - macOS (arm64): `GOOS=darwin GOARCH=arm64 go build -o server-darwin-arm64 main.go`
  - Windows (amd64): `GOOS=windows GOARCH=amd64 go build -o server.exe main.go`

License
- MIT by default (see LICENSE).