# Skill Seekers - Simple Usage Guide

**TL;DR:** Turn any documentation, GitHub repo, or PDF into a Claude skill you can upload.

---

## What This Tool Does

```
Documentation Website  ──┐
GitHub Repository      ──┼──►  [Skill Seekers]  ──►  .zip file  ──►  Upload to Claude
PDF Manual             ──┘
```

Claude then becomes an expert on that topic.

---

## Installation (Windows)

```powershell
pip install skill-seekers
```

Done. Verify with:
```powershell
skill-seekers --help
```

---

## The 4 Main Commands You'll Use

| Command | What It Does |
|---------|--------------|
| `skill-seekers scrape` | Scrape a documentation website |
| `skill-seekers github` | Scrape a GitHub repository |
| `skill-seekers pdf` | Extract content from a PDF |
| `skill-seekers package` | Create .zip file to upload |

---

## Quick Start Examples

### Example 1: Scrape a Docs Website

```powershell
# Scrape React docs
skill-seekers scrape --name react --url https://react.dev/

# Package it
skill-seekers package output/react/

# Upload output/react.zip to https://claude.ai/skills
```

### Example 2: Scrape a GitHub Repo

```powershell
# Scrape FastAPI repo
skill-seekers github --repo tiangolo/fastapi

# Package it
skill-seekers package output/fastapi/
```

### Example 3: Extract from PDF

```powershell
# Extract from a PDF manual
skill-seekers pdf --pdf "C:\Docs\manual.pdf" --name mymanual

# Package it
skill-seekers package output/mymanual/
```

---

## Complete Workflow (Step by Step)

### Step 1: Create a Skills Folder

```powershell
mkdir C:\Skills
cd C:\Skills
```

### Step 2: Scrape Something

Pick one:

```powershell
# Option A: Documentation website
skill-seekers scrape --name vue --url https://vuejs.org/guide/

# Option B: GitHub repo
skill-seekers github --repo pallets/flask

# Option C: PDF file
skill-seekers pdf --pdf "C:\path\to\doc.pdf" --name mydoc
```

### Step 3: (Optional) Enhance with AI

Makes the skill much better - Claude rewrites SKILL.md with real examples:

```powershell
skill-seekers-enhance output/vue/ --interactive-enhancement
```

A new PowerShell window opens with Claude Code. Wait for it to finish.

### Step 4: Package

```powershell
skill-seekers package output/vue/
```

Creates: `output/vue.zip`

### Step 5: Upload to Claude

1. Go to https://claude.ai/skills
2. Click "Upload Skill"
3. Select `output/vue.zip`
4. Done!

---

## Using Config Files (For Repeated Use)

Instead of typing long commands, create a config file:

### Create Config

Save as `C:\Skills\configs\react.json`:
```json
{
  "name": "react",
  "description": "React framework for building UIs",
  "base_url": "https://react.dev/",
  "max_pages": 200,
  "rate_limit": 0.5
}
```

### Use Config

```powershell
skill-seekers scrape --config configs/react.json
```

---

## Preset Configs (Ready to Use)

Skill Seekers comes with preset configs. Download them:

```powershell
# Clone the repo to get configs
git clone https://github.com/yusufkaraaslan/Skill_Seekers.git
cd Skill_Seekers

# Use a preset
skill-seekers scrape --config configs/react.json
skill-seekers scrape --config configs/django.json
skill-seekers scrape --config configs/godot.json
```

---

## Common Options

### Scrape Command Options

```powershell
# Basic
skill-seekers scrape --name <name> --url <url>

# With config file
skill-seekers scrape --config configs/myconfig.json

# Faster (async mode)
skill-seekers scrape --config configs/react.json --async --workers 8

# Skip re-scraping (use cached data)
skill-seekers scrape --config configs/react.json --skip-scrape
```

### GitHub Command Options

```powershell
# Basic
skill-seekers github --repo owner/repo

# With more data
skill-seekers github --repo owner/repo --include-issues --include-changelog --include-releases

# With code analysis (extracts function signatures)
skill-seekers github --repo owner/repo --include-code
```

### PDF Command Options

```powershell
# Basic
skill-seekers pdf --pdf file.pdf --name myskill

# With table extraction
skill-seekers pdf --pdf file.pdf --name myskill --extract-tables

# With OCR (for scanned PDFs)
skill-seekers pdf --pdf file.pdf --name myskill --ocr

# Faster (parallel processing)
skill-seekers pdf --pdf file.pdf --name myskill --parallel --workers 8
```

---

## Enhancement (Making Skills Better)

After scraping, you can enhance the SKILL.md file with AI:

```powershell
# Opens a new terminal with Claude Code
skill-seekers-enhance output/react/ --interactive-enhancement
```

**What it does:**
- Reads all the scraped documentation
- Rewrites SKILL.md with real code examples
- Adds quick reference patterns
- Makes the skill much more useful

**Requires:** Claude Code CLI installed (`claude --version`)

---

## Output Structure

After scraping, you get:

```
output/
├── react_data/          # Raw scraped data (cached)
│   └── pages/           # JSON files for each page
├── react/               # The skill
│   ├── SKILL.md         # Main skill file (Claude reads this first)
│   └── references/      # Organized documentation
│       ├── index.md
│       ├── getting_started.md
│       ├── api.md
│       └── ...
└── react.zip            # Packaged skill (after running package)
```

---

## Troubleshooting

### "No content extracted"

The CSS selector didn't match. Try a different docs site or use a preset config.

### "Rate limited" or slow

Add `--rate-limit 1.0` to wait longer between requests.

### "claude command not found" during enhancement

Make sure Claude Code CLI is installed: https://claude.ai/code

### Enhancement opens wrong terminal

Set your preferred shell:
```powershell
$env:SKILL_SEEKER_TERMINAL = "pwsh"
```

---

## Cheat Sheet

```powershell
# === SCRAPING ===
skill-seekers scrape --name X --url URL           # Scrape docs
skill-seekers github --repo owner/repo            # Scrape GitHub
skill-seekers pdf --pdf file.pdf --name X         # Extract PDF

# === ENHANCE (optional but recommended) ===
skill-seekers-enhance output/X/ --interactive-enhancement

# === PACKAGE ===
skill-seekers package output/X/                   # Creates X.zip

# === UPLOAD ===
# Go to https://claude.ai/skills and upload the .zip
```

---

## Tips

1. **Start small** - Test with `--max-pages 20` first
2. **Use enhancement** - It makes skills 10x better
3. **Check output** - Look at SKILL.md before packaging
4. **Use presets** - Clone the repo to get working configs
5. **GitHub token** - Set `$env:GITHUB_TOKEN` for higher rate limits

---

## Need Help?

- Full docs: https://github.com/yusufkaraaslan/Skill_Seekers
- Issues: https://github.com/yusufkaraaslan/Skill_Seekers/issues

---

*Guide created for Windows users. Commands work in PowerShell.*
