# MCC Faculty Records

A read-only, searchable directory linked to your Google spreadsheet. No build tools, API keys, or paid services required. All CSS and JavaScript are inside `index.html`.

## Publish on GitHub Pages

1. Extract this ZIP on your computer.
2. Create a GitHub repository, or open the repository where you want this directory.
3. Upload `index.html` to the repository root and commit it. You can also upload this README.
4. In the repository, open **Settings → Pages**.
5. Under **Build and deployment**, select **Deploy from a branch**, then **main** and **/(root)**. Save.
6. Open the website address GitHub displays when publishing finishes.

If adding this to an existing website, put `index.html` in a folder such as `faculty-records` and visit that folder's URL. Do not overwrite an existing homepage unless you intend to replace it.

## Two views, two direct links

The navigation switches between both datasets. Each view can also be linked separately:

- `https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/#current-pgps`
- `https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/#tof-completions`

The page keeps separate search, sorting, and pagination choices for each view while it remains open. Reloading starts a new session.

## Connection and updates

The source is preconfigured:

https://docs.google.com/spreadsheets/d/1eq7OWemYOStTBW57HF1N9x65HkpxvRFHeXEDMM9EWKE/edit

| View | Sheet tab | Sheet ID (gid) | Header row |
| --- | --- | --- | --- |
| Current PGPs | CurrentPGPs | 0 | 2 |
| TOF Completions | TOF Completions | 1519593224 | 1 |

CurrentPGPs row 1 contains staff instructions. The directory deliberately starts with headings on row 2. TOF Completions uses headings on row 1. It displays the source heading `f` as `Faculty name`, fixes the display spelling of `CTL Aprrover`, and displays `Name (first last)` as `Instructor name`. The sheet itself is not modified.

The page retrieves CSV directly from Google when opened, when **Refresh records** is selected, and every five minutes while visible. Returning to an older open page triggers a refresh. Only the selected view refreshes; switching to an outdated view retrieves it again. Google may cache or delay exports, so this is periodically refreshed data, not instantaneous synchronization. The timestamp means the last successful retrieval, not the time someone edited the sheet.

Edit records in Google Sheets. No GitHub upload is needed for ordinary data changes. Newly added rows and columns are picked up automatically. Completely empty rows and entirely blank columns are omitted. Nonempty columns without headings receive a numbered heading. Filters or hidden rows in the sheet do not establish access restrictions and should not be used to hide confidential data.

## Access matters

Anonymous CSV retrieval worked for both tabs during development. This version uses public, unauthenticated read access. It contains no login or access control. Anyone able to access the source can retrieve its data, including faculty IDs, approval information, and notes. Changing display columns or using an unlisted link does not protect those fields. The robots directive discourages indexing but is not security.

Use this version only if those records are approved for public access. A safer public directory can use a separate spreadsheet containing only approved fields and records. Replace the configured spreadsheet ID and tab IDs with that spreadsheet's values. For staff-only records, use an authenticated application and authorized data access instead; a public static HTML page alone does not provide that protection. No sharing settings were changed as part of this work.

If access fails, check that the spreadsheet is accessible while signed out of Google, that the tab IDs still match, and that your organization permits public read access. If public access is appropriate and approved, Google Sheets **Share → General access → Anyone with the link → Viewer** is the documented link-sharing route. This implementation does not require publishing the whole workbook to the web. Do not add passwords, private service-account keys, or access tokens to this HTML or a public repository.

## Using the directory

- Search any displayed column, or select one column in **Search within**.
- Multiple search words must all occur somewhere in the selected search scope, regardless of order. Matching ignores case and accents.
- Select a header once for ascending order, again for descending. Sorting applies to every matching row before pagination.
- Dates formatted as `M/D/YYYY` or `YYYY-MM-DD` sort chronologically. Other text uses natural ordering (for example, Course 2 before Course 10). Academic terms sort as text, not by academic calendar. Blank cells appear as a dash and sort last.
- Leading-zero IDs remain text and display as exported by Google.
- Choose 25, 50, or 100 results per page. Wide tables scroll horizontally.
- If refresh fails, previously retrieved records stay visible with a warning. No records are written to browser storage or included in these source files.

## Customize

Near the bottom of `index.html`, edit `CONFIG` to change the spreadsheet ID, tab `gid` values, header rows, display titles, or refresh interval. Find each tab's gid in its Google Sheets URL. A renamed existing tab keeps its gid; a deleted and recreated tab may get a new one.

MCC colors are CSS variables near the top: navy `#003E6F` and orange `#FF6600`. Lato loads from Google Fonts, with Arial and system sans-serif fallbacks. The MCC text mark is typography, not an official logo asset. Sheet cell values are inserted as text, never interpreted as HTML.

Keep headings unmerged and on a single row, and use one record per row. Keep administrative instructions above the configured header row or in another tab. This directory reflects the source records as written; it does not deduplicate entries or infer completion decisions.

## Documentation

- Google spreadsheet access: https://developers.google.com/chart/interactive/docs/spreadsheets
- GitHub Pages setup: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

Open the deployed HTTPS site for reliable testing. Double-clicking a local HTML file can have different browser network restrictions.
