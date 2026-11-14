# Formats plan

> **Plan. There is no code yet.** Anne's Keep can take in any file, whether or not it can open it, and edits none of them. What varies by format is how much the app can *do* with an item: identify it, open it to test it, make a rendition of it, and compare the rendition with the original. Readers and writers come from the sister apps wherever one exists. Formats are recognized by content, not by extension.

## The holding

| Format | Use |
|---|---|
| `.keep` | The holding: a ZIP container with a SQLite catalog, a journal, the format register in use and derived text. It does not contain the items. See [ARCHITECTURE-PLAN.md](ARCHITECTURE-PLAN.md). |
| `KEEP/` folder at each place | A plain-text SHA-256 manifest, the catalog as JSON and as readable text, and a README, so that a copy can be checked and understood without the app |
| Text folder | The holding as JSON and Markdown files, for version control (`dev.exportText`); can be imported back |

The extension is provisional until M1. Some tools use an empty file named exactly `.keep` as a placeholder in a folder; that is not a holding, and since formats are recognized by content it will not be mistaken for one. If the clash proves confusing in practice, the extension will change before the first release.

## Four levels of support

| Level | What the app can do | Applies to |
|---|---|---|
| **Kept** | Fingerprint, copy, verify, describe, retain, hand over | Every file, including ones nothing can identify |
| **Identified** | The above, plus name the format and version, and rate its risk from the register | Formats with an identification rule |
| **Opened** | The above, plus the Open, Structure, Lock and Dependency Checks, text for search, and a preview | Formats with a suite reader |
| **Carried forward** | The above, plus a rendition in a lasting format and a Sameness Check on it | Formats with a suite reader, a suite writer for the target, and a comparator |

An item at the first level is still protected against loss and damage. The Format Census shows how much of a holding is at each level.

## Items the app can open

| Kind | Formats | Reader | Milestone |
|---|---|---|---|
| Plain text and data | .txt, .md, .csv, .tsv, .json, .xml, .html, older character sets | built in | M1 |
| PDF | .pdf, including scanned and damaged files | Anne's Folio engine | M1 |
| Pictures | JPEG, PNG, TIFF, WebP, HEIC, GIF, BMP, camera raw previews, and the older formats Anne's Lens reads | Anne's Lens readers | M1 |
| Documents | Anne's Pen, .docx, .doc, .odt, .rtf, and the older word-processor formats Anne's Pen reads | Anne's Pen readers | M2 |
| Workbooks | Anne's Grid, .xlsx, .xls, .ods, and the older spreadsheet formats Anne's Grid reads | Anne's Grid readers | M2 |
| Presentations | Anne's Stage, .pptx, .ppt, .odp | Anne's Stage readers | M2 |
| Archive files | ZIP, TAR, gzip, and older archive formats where a public description exists | built in; the suite's ZIP salvage for damaged ones | M2 |
| Mail | .eml, .msg, .mbox, messages from Anne's Post | Anne's Post readers | M5 |
| Databases | Anne's Base, SQLite, .accdb and .mdb (as Anne's Base reads them), .dbf | Anne's Base readers | M5 |
| Family tree files | GEDCOM 5.5, 5.5.1, 7.0 | Anne's Chart reader | M5 |
| Layouts and web sites | Anne's Press layouts, Anne's Loom sites, folders of HTML | Anne's Press and Loom readers | M5 |
| Sound | WAV, FLAC, MP3, M4A, OGG | platform media | M5 |
| Video | MP4, WebM, MOV and others the platform plays | platform media (Opened only; see below) | M5 |
| E-books | EPUB (without usage restrictions) | built in | M5 |
| Web captures | saved pages; WARC (read) | built in | M6 |
| Disk images | raw images of floppy disks, hard disks, cards and optical discs; FAT, exFAT, NTFS (read), ISO 9660 and UDF | built in, with the suite recovery engines | M6 |
| Account exports | ZIP archives of JSON, HTML and media as web services provide them | built in, as an archive with recognized parts | M6 |

Files protected by usage restrictions or by a password you do not have are kept and identified, not opened. The Lock Check reports them.

## Renditions: lasting-format choices

The defaults below are the holding policy's starting point (`rendition.targets`); every one can be changed. "Lasting" here means only this: the specification is published, more than one independent program reads the format, and it does not depend on anything outside the file. It is not a prediction.

| Content | Default lasting format | Also offered | Writer | What the Sameness Check compares | Milestone |
|---|---|---|---|---|---|
| Any text-bearing item | Plain text, UTF-8 | — | built in | every word present, in order | M5 |
| Word-processor documents | OpenDocument Text or .docx, by policy | PDF for the look; page pictures | Anne's Pen; Anne's Folio | words, structure counts, fonts; pages as pictures for the PDF | M5 |
| Fixed-page documents | PDF prepared for archiving | page pictures (PNG or TIFF) | Anne's Folio | words, page count, pages as pictures | M5 |
| Workbooks | OpenDocument Spreadsheet or .xlsx, by policy | one CSV per sheet with a list of formulas | Anne's Grid | cell values, recomputed formula results | M5 |
| Presentations | PDF, with OpenDocument Presentation or .pptx | page pictures | Anne's Stage; Anne's Folio | text, slide count, slides as pictures | M5 |
| Pictures in lossless or raw formats | TIFF or PNG | — | Anne's Lens | pixels exactly; embedded details | M5 |
| Pictures in JPEG | kept as they are | — | — | re-encoding a lossy picture loses more or wastes space; JPEG's specification is public, so the item is rated accordingly | — |
| Sound | FLAC or WAV | — | built in or platform | samples exactly for lossless sources; playing time | M7 |
| Mail | .mbox or one .eml per message, with attachments | PDF of each message | Anne's Post | message count, headers, bodies, attachments by hash | M7 |
| Databases | SQLite, with one CSV per table and the schema as text | — | Anne's Base | tables, columns, row counts, a hash of each table's rows | M7 |
| Family tree files | GEDCOM 7.0, with a plain-text listing | — | Anne's Chart | persons, families, events, citations | M7 |
| Web sites | a folder of static pages that opens in a browser | WARC | Anne's Loom | pages, text, pictures by hash | M7 |
| Layouts | PDF, with the layout file, its pictures and its fonts grouped | page pictures | Anne's Press; Anne's Folio | pages as pictures | M7 |
| Video | no conversion in the app | conversion through a program the user has installed, then the same record and comparison of playing time and frames sampled | — | see below | M9 |

### Honest names

- A PDF rendition is called **prepared for archiving** until Anne's Folio writes conforming PDF/A and a validator confirms each file. Until then Anne's Keep reports what stands in the way, as Anne's Folio does, and does not use the name of the standard for its output.
- Video is **Opened**, not **Carried forward**. The permissively licensed tools available to the base app cannot yet transcode video to an open lossless format, and the widely used converters carry licenses the suite does not accept in its builds (see [LEGAL.md](LEGAL.md)). A video item is therefore identified, fingerprinted, copied, verified and described, and its format risk is shown; conversion is left to a program of the user's choice, whose output can be added as a rendition and compared.
- A plain-text rendition of a picture-only document is the recognized text (OCR) and is labeled as such. It is an aid; the pictures remain the content.

## Exports

| Output | Formats |
|---|---|
| Finding Aid, Format Guide, Condition Report, Audit Report, Change Report, Release Record | Anne's Pen, .docx, PDF, HTML, Markdown, plain text |
| Item List, Risk Register, Rendition Report | Anne's Grid, .xlsx, .csv, PDF |
| Copy Map, Rendition Lineage | Anne's Chart, SVG, PNG; the table as .csv |
| Handover Packet | a folder: `START-HERE.txt` and `START-HERE.html`, the item list, the format guide, the chosen files, and a SHA-256 manifest |
| Package for Deposit | the published BagIt layout (RFC 8493): a data folder, manifests, and descriptive tag files |
| Catalog | CSV, JSON, and XML with commonly used descriptive field names (the Dublin Core terms) |
| Manifests | SHA-256 by default; SHA-512, and MD5 and SHA-1 for comparison with older lists only |
| Reminders | iCalendar, through Anne's Post or the system calendar |

## Imports

| From | What comes in |
|---|---|
| Checksum lists in the common tool formats (SHA-256, SHA-512, SHA-1, MD5) | fingerprints to verify against; older algorithms are checked, then SHA-256 is added |
| BagIt packages | items, manifests and tag files |
| Anne's Lens fixity manifests | fingerprints and their history |
| An Anne's Witness case | its sources as items, with their fingerprints (`tools.fromWitness`) |
| GEDCOM | the media a tree refers to, with links to persons (`tools.fromChart`) |
| Details embedded in files | Exif, IPTC and XMP in pictures; document properties; PDF information; tags in sound files |
| CSV | a catalog made elsewhere, matched to files by path or by fingerprint |
| Another `.keep` holding | items, descriptions, places and events (`review.merge`, `review.importDescriptions`) |

Importers for the reports and catalogs of other preservation, backup and cataloguing programs will be added only where the format is publicly documented.

## Standards the plan draws on

Each is implemented, where it is used at all, from its public specification. Anne's Keep claims conformance to none of them until a named test shows it, and says so in its output.

| Standard | Use |
|---|---|
| SHA-2 (FIPS 180-4) | fingerprints |
| BagIt (RFC 8493) | Package for Deposit; the manifest line format |
| ZIP, TAR | containers |
| Dublin Core terms | names of descriptive fields on export |
| PDF (ISO 32000) and PDF/A (ISO 19005) | PDF renditions, through Anne's Folio |
| OpenDocument (ISO/IEC 26300) and Office Open XML (ISO/IEC 29500) | document, workbook and presentation renditions, through Anne's Pen, Grid and Stage |
| TIFF, PNG, FLAC, WAV | picture and sound renditions |
| GEDCOM 7.0 | family tree renditions, through Anne's Chart |
| WARC (ISO 28500) | web captures: read in M6, written in M7 |
| iCalendar (RFC 5545) | reminders |
| Unicode | text; file-name normalization checks |
| Published preservation-metadata and archival-description standards | the general shape of the Event record and of the Finding Aid; export in their XML forms is a stretch goal |
