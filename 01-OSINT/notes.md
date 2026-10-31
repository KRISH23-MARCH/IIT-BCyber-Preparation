# Day 2: OSINT & Google Dorking

- **Date:** Day 2
- **Focus:** Reconnaissance & Search Operators

## Key Concepts
- OSINT relies entirely on legal, publicly available data.
- Google Dorking uses advanced operators to pinpoint specific files or directories.

## Operators Tested Today
- `site:` - Limits results to a target domain.
- `filetype:` - Searches for specific file formats (e.g., pdf, txt).
- `intitle:` - Targets text appearing in the browser tab title.
- `inurl:` - Searches for web pages where the specific keyword appears inside the website's URL address.
- 'intext:'-Looks for specific words or phrases inside the actual body text of the web page, ignoring titles and URLs.
- 'ext'-Works just like filetype:, targeting specific file extensions.

## Day 3: Metadata Extraction & Analysis

- **Objective:** Extract and analyze hidden file metadata using ExifTool via Windows Command Prompt.
- **Environment:** Windows Command Prompt, directory navigation (`cd`), and executing binaries using the `.\` syntax.
- **Tool Used:** `exiftool.exe` (Version 13.60)
- **Target Analyzed:** `MathonGo-Diwali-Card.png`
- **Key Findings:**
  - **File Type & MIME:** PNG image (`image/png`), 8-bit RGB with Alpha.
  - **Dimensions:** 1080x1350 pixels (1.5 Megapixels).
  - **Timestamps:** Successfully captured file creation, modification, and access times.
- **Key Takeaway:** Metadata analysis is a vital reconnaissance technique that reveals file specifications, underlying properties, and historical timestamps.
