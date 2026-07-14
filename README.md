# Convert to Markdown

A collection of Copilot skills that convert common document formats into Markdown so their contents can be accurately analyzed, summarized, searched, or extracted from. Use these skills whenever a `.docx`, `.xlsx`, or `.pdf` file needs to be read, reviewed, compared, or processed — the conversion happens automatically so you never have to parse proprietary formats directly.

## Included Skills

| Skill | Supported formats | Script |
|---|---|---|
| [convert-word-to-md](skills/convert-word-to-md/SKILL.md) | `.docx` | `scripts/convert_word_to_md.py` |
| [convert-excel-to-md](skills/convert-excel-to-md/SKILL.md) | `.xlsx` | `scripts/convert_excel_to_md.py` |
| [convert-pdf-to-md](skills/convert-pdf-to-md/SKILL.md) | `.pdf` | `scripts/convert_pdf_to_md.py` |

## Quick Start

Tell Copilot what you need and the skill handles the rest:

```
summarize this Word document
```

```
extract the key dates from report.docx
```

```
analyze this spreadsheet and show trends
```

```
summarize all the PDFs in this folder
```

```
convert all the Word files in this folder to Markdown
```

Each skill converts the source file → Markdown first, then performs whatever analysis you asked for.

## Setup

Before the first conversion in a given environment, ensure Python 3.10+ and the required packages are installed. See each skill's `references/setup.md` for detailed step-by-step instructions, or simply:

```powershell
python -m pip install "markitdown[docx]" pymupdf
```

This installs all dependencies needed by all three skills.

## Usage

### Word (.docx)

```powershell
python skills\convert-word-to-md\scripts\convert_word_to_md.py "C:\path\to\document.docx"
python skills\convert-word-to-md\scripts\convert_word_to_md.py "C:\path\to\folder" --recursive
```

### Excel (.xlsx)

```powershell
python skills\convert-excel-to-md\scripts\convert_excel_to_md.py "C:\path\to\workbook.xlsx"
python skills\convert-excel-to-md\scripts\convert_excel_to_md.py "C:\path\to\folder" --recursive
```

### PDF (.pdf)

```powershell
python skills\convert-pdf-to-md\scripts\convert_pdf_to_md.py "C:\path\to\document.pdf"
python skills\convert-pdf-to-md\scripts\convert_pdf_to_md.py "C:\path\to\folder" --recursive
```

All scripts support `-o "C:\path\to\output_folder"` for custom output locations.

Each document produces a self-contained output folder:

```
<name>/
    img/
        img001.<ext>
        img002.<ext>
    <name>.md
```

Images are extracted as real files with relative references in the Markdown. If a document has no images, no `img/` folder is created.

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| `ModuleNotFoundError: No module named 'markitdown'` | MarkItDown not installed | `pip install "markitdown[docx]"` |
| `ModuleNotFoundError: No module named 'pymupdf'` | PyMuPDF not installed (PDF skill) | `pip install pymupdf` |
| `ERROR: Unsupported file type '.doc'` | Legacy `.doc`, not `.docx` | Ask the user to re-save as `.docx` |
| `ERROR: Unsupported file type '.xls'` | Legacy `.xls`, not `.xlsx` | Ask the user to re-save as `.xlsx` |
| `ERROR: Input path not found` | Wrong path or file moved | Confirm the correct path |

## License

MIT