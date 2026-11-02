# Final Project Proposal

Houston Brummett

## 1. Research question

**How did the City of Boulder's marijuana tax revenue change from 2018 to 2024, and did its share of the city's total sales and use tax rise or fall over those years?**

The answer is a yearly dollar figure and a yearly percentage, so it can take many values. It comes entirely from web data: the Finance Department's revenue reports, published as PDFs in the city's public records portal.

**Who would care.** Boulder City Council and the Finance Department set the city's marijuana taxes. The 2020 report lists three of them: the base 3.86% sales and use tax, an additional 3.50% tax on recreational marijuana, and a 5.0% excise tax on transfers from cultivation facilities. A multi-year series shows council how much of the budget depends on one industry before it changes a rate. The *Boulder Daily Camera* could use the same series to report on what legal marijuana brings the city, since the reports themselves present one year at a time.

**What I expect.** I expect marijuana revenue to have grown through 2020 and 2021 and then fallen, while total sales and use tax kept rising: Chapter 9's case study shows the total climbing from \$135.2 million in 2020 to \$175.5 million in 2023. If so, marijuana's share of the total shrank after 2021.

**What would surprise me.** If marijuana revenue kept growing as fast as the total through 2024, or if it fell before 2020 rather than after, my expectation was wrong.

## 2. Data source and method

**Source.** The year-end revenue reports in the [Revenue Reports folder](https://documents.bouldercolorado.gov/WebLink/Browse.aspx?id=194345&dbid=0&repo=LF8PROD2) of Boulder's records portal, which runs Laserfiche WebLink. Each report is downloaded from `https://documents.bouldercolorado.gov/WebLink/ElectronicFile.aspx?docid=<id>&dbid=0&repo=LF8PROD2`.

**How I will get it.**

- **Dynamic pages (Chapter 8).** The folder page is filled in by JavaScript. I request its JSON listing from `FolderListingService.aspx/GetFolderListing2`, as Chapter 9 does, to find each report's document ID. The 2018, 2019, and 2020 reports sit at the top of the folder (IDs 194398–194400). The 2021–2024 year folders each hold twelve monthly reports; the December reports are 194358, 194371, 194384, and 194397.
- **PDFs (Chapter 9).** pypdf and pdfplumber for pages with a text layer, and Tesseract OCR for marijuana charts that are images. In my Chapter 9 work, the 2018 and 2019 marijuana pages had little text, while the 2020 report drew its chart labels as text.

**Scope.** Seven year-end reports, 2018 through December 2024, about 100 pages in all (the three I downloaded first run 14–16 pages). Each report covers its year and the year before, so the series runs from 2017 to 2024: eight years. This is a one-time collection, not collection over time.

**Analysis.**

1. A table of marijuana revenue by year and by type (medical sales tax, recreational sales tax, excise tax, and the state's share-back payment), using each year's latest printing, as Chapter 9's case study does.
2. A line chart of total marijuana revenue by year, 2017–2024, with the change from the year before.
3. Marijuana revenue as a percentage of total sales and use tax each year, which answers the second half of the question.
4. A check: for each year printed in two reports, compare the two figures and note any restatement.

## 3. Ethics and feasibility

**Terms of service and robots.txt.** The reports are public records that the city publishes for anyone to download. [Check `https://documents.bouldercolorado.gov/robots.txt` and the portal's terms or disclaimer page, and state here what they say about `/WebLink/` and automated access.] I stay within limits by sending a User-Agent that identifies me, pausing 30 seconds between requests, and saving every file so it is downloaded once. On October 6, 2026, the server stopped answering after 13 to 17 requests in a row (Chapter 9); my collection took eight requests, four folder listings and four downloads, since I already had the 2018–2020 reports from Chapter 9. I check the certificate with the bundle Chapter 9 provides and never turn verification off.

**Personal information.** The figures are citywide totals, so the data holds no taxpayer names. The 2018 report's cover names a city staff member with an email address and phone number; I will leave contact details like these out of my dataset.

**One record, retrieved.** On November 1, 2026, `notebooks/01_collection.ipynb` downloaded the December 2021 report with this request:

```python
url = PORTAL + "ElectronicFile.aspx?docid=194358&dbid=0&repo=LF8PROD2"
response = requests.get(url, headers=HEADERS, timeout=120, verify=BUNDLE)
response.raise_for_status()
```

It returned status 200 and a 913,457-byte PDF that began with `%PDF-`.

For a record's content, page 9 of the 2020 report, downloaded the same way during my Chapter 9 exercise, is the marijuana section. Its text begins:

> Marijuana Tax Revenues. The City of Boulder collects revenue from the sale of both medical and recreational marijuana. The City collects the base 3.86% sales and use tax on medical and recreational marijuana.

Its first dollar amounts, read with pypdf from the labels of Charts 8 and 9, were `$892,122`, `$302,165`, `$2,288,916`, `$3,064,306`, `$664,193`, and `$394,371`.

Fields I will use: report year, revenue type (medical sales tax, recreational sales tax, excise tax, state share-back), dollar amount, and the page it came from.

**Biggest risk and fallback.** The biggest risk is that some years' marijuana charts are images whose labels OCR misreads, or that a later report drops the marijuana section. My fallback is a smaller window: 2019–2020 from the 2020 report, whose chart labels pypdf already reads as text, plus any later years whose pages have a text layer. A second fallback is the total marijuana figure alone, without the breakdown by type, which needs one number per year. The portal also holds monthly reports for 2021–2024, a second source if a year-end report lacks the section.
