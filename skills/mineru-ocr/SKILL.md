---
name: mineru-ocr
description: Use attached OcrPlane OCR MCP tools when the user uploads PDFs, images, Office files, or asks to extract text, tables, formulas, markdown, or structured OCR content.
author: ToolPlane
---

# MineRU OCR Skill

Use this skill when the user wants OCR or document understanding for PDFs,
images, DOCX, XLSX, PPTX, CSV, scanned documents, technical papers, forms,
tables, or formula-heavy documents.

## Required Tooling

Do not implement OCR in the skill. Do not run long OCR scripts from this skill.
Use the attached OcrPlane OCR MCP deployment, usually exposed as tools such as:

- `parse_document`
- `get_task_status`
- `get_markdown`
- `get_content_blocks`
- `get_full_result`
- `reprocess_task`
- `list_tasks`

If these MCP tools are not attached to the agent, explain that the OcrPlane OCR
MCP deployment is missing and ask for it to be attached.

## Authentication

Never place API keys in this skill, chat messages, or script arguments.
Authentication is handled by the OcrPlane OCR MCP deployment variables:

- `OCRPLANE_BASE_URL`
- `OCRPLANE_API_KEY`

Compatibility variables may exist for older deployments:

- `MINERU_API_BASE_URL`
- `MINERU_BASE_URL`
- `MINERU_API_KEY`

Prefer `OCRPLANE_*` for new deployments.

## Recommended Flow

1. Call `parse_document` first.
2. Prefer `file_url` for large files. Use `base64_content` only for small files.
3. For Chinese documents use `lang: "ch"`; for mixed Chinese and English use
   `lang: "ch,en"`.
4. Start with `backend: "pipeline"` for speed. Use `hybrid-auto-engine` or a VLM
   backend only when layout quality matters more than latency.
5. Keep `formula_enable` and `table_enable` enabled for papers, reports,
   invoices, and spreadsheets.
6. For large PDFs, use `start_page_id` and `end_page_id` to process sections.

## Large Result Handling

Do not request the entire OCR result unless the document is small.

- Use `get_markdown` with `offset` and `max_length` to page through markdown.
- Use `get_content_blocks` with `offset`, `limit`, and optional `page_idx` for
  structured extraction.
- Use `get_full_result` only for small documents or quick previews.

When summarizing a large document, first inspect the task summary, then fetch
only the relevant markdown ranges or content blocks.

## Output Guidance

For the user, return clean conclusions first, then cite extracted sections,
tables, page numbers, or block context when relevant. If OCR confidence seems
low, say so and suggest reprocessing with a different backend or selected page
range.

