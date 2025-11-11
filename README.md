# DATCOM-TFM-memoria

Master's thesis for the Master in Data Science and Computer Engineering (DATCOM) at Universidad de Granada.

## Document Structure

The document follows a clean, modular structure:

```
main.tex                    # Main document file (minimal, loads config modules)
├── config/                 # Configuration modules (modular preamble)
│   ├── packages.tex       # All package loading
│   ├── formatting.tex     # Typography and page layout
│   ├── commands.tex       # Custom commands and environments
│   ├── metadata.tex       # Document/author information
│   └── hyperref.tex       # Hyperlinks and cross-references
├── preliminares/           # Front matter (cover, title, abstract, ToC)
├── parts/                  # Main content
│   ├── parts.tex          # Master file that includes all parts
│   └── XX-name/           # Each part in its own directory
│       ├── part.tex       # Part declaration (uses \createpart command)
│       ├── chapters.tex   # Lists all chapters for this part
│       └── NN-name.tex    # Individual chapter files
├── apendices/             # Appendices (optional)
└── img/                   # Image files
```

## How to Add New Content

### Adding a New Chapter

1. Navigate to the appropriate part directory (e.g., `parts/01-context/`)
2. Create a new chapter file: `03-chapter-name.tex`
   ```latex
   % !TeX root = ../../main.tex
   % !TeX encoding = utf8
   
   \chapter{Chapter Title}\label{ch:chapter-name}
   
   Your content here...
   ```
3. Edit `chapters.tex` in that directory and add **one line**:
   ```latex
   \input{parts/01-context/03-chapter-name}
   ```

That's it! No need to touch `main.tex`.

### Adding a New Part

1. Create a new directory: `parts/03-new-part/`
2. Create `part.tex` using the custom `\createpart` command:
   ```latex
   % !TeX root = ../../main.tex
   % !TeX encoding = utf8
   
   \createpart[Optional preamble text]{Part Title}{part:label}
   ```
3. Create `chapters.tex` to list all chapters:
   ```latex
   % !TeX root = ../../main.tex
   % !TeX encoding = utf8
   
   \input{parts/03-new-part/01-first-chapter}
   ```
4. Create your first chapter: `01-first-chapter.tex`
5. Edit `parts/parts.tex` and add **two lines**:
   ```latex
   \input{parts/03-new-part/part}
   \input{parts/03-new-part/chapters}
   ```

### Adding an Appendix

1. Create files in `apendices/` directory
2. Uncomment and modify the appendix section in `main.tex`

### Editing Document Metadata

Edit `config/metadata.tex` to update:
- Author name
- Thesis title
- Advisors
- Academic year
- etc.

## Building the Document

Compile with:
```bash
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

Or use your LaTeX editor's build system.

## Key Features

### Modular Configuration
- **Separated preamble**: All LaTeX configuration split into logical modules in `config/`
- **Easy customization**: Edit one specific file instead of searching through 500+ line preambles
- **No repetition**: Custom `\createpart` command eliminates boilerplate

### Content Organization
- **Each part and chapter in its own file**: Clean separation of concerns
- **Never modify `main.tex`**: Add content by editing index files only
- **Clear structure**: Numbered directories maintain reading order
- **Proper editor integration**: All files specify `!TeX root`

### Examples of No Repetition

**Old way** (repetitive):
```latex
% In every part.tex file:
\setpartpreamble[c][0.75\linewidth]{%
    \bigskip
    Some description here
}
\part{Part Title}\label{part:label}
```

**New way** (clean):
```latex
\createpart[Some description here]{Part Title}{part:label}
```

## Configuration Files

| File | Purpose | When to Edit |
|------|---------|--------------|
| `config/packages.tex` | Package loading | Adding new packages |
| `config/formatting.tex` | Typography, page layout | Changing visual style |
| `config/commands.tex` | Custom commands | Adding new commands/environments |
| `config/metadata.tex` | Document information | Updating title, author, etc. |
| `config/hyperref.tex` | PDF links, cross-refs | Changing link colors |

## Bibliography

References are managed in `references.bib` using BibLaTeX with APA style and numeric citations.

## Archive

The `_archive/` directory contains files from previous work (not used in current document).
