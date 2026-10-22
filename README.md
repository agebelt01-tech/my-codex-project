# AGEROLL PDF Editor

A private, browser-based PDF text editor using the AGEROLL branding and red palette. Upload a PDF, select an editable text area, change its words, review the live preview, and download the edited document. An interactive sample is included.

## Technologies

TanStack Start, React, TypeScript, Vite, PDF.js for rendering and text recognition, pdf-lib for editing existing PDF content streams, and Lucide icons. The app deploys on Netlify. PDF.js font, CMap, and WASM resources are served from the same origin.

## Local development

Use Node 22.13+ and pnpm.

```sh
pnpm install
pnpm dev
```

Open the address shown by Vite. `pnpm build` creates the production site; Netlify runs the configured build automatically.

## How editing works

The editor replaces only selected text-showing instructions in the original PDF stream. It reuses the existing font, size, color, and text positioning rather than covering the original text with a white rectangle. Advance compensation retains the following text's position. Untouched page instructions remain intact. An unchanged download returns the original file bytes.

The editor supports text that maps safely between PDF.js recognition and the PDF's original font encoding. Standard Latin fonts, WinAnsi fonts with usable widths, and embedded fonts with supported Unicode maps are handled. Characters absent from an embedded font are rejected instead of replaced with a fallback font. Replacement text is single-line; longer text can overlap nearby content and should be reviewed in the preview.

Scanned pages need OCR, which is not included. Complex layouts that merge multiple text operations, rotated text, shared form objects, custom CID encodings, inline-image streams, and unsupported fonts remain protected. Password-protected files must be unlocked first. This is a PDF text editor, not a universal PDF reconstruction tool.

Files and edits remain in browser memory for the current session. There are no document uploads, database writes, accounts, or external document processing services. Download your work before closing or refreshing. The interface's typefaces load from Google Fonts; PDF content never goes there.

When updating PDF.js, refresh `public/pdf-assets/{cmaps,standard_fonts,wasm}` from the installed package to keep resources compatible with the bundled worker.
