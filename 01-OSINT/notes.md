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

- ## Day 4: File Carving & Deep Data Streams

- **Objective:** Extract hidden text fragments, embedded files, and deep data streams from binary targets.
- **Environment:** Windows Command Prompt, directory navigation (`cd`), and binary execution (`.\exiftool.exe`).
- **Tool & Command:** `exiftool.exe -ee -j <file_path>`
- **Target Analyzed:** `MathonGo-Diwali-Card.png`
- **Key Concepts:**
  - **Embedded Stream Extraction (`-ee`):** Forces ExifTool to scan deeper layers of multi-stream files or hidden data pockets.
  - **JSON Output Formatting (`-j`):** Formats output data cleanly for programmatic parsing.
  - **Forensic Carving:** Techniques used to extract embedded payloads or hidden metadata when standard tags are omitted.
- **Takeaway:** Advanced CTF challenges frequently conceal flags inside embedded data streams rather than standard top-level metadata tags.
