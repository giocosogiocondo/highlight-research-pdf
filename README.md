<img width="2172" height="603" alt="banner" src="https://github.com/user-attachments/assets/0bd25ce3-9bfd-4d55-92ec-bc39dbd06022" />

> **My professor wants a literature review. GTA 6 wants my evening.**<br>
> Close the AI chat. The highlights stay in the paper.

## What it does

Give Codex or Claude Code a research paper. The skill picks full sentences from the original text and saves a PDF copy with embedded highlights. Your source PDF stays intact.

| Color | What it marks |
| :--- | :--- |
| **🟨&nbsp;Yellow** | The sentence that best captures the point of a substantive paragraph. |
| **🟩&nbsp;Green** | Sentences that state a **Problem Statement**, **Research Gap**, **Research Question**, **Methodology**, **Results**, **Contribution to Knowledge**, or **Practical Significance**. |

If a paragraph's key sentence also serves a research role, it gets a single green highlight.

### Before and after

The same page before and after highlighting. Select either image to see it at full size.

| Before · Original PDF | After · Annotated PDF |
| :---: | :---: |
| <img width="629" height="891" alt="before" src="https://github.com/user-attachments/assets/d8dc3f48-1020-4052-a82c-ebca2800114a" /> | <img width="629" height="895" alt="after" src="https://github.com/user-attachments/assets/630a6f42-7831-4bd9-9b42-5a1850d2fd00" />|

## Read and take notes in Zotero

1. **Highlight.** Ask Codex or Claude Code to highlight the paper and save an annotated PDF copy.
2. **Import.** Attach the copy to the paper's Zotero entry and open it in the Zotero PDF reader. Choose **File → Import Annotations…** to make the highlights editable in Zotero. [Zotero documentation](https://www.zotero.org/support/kb/annotations_in_database#interacting_with_embedded_annotations)
3. **Read with Notes open.** Use the left Annotations pane to jump to a passage and the right Notes pane to write as you read. Drag a highlight into your note to keep a link to the passage. Then write your own take, such as how the authors' evidence supports the claim or where you would use it in your review. [Zotero PDF Reader and Note Editor](https://www.zotero.org/support/pdf_reader)

<img width="1919" height="1030" alt="zotero-reading" src="https://github.com/user-attachments/assets/2005628f-c4d2-46e6-8785-445c92eb3507" />


*A reading setup with annotations on the left, the paper in the middle, and notes on the right.*

## Install in Codex

With Git and Python installed, run these commands in PowerShell, Git Bash, or a macOS/Linux shell. Install PyMuPDF in the Python environment that will run the annotation script.

```sh
git clone https://github.com/giocosogiocondo/highlight-research-pdf.git "$HOME/.agents/skills/highlight-research-pdf"
python -m pip install -r "$HOME/.agents/skills/highlight-research-pdf/requirements.txt"
```

Attach the PDF in Codex and try this prompt.

> Use `$highlight-research-pdf` to highlight this paper and save an annotated PDF copy.

See the [Codex skill documentation](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills) for project-scoped installation.

## Install in Claude Code

With Git and Python installed, run these commands in PowerShell, Git Bash, or a macOS/Linux shell. Install PyMuPDF in the Python environment that will run the annotation script.

```sh
git clone https://github.com/giocosogiocondo/highlight-research-pdf.git "$HOME/.claude/skills/highlight-research-pdf"
python -m pip install -r "$HOME/.claude/skills/highlight-research-pdf/requirements.txt"
```

Start Claude Code in the folder with the PDF and try this prompt, or ask in plain words and Claude Code loads the skill on its own.

> /highlight-research-pdf Highlight paper.pdf and save an annotated PDF copy.

For project-scoped installation, clone into `.claude/skills/highlight-research-pdf` inside the project instead. See the [Claude Code skills documentation](https://docs.claude.com/en/docs/claude-code/skills).

## Apply your own selections

The [annotation script](scripts/annotate.py) takes reviewed excerpts from a PDF with horizontal, selectable text. Use one-based PDF page numbers and exact excerpts in a UTF-8 `selections.json` file. Omit `roles` for yellow, or use the exact English role names above for green.

```json
[
  {"page": 1, "text": "The exact sentence selected from the PDF."},
  {"page": 2, "text": "The exact sentence that states the research gap.", "roles": ["Research Gap"]}
]
```

Run this command from the skill folder.

```sh
python scripts/annotate.py input.pdf selections.json highlighted.pdf
```

Choose a new output filename. For scans and rotated text, see the OCR and layout guidance in [SKILL.md](SKILL.md).
