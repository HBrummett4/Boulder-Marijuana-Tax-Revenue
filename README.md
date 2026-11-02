# Boulder Marijuana Tax Revenue, 2017–2024

Houston [last name] · Partner: [name, or remove this line]

Final Project for INFO 4617 Web Data Science, CU Boulder, Fall 2026.

This project asks how the City of Boulder's marijuana tax revenue changed from 2018 to 2024, and whether its share of the city's total sales and use tax rose or fell over those years. The answer comes from the Finance Department's year-end revenue reports, published as PDFs in the city's public records portal, which present one year at a time; this project builds them into one series. City Council and the Finance Department set Boulder's marijuana taxes, and a multi-year series shows how much of the budget depends on one industry. The full plan is in [proposal.md](proposal.md).

## Data

Seven year-end revenue reports, 2018 through December 2024, from the [Revenue Reports folder](https://documents.bouldercolorado.gov/WebLink/Browse.aspx?id=194345&dbid=0&repo=LF8PROD2) of the City of Boulder's records portal. Each report covers its year and the year before, so the series runs from 2017 to 2024.

| Report | Document ID |
|---|---|
| Revenue Report 2018 | 194398 |
| Revenue Report 2019 | 194399 |
| Revenue Report 2020 | 194400 |
| Revenue Report 2021.12 | 194358 |
| Revenue Report 2022.12 | 194371 |
| Revenue Report 2023.12 | 194384 |
| Revenue Report 2024.12 | 194397 |

The PDFs are in [`data/raw/`](data/raw/), and [`data/README.md`](data/README.md) records when each was downloaded and its size. The figures are citywide totals with no taxpayer names; staff contact details printed on report covers are left out of the dataset.

## Methods

- **Collection** ([`notebooks/01_collection.ipynb`](notebooks/01_collection.ipynb)): requests the portal's JSON folder listing, as the folder page does (Chapter 8), to find each report's ID, then downloads each report once, with an identifying User-Agent and 30 seconds between requests.
- **Extraction** (to come): pypdf and pdfplumber for pages with a text layer, and Tesseract OCR for charts that are images (Chapter 9).
- **Analysis** (to come): marijuana revenue by year and type, its change from the year before, and its share of total sales and use tax.

## Findings

To come.

## How to reproduce

1. Create the environment and start Jupyter from Anaconda Prompt, in this folder:

   ```
   conda env create -f environment.yml
   conda activate boulder-revenue
   jupyter notebook
   ```

   Start Jupyter from the activated prompt, so Tesseract can find its DLLs and language files.
2. Save `boulder-ca-bundle.pem`, the certificate bundle from Chapter 9 of *Web Data Science*, in `data/`.
3. Put your email address in `HEADERS` in `notebooks/01_collection.ipynb`, and run it. Files already in `data/raw/` are not downloaded again.

## AI assistance

Claude helped draft the proposal, this README, and the starter collection notebook.
