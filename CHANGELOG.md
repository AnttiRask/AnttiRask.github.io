# GitHub Repos Cleanup & Portfolio Setup - January 2026

This document records the changes made during a comprehensive GitHub repository cleanup and portfolio setup session.

## Overview

- Analyzed 107 GitHub repositories
- Archived 59 repositories
- Deleted 3 repositories
- Created GitHub Pages sites for portfolio and key projects
- Established consistent branding across all sites

---

## Repository Cleanup

### Archived Repositories (59 total)
Repositories that were forked for learning or no longer actively maintained were archived to reduce clutter while preserving history.

### Deleted Repositories (3 total)
- BiblioStatus-related test/duplicate repos (deleted via GitHub GUI due to permission requirements)

---

## GitHub Pages Sites Created

### 1. Main Portfolio (AnttiRask.github.io)
- **Location**: https://anttirask.github.io/
- **Source**: `/docs` folder in `AnttiRask.github.io` repo
- **Features**:
  - youcanbeapiRate banner image
  - Featured Projects section with badges (Book, App, R Package)
  - Learning Resources section
  - Other Projects section
  - Skills overview
  - Links to GitHub, LinkedIn, Substack

### 2. BiblioStatus
- **Location**: https://anttirask.github.io/BiblioStatus/
- **Source**: `/docs/index.html`
- **Features**:
  - Hero section with app description
  - Screenshot from repo
  - Features grid
  - Tech stack display
  - How It Works steps
  - Data Source (Kirkanta API) section

### 3. TuneTeller (formerly music_recommender)
- **Location**: https://anttirask.github.io/TuneTeller/
- **Source**: `/docs/index.html` and `/docs/screenshot.png`
- **Features**:
  - Dark theme (kept for music app aesthetic)
  - Hero with app description
  - Screenshot
  - How It Works steps
  - Features grid
  - Tech stack and API info
- **Note**: Repo was renamed from `music_recommender` to `TuneTeller`

### 4. col2hex2col (pkgdown site)
- **Location**: https://anttirask.github.io/col2hex2col/
- **Source**: Auto-generated via pkgdown GitHub Action, deployed to `gh-pages` branch
- **Configuration**: `_pkgdown.yml` with flatly theme
- **Logo**: Moved from `img/hex-col2hex2col.png` to `man/figures/logo.png` (pkgdown convention)

---

## Branding - youcanbeapiRate Color Scheme

All GitHub Pages sites were updated to use consistent branding:

```css
--primary: #C1272D;      /* Red - accent color */
--primary-dark: #a02025; /* Darker red for hover states */
--black: #000000;        /* Text color */
--white: #ffffff;        /* Background */
--gray: #B2B2B2;         /* Borders, secondary elements */
```

**Banner image**: Twitter Cover A.png from `/Dropbox/Kuvat/youcanbeapiRate/Final/`

---

## col2hex2col Package Updates

### pkgdown Setup
- Added `.github/workflows/pkgdown.yaml` for automated documentation builds
- Created `_pkgdown.yml` with:
  - Bootstrap 5 + flatly theme
  - Organized function reference (Color Conversion, Color Data)
  - Author link to portfolio

### Logo Fix
- **Problem**: Logo referenced `img/hex-col2hex2col.png` but pkgdown expects `man/figures/logo.png`
- **Solution**: Copied logo to `man/figures/logo.png` and updated README

### R-CMD-check Workflow
- **Problem**: macOS runner failing due to transient xml2 download issues
- **Solution**: Temporarily removed macOS from test matrix
- **File**: `.github/workflows/R-CMD-check.yaml`
- **Note for CRAN**: Re-add macOS before CRAN submission, or use `rhub::check_for_cran()` for pre-submission checks. CRAN runs their own macOS tests anyway.

Current matrix:
```yaml
config:
  - {os: windows-latest, r: 'release'}
  - {os: ubuntu-latest,  r: 'devel', http-user-agent: 'release'}
  - {os: ubuntu-latest,  r: 'release'}
  - {os: ubuntu-latest,  r: 'oldrel-1'}
```

---

## TuneTeller Updates

### Repo Rename
- Renamed from `music_recommender` to `TuneTeller`
- Had to delete a private `TuneTeller` repo first (done via GitHub GUI)
- Local folder still named `music_recommender` - consider renaming locally too

### README
- Added comprehensive README with:
  - Features list
  - Screenshot
  - Project structure
  - How It Works explanation
  - API keys documentation
  - Local development instructions
  - Tech stack table

### GitHub Pages
- Created `/docs/index.html` with dark Spotify-inspired theme
- Screenshot copied to `/docs/screenshot.png` (GitHub Pages serves from /docs as root)

---

## Files Modified/Created

### AnttiRask.github.io
- `index.html` - Main portfolio page
- `img/banner.png` - youcanbeapiRate banner

### BiblioStatus
- `docs/index.html` - Landing page

### TuneTeller (music_recommender folder locally)
- `README.md` - Comprehensive project README
- `docs/index.html` - GitHub Pages landing page
- `docs/screenshot.png` - App screenshot
- `img/screenshot.png` - Screenshot for README

### col2hex2col
- `_pkgdown.yml` - pkgdown configuration
- `.github/workflows/pkgdown.yaml` - pkgdown build workflow
- `.github/workflows/R-CMD-check.yaml` - Removed macOS from matrix
- `man/figures/logo.png` - Logo in pkgdown-expected location
- `README.md` - Updated logo path

---

## Pending/Future Tasks

1. **Branch protection for col2hex2col**: Optional - can be enabled in GitHub Settings > Branches if desired
2. **Re-add macOS to R-CMD-check**: Consider before CRAN submission
3. **Rename local folder**: `music_recommender` → `TuneTeller` for consistency
4. **ggplot2-extended-book**: Skipped GitHub Pages setup as it already has dedicated domain (ggplot2-extended-book.com)

---

## Commands Reference

### Archive a repo
```bash
gh repo archive AnttiRask/repo-name
```

### Delete a repo (requires delete_repo scope)
```bash
gh auth refresh -h github.com -s delete_repo
gh repo delete AnttiRask/repo-name --yes
```

### Rename a repo
```bash
gh repo rename new-name -R AnttiRask/old-name
```

### Re-run failed workflow
```bash
gh run rerun <run-id> -R AnttiRask/repo-name --failed
```

### Check workflow status
```bash
gh run list -R AnttiRask/repo-name --limit 5
```
