# KisiLab build & verification report

Build version: 1.1.0

## Executed successfully in this workspace

- `npm ci --offline --no-audit --no-fund` — passed (project uses no Node runtime package dependencies; browser libraries are version-pinned in `browserDependencies` and loaded from CDN).
- `npm run build` — passed; static output created in `dist/`.
- `npm test` — 6/6 tests passed.
- `node --check src/main.js` — passed.
- `node --check netlify/functions/_ai.js` — passed.
- ZIP integrity test — passed after packaging; archive paths are rooted directly at project files (no outer `KisiLab/` directory).

## Not verified here

- Real Gemini/OpenAI API requests: require the user's own API key, account quota, and a deployed Netlify Functions environment.
- End-to-end Netlify deployment and Android installation: require a live Netlify site.
- Browser visual/interaction smoke test: headless Chromium launch timed out in this environment while loading remote CDN modules. Do not interpret unit tests as a full browser QA pass.
- OCR, DOCX/PDF/XLSX parsing and Word/PDF export: depend on external browser libraries/CDN and real sample files; not fully exercised end-to-end here.

## Known product limitations

- Image generation is explicitly not enabled; the AI function returns HTTP 501 rather than pretending to create an image.
- Automated difficulty-equivalent multi-form generation and psychometric item statistics are not implemented.
- IndexedDB keys are not encrypted. Keys are sent over HTTPS to Netlify Functions only when the user requests AI.
- Netlify Drop static drag-and-drop does not install Functions. Deploy through GitHub integration for AI functionality.
