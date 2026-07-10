# Convert Word to Markdown

A Copilot skill that converts Word (`.docx`) documents into Markdown so their contents can be accurately analyzed, summarized, searched, or extracted from. Use this skill whenever a `.docx` file needs to be read, reviewed, compared, or processed — the conversion happens automatically so you never have to parse `.docx` XML directly.

## Quick Start

Tell Copilot what you need and the skill handles the rest:

```
summarize this Word document
```

```
extract the key dates from report.docx
```

```
convert all the Word files in this folder to Markdown
```

The skill converts `.docx` → Markdown first, then performs whatever analysis you asked for.

## Setup

Before the first conversion in a given environment, ensure Python 3.10+ and the `markitdown` package are installed. See [`skills/convert-word-to-md/references/setup.md`](skills/convert-word-to-md/references/setup.md) for step-by-step instructions, or simply:

```powershell
python -m pip install "markitdown[docx]"
```

## Usage

**Single file:**

```powershell
python skills\convert-word-to-md\scripts\convert_word_to_md.py "C:\path\to\document.docx"
```

**Custom output location:**

```powershell
python skills\convert-word-to-md\scripts\convert_word_to_md.py "C:\path\to\document.docx" -o "C:\path\to\output_folder"
```

**Batch — all `.docx` files in a folder:**

```powershell
python skills\convert-word-to-md\scripts\convert_word_to_md.py "C:\path\to\folder"
```

**Batch — include subfolders:**

```powershell
python skills\convert-word-to-md\scripts\convert_word_to_md.py "C:\path\to\folder" --recursive
```

Each `.docx` produces a self-contained output folder:

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
| `ModuleNotFoundError: No module named 'markitdown'` | MarkItDown not installed | Follow [`references/setup.md`](skills/convert-word-to-md/references/setup.md) |
| `ERROR: Unsupported file type '.doc'` | Legacy `.doc`, not `.docx` | Ask the user to re-save as `.docx` |
| `ERROR: Input path not found` | Wrong path or file moved | Confirm the correct path |

## License

MIT