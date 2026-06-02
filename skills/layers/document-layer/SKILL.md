---
name: document-layer
description: Activate this skill group when the output is a file in a specific format: Word document (.docx), PDF, PowerPoint presentation (.pptx), Excel spreadsheet (.xlsx), or when reading/extracting content from any uploaded file. Triggers include: make me a Word doc, create a presentation, build a slide deck, make a spreadsheet, read this PDF, extract from this file, fill this form, create a report as a document, pitch deck as slides, and any request where the deliverable is a downloadable file rather than inline text. Also triggers for the Allan Gray application if it needs to be submitted as a formatted document.
---

# Document Layer

This group covers all file-based output: Word, PDF, PowerPoint, Excel, and file reading. When activated, identify the right sub-skill and **read its SKILL.md before writing a single line of code** — each has environment-specific constraints that are not in general training data.

## Skill Map

### Creating Documents
- **docx** — Word documents (.docx): reports, memos, letters, templates, formatted professional documents. Use when the user explicitly wants a Word doc or a formal deliverable to send to someone.
- **pdf** — PDF creation, filling, merging, splitting, watermarking, form filling. Use for any PDF manipulation task.
- **pptx** — PowerPoint slide decks (.pptx): pitch decks, presentations, slide content from ideas or data. Use when the deliverable is slides.
- **xlsx** — Excel spreadsheets (.xlsx): financial models, data tables, formatted data, formulas. Use when the deliverable is a spreadsheet.

### Reading / Extracting from Files
- **file-reading** — router skill: tells which tool to use for each file type (PDF, docx, xlsx, csv, json, images, archives). **Read this first whenever a file has been uploaded and its content is not already visible in context.**
- **pdf-reading** — specialized PDF reading: text extraction, page rasterization, embedded images, form fields, scanned documents. Use when reading complex or multi-page PDFs.

### Frontend Documents (Web-Native)
- **frontend-design** — when a "presentation" or "report" should be a polished HTML/React artifact rather than a .pptx or .docx file. Use when the deliverable will be viewed in a browser.

## How to Use

1. **Always read the relevant SKILL.md before generating any file.** The skills encode environment-specific constraints (available libraries, rendering quirks, output paths) that directly affect whether the file works.
2. For uploaded files: read **file-reading** first to determine the correct reading strategy, then proceed.
3. Default preference: inline markdown for reports the user will read in chat; .docx only when they explicitly need a Word file; .pptx only for actual presentations.
4. All output files go to `/mnt/user-data/outputs/` and must be presented with `present_files`.

## Format Decision Guide

| Request | Use |
|---|---|
| "make me a report" | Inline markdown (not a file) |
| "Word doc / .docx / to send to someone" | docx skill |
| "slide deck / presentation / pitch" | pptx skill |
| "spreadsheet / Excel / financial model" | xlsx skill |
| "PDF / fill this form" | pdf skill |
| "read this file I uploaded" | file-reading skill first |
