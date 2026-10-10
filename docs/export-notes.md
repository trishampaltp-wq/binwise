# Export notes

Exported 10 October 2026 from the current Binwise Site source, commit `18b4132ff9e88bd4b15c343b0949ced3fa8fc020`.

All files under `src/` and `tests/`, the original HTML entry point, demo launcher, and architecture/pitch/metrics documentation are preserved byte-for-byte. The project contains no server implementation or private runtime assets.

Changes for portability: ordinary Vite dev/preview scripts, a Node.js requirement, package description, `.nvmrc`, expanded `.gitignore`, relative Vite asset paths and standalone setup documentation. The Site hosting configuration and Git metadata are excluded. The live Site has not been modified.

Assets consist of inline SVG in the React source, CSS, dependency-provided Lucide icons and externally loaded Google Fonts. No separate image/video assets exist in this source version. The original Google Fonts import is preserved and has not been bundled for offline use.

The PPTX pitch deck is a separate deliverable, not an app dependency. Pitch text and architecture documents from the Site are included.

Verification: identical hashes for original application and test files, clean npm installation, eight passing engine tests and a successful production build. Browser-based visual comparison is not performed. The included dist directory is built from this standalone package.
