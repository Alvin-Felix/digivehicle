# DigiLoan Master Ultimate

An offline-first, browser-based field investigation tool for vehicle loans. The app runs entirely from static HTML/JS and is optimized for mobile inspectors collecting borrower information in Tamil or English.

## Project structure
- **index.html** – Main single-page experience with bilingual forms, speech features, simulated OCR, validation, progress tracking, and Word export.
- **ending.html** – Printable acknowledgement page showing reference number, next steps, and required documents.

## How the app works
- **Schema-driven form flow**: Sections such as Identity, Personal Details, Address, Employment, Financials, Loan Request, and Assets are defined in a `schema` array. Navigation moves through `app.step`, with progress indicated by a footer bar.
- **State management**: User inputs are stored in `app.data`; completed records are persisted in `localStorage` under `DigiLoan_Ultimate_V2`. A dashboard lists prior cases and allows Word export.
- **Bilingual UI**: `app.lang` toggles between Tamil (`ta`) and English (`en`); labels and option values are translated via `optMap` and per-field text keys.
- **Speech & scan helpers**: Buttons let users read labels aloud (`SpeechSynthesis`), capture input via speech recognition (Chrome only), and trigger simulated OCR for key fields.
- **Calculated helpers**: Financial and loan sections show live badges for disposable income and on-road price/pending margin based on entered numbers.
- **Data integrity**: Before saving, OTP is removed and a SHA-256 hash of the record is stored to provide a tamper indicator. Records can be exported to a `.doc` file for bank appraisal.
- **Service worker hook**: Registers `sw.js` if available to enable PWA install/offline caching.
- **Success/print page**: `ending.html` displays confirmation with reference number (from query string if provided), branch checklist, required documents, and print/new-application actions.

## Running locally
Open `index.html` directly in a modern browser (Chrome recommended for speech features). No build step or server is required. To print acknowledgements, navigate to `ending.html` (optionally with `?ref=REFNUMBER`).

## Notes for contributors
- The app is intentionally dependency-free; keep changes minimal and front-end only.
- New fields should be added to the `schema` to automatically inherit layout, speech, and validation behavior.
- Local data persists only in the browser; clear `localStorage` to reset saved cases.
