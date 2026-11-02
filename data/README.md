# Data

## raw/

The year-end revenue reports, exactly as downloaded from the City of Boulder's records portal. Never edited.

| File | Document ID | Downloaded | Bytes |
|---|---|---|---|
| revenue-2018.pdf | 194398 | 2026-10-19 | 617,609 |
| revenue-2019.pdf | 194399 | 2026-10-19 | 629,675 |
| revenue-2020.pdf | 194400 | 2026-10-19 | 1,322,800 |
| revenue-2021-12.pdf | | | |
| revenue-2022-12.pdf | | | |
| revenue-2023-12.pdf | | | |
| revenue-2024-12.pdf | 194397 | | |

The 2018–2020 reports were downloaded on October 19, 2026, during the Chapter 9 exercise (saved then as boulder-revenue-2018.pdf, -2019.pdf, and -2020.pdf), and copied here under new names, so they don't appear in download-log.csv.

`01_collection.ipynb` writes `download-log.csv` here with the ID, date, and size of every file it downloads.

## processed/

Tables extracted from the PDFs. For each one, record which pages and which tool (pypdf, pdfplumber, or OCR) it came from.

## Known issues

- Some reports draw their marijuana charts as images, which need OCR.
- A year can be printed in two reports; the later printing may be a restatement.
