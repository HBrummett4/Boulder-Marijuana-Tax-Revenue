# Data

## raw/

The year-end revenue reports, exactly as downloaded from the City of Boulder's records portal. Never edited.

| File | Document ID | Downloaded | Bytes |
|---|---|---|---|
| revenue-2018.pdf | 194398 | | |
| revenue-2019.pdf | 194399 | | |
| revenue-2020.pdf | 194400 | | |
| revenue-2021-12.pdf | | | |
| revenue-2022-12.pdf | | | |
| revenue-2023-12.pdf | | | |
| revenue-2024-12.pdf | 194397 | | |

`01_collection.ipynb` writes `download-log.csv` here with the ID, date, and size of every file it downloads.

## processed/

Tables extracted from the PDFs. For each one, record which pages and which tool (pypdf, pdfplumber, or OCR) it came from.

## Known issues

- Some reports draw their marijuana charts as images, which need OCR.
- A year can be printed in two reports; the later printing may be a restatement.
