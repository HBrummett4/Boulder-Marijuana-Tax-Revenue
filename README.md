# Boulder Marijuana Tax Revenue, 2017–2024

Houston Brummett

Final Project for INFO 4617 Web Data Science, CU Boulder, Fall 2026.

## Research question

How did the City of Boulder's marijuana tax revenue change from 2018 to 2024, and did its share of the city's total sales and use tax rise or fall over those years?

## Data source

The year-end revenue reports in the [Revenue Reports folder](https://documents.bouldercolorado.gov/WebLink/Browse.aspx?id=194345&dbid=0&repo=LF8PROD2) of the City of Boulder's records portal, published as PDFs by the Finance Department.

| Report | Portal location | Document ID |
|---|---|---|
| Revenue Report 2018 | Revenue Reports folder | 194398 |
| Revenue Report 2019 | Revenue Reports folder | 194399 |
| Revenue Report 2020 | Revenue Reports folder | 194400 |
| December 2021 report | 2021 folder (194346) | found by `01_collection.ipynb` |
| December 2022 report | 2022 folder (194359) | found by `01_collection.ipynb` |
| December 2023 report | 2023 folder (194372) | found by `01_collection.ipynb` |
| Revenue Report 2024.12 | 2024 folder (194385) | 194397 |

Each report covers its year and the year before, so the series runs from 2017 to 2024.

## Method

- **Finding the files (Chapter 8, dynamic pages):** the portal's folder pages are filled in by JavaScript; the notebook requests the same JSON listing the page uses (`FolderListingService.aspx/GetFolderListing2`).
- **Reading the files (Chapter 9, PDFs):** pypdf and pdfplumber for pages with a text layer, and Tesseract OCR for charts that are images.
- **Analysis:** marijuana revenue by year and type, its change from the year before, and its share of total sales and use tax.

## Repository layout

```
├── README.md            # this file
├── environment.yml      # the Python packages and versions this project uses
├── .gitignore           # keeps keys and temporary files out of the repository
├── data/
│   ├── raw/             # the PDFs as downloaded; never edited
│   ├── processed/       # tables extracted from the PDFs
│   └── README.md        # where each file came from and when
├── notebooks/
│   └── 01_collection.ipynb
├── scripts/
└── output/
    ├── figures/
    └── tables/
```

## Setup

From Anaconda Prompt, in this folder:

```
conda env create -f environment.yml
conda activate boulder-revenue
jupyter notebook
```

Start Jupyter from the activated prompt, so Tesseract can find its DLLs and language files. The notebooks also need `boulder-ca-bundle.pem`, the certificate bundle from Chapter 9, saved in `data/`.

## Collection rules

- Every request sends a User-Agent with a contact address.
- 30 seconds between requests, and each file is downloaded once; later runs read the saved copy.
- About 11 requests in all. Chapter 9 reports that the portal stopped answering after 13 to 17 requests in a row on October 6, 2026.
- Certificates are checked with the bundle; verification is never turned off.
- [robots.txt and the portal's terms: state what they say once checked.]

## Personal information

The figures are citywide totals with no taxpayer names. Report covers can name city staff with contact details; those are left out of the dataset.

## AI assistance

Claude helped draft the proposal, this README, and the starter collection notebook.
