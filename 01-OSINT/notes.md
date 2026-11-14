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

## Day 5: Image Steganography, Trailer Injection & Binary Extraction
## Comprehensive Reference Guide: ExifTool, Embedded Streams & Trailer Data Steganography

- **Objective:** Master foundational command-line forensics, metadata inspection, embedded data stream extraction, and trailer-injection steganography for CTF challenges and admission hackathons.
- **Environment:** Windows 11 Command Prompt (`cmd.exe`), `exiftool.exe`, and Windows built-in utility (`findstr`).
- **Target File Used:** `C:\Users\padma\Downloads\MathonGo-Diwali-Card.png`

---

### 1. Core Concepts Covered
- **Directory Navigation & Execution Prefix (`.\`):** Understanding that Windows command prompt resets to the user profile directory on launch (`C:\Users\padma`), requiring a directory shift (`cd`) to the installation path before executing binaries with the `.\` prefix.
- **Metadata Extraction:** Reading standard, surface-level attributes (file size, dimensions, modification date, MIME type) as well as specific comment tags (`-comment`, `-UserComment`, `-ImageDescription`) where metadata or author notes are often stored.
- **Embedded Stream Extraction (`-ee`):** Using ExifTool flags to scan deeper layers, multi-stream files, or hidden data pockets embedded within binary assets.
- **Trailer Injection (EOF Steganography):** Appending raw text or payloads directly after an image's official end-of-file marker (`IEND` chunk in PNG files). Because image rendering engines stop reading at `IEND`, the image displays normally while carrying hidden strings.
- **Binary String Searching (`findstr`):** Using command-line tools to scan through binary files and extract hidden text strings matching specific query patterns.

---

### 2. Step-by-Step Command Playbook

#### Step A: Directory Navigation
Always navigate to the ExifTool directory first before executing local binaries:
* **Command:** `cd C:\JEE\exiftool-13.60_64\exiftool-13.60_64`

#### Step B: Standard & Deep Metadata Inspection
* **Basic Scan:** `.\exiftool.exe C:\Users\padma\Downloads\MathonGo-Diwali-Card.png`
* **Targeted Comment Check:** `.\exiftool.exe -comment -UserComment -ImageDescription C:\Users\padma\Downloads\MathonGo-Diwali-Card.png`
* **Deep Embedded Stream Scan:** `.\exiftool.exe -ee -j C:\Users\padma\Downloads\MathonGo-Diwali-Card.png`
  * *Purpose:* Inspects hidden data layers and formats output into clean JSON for parsing.

#### Step C: Trailer Data Steganography (Injecting a Secret Message)
* **Command:** `echo "IIT_KANPUR_SECRET_FLAG{stego_test_123}" >> C:\Users\padma\Downloads\MathonGo-Diwali-Card.png`
  * *Purpose:* Appends a custom text payload directly to the binary tail of the PNG file without corrupting its layout.

#### Step D: Forensic Detection & String Extraction
* **Detection Check:** `.\exiftool.exe -ee C:\Users\padma\Downloads\MathonGo-Diwali-Card.png`
  * *Forensic Indicator:* Triggers `Warning : [minor] Trailer data after PNG IEND chunk`, proving extra payload data exists past the official end marker.
* **Extraction Search:** `findstr /I "IIT_KANPUR" C:\Users\padma\Downloads\MathonGo-Diwali-Card.png`
  * *Recovered Output:* `IIT_KANPUR_SECRET_FLAG{stego_test_123}`

---

### 3. Key Takeaways for Hackathons
- Always look for minor warnings like `Trailer data after PNG IEND chunk` in ExifTool output during file forensics.
- Trailer data injection is a fast, common way CTF challenges hide flags at the end of valid media files.
- Command-line utilities like `findstr` on Windows (or `strings` / `grep` on Linux) allow rapid recovery of hidden strings without needing heavy GUI tools.
