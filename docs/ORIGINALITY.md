# Originality survey

> **Plan. There is no code yet.** This file records the review that was done before Anne's Keep was named: every app in the Anne's Office suite, and Adobe's apps, each checked against one question — *is its main job to see that files someone already has stay findable, whole and readable over many years?* It also names the nearest relatives outside those two lineups, so that the claim of originality is stated no more strongly than the review supports.

## What is claimed, and what is not

- **Claimed:** Anne's Keep is not a clone, port or rehash of any Anne's Office app or of any Adobe app. None of them has the long-term survival of a body of files as its subject.
- **Not claimed:** that nothing like any part of it exists anywhere. Digital preservation is an established field with its own tools, standards and literature (section 3). What was not found is one general tool that brings that practice to a person, a family or a small office and joins it to copies, tested conversion, retention and handover. No market search was done.
- **How the review was done:** the twelve suite repositories were checked directly. Anne's Witness was read in full; the other eleven were searched for preservation features (fixity, checksums, archival formats, archives, backups, metadata, recovery), and the places found were read. The Adobe lineup in section 2 is the list recorded in [Anne's Witness's survey](https://github.com/socrtwo/annes-witness/blob/main/docs/ORIGINALITY.md) in the same month; it was not checked again for this review, so it carries the same open item (re-check against Adobe's own catalog; see [ROADMAP.md](ROADMAP.md), M0). Section 3 was written from general knowledge of the field, without a search.

## 1. The Anne's Office suite

| App | Its job | Nearest feature to Anne's Keep | Why it is a different job |
|---|---|---|---|
| Anne's Pen | Write documents | Opens damaged documents with a recovery engine; saves in several formats | Works on the one document that is open. It does not know which documents exist, where their copies are, or whether a saved-as copy lost anything |
| Anne's Grid | Spreadsheets | Opens damaged workbooks with a recovery engine | The same, for workbooks |
| Anne's Post | Email, calendar, contacts | Local Archives; archive by year | Moves messages out of the way inside the mail program. It does not verify the archive, rate its format or count its copies |
| Anne's Stage | Presentations | Recovery engine | Works on one presentation |
| Anne's Loom | Web sites | Site archive ZIP; site reports | Packs the site being built. Anne's Keep will use Loom to capture a site, then look after the capture |
| Anne's Press | Desktop publishing | — (its repository holds only an early plan) | Lays out pages; a layout with its links is a typical grouped item |
| Anne's Folio | PDF | *Prepare for Archiving*; checks that report what blocks PDF/A conformance; repair | One format, one file at a time. Anne's Keep will use Folio as the writer and the checker for PDF renditions |
| Anne's Lens | Pictures | Checksums and a *Fixity Report* for a folder; metadata; batch conversion; carving pictures out of damaged media | The nearest neighbor. Lens offers a fixity manifest for a folder of pictures as one of its Metadata commands. It has no places, copy rule, format risk, tested renditions of other file types, retention or handover. Anne's Keep will import Lens manifests |
| Anne's Base | Databases | Integrity checks; downloaded backups; carving tables out of disk images | Protects the one database that is open |
| Anne's Chart | Diagrams, org charts, family trees | GEDCOM export; privacy filter for living people | Draws the tree. Anne's Keep will keep the tree file and the media it refers to, and reuse the living-person rule |
| Anne's Test | Web security testing | — | Tests a web site; its reports can be items |
| Anne's Witness | Evidence | Source fingerprints, *Check Fingerprints*, portable and sealed cases | Fingerprints serve the proof: they show that a tied source has not changed. Witness does not ask whether the source will still open in thirty years or whether there is a second copy. The two fit together: a case's sources can live in a holding |

Anne's Keep sits beside the suite; it does not replace any part of it. It opens the other apps' files to test them, asks the other apps to write renditions and to repair damaged files, and edits nothing.

## 2. Adobe's apps

Grouped by job, as recorded in the Anne's Witness survey. None has the long-term survival of a body of files as its subject.

| Group | Apps | Job |
|---|---|---|
| Photographs and painting | Photoshop, Lightroom, Lightroom Classic, Photoshop Elements, Fresco | Edit, organize and paint pictures |
| Drawing and layout | Illustrator, InDesign, InCopy, Express | Vector art, page layout, editorial copy, quick designs |
| Video and motion | Premiere, Premiere Elements, After Effects, Media Encoder, Character Animator, Animate, Frame.io | Edit, composite, encode, animate and review video |
| Sound | Audition, Podcast | Record and edit audio |
| 3D | Substance 3D Painter, Designer, Sampler, Stager and Modeler; Dimension; Project Neo; Mixamo | Model, texture and render 3D |
| Generative AI | Firefly (with Boards and, as reported at MAX 2026, Firefly Builder, Firefly Graph and the Firefly AI Assistant) | Generate and edit images, video, audio, designs and prototypes; automate creative workflows |
| Documents | Acrobat Reader, Standard, Pro and Studio; Acrobat Sign; Scan; Fill & Sign; Digital Editions | View, edit, sign, scan and read PDFs and e-books |
| Web and interface design | Dreamweaver, XD | Build web pages; design interfaces |
| Assets and services | Bridge, Fonts, Stock, Color, Capture, Behance, Portfolio | Browse files, license fonts and stock, pick colors, show work |
| Technical and learning | FrameMaker, RoboHelp, Captivate, Connect, ColdFusion | Technical manuals, help systems, e-learning, web meetings, an application server |
| Provenance of media | Content Authenticity (and Content Authenticity for Enterprise) | Attach signed content credentials to a creative file saying who made it and how |
| Marketing and enterprise | Experience Manager, Analytics, Target, Campaign, Marketo Engage, Journey Optimizer, Real-Time CDP, Commerce, Advertising, Workfront, GenStudio | Web content management, analytics, marketing automation, commerce, work management |
| Retired or winding down | PageMaker, FreeHand, Fireworks, Flash Professional, Director, Authorware, GoLive, Muse, Contribute, Encore, Soundbooth, Prelude, SpeedGrade, Story, Spark, Premiere Rush, Aero, Comp, Photoshop Mix, Fix, Sketch and Camera, Illustrator Draw, the Edge tools, PhoneGap, Flash Builder | Earlier layout, drawing, web, multimedia authoring, video and mobile tools |

The last row is itself a reason for this app: files made with retired programs are exactly the items Anne's Keep is meant to find, rate and carry forward.

### The closest Adobe features, and how they differ

| Adobe feature | What it does | Difference |
|---|---|---|
| Acrobat **PDF/A conversion and Preflight** | Converts a PDF to an archival profile and checks it against that profile | One target format, one file, and a test of conformance to the profile. Anne's Keep covers any file type, tests that the *content* matches the original, and tracks the item afterward |
| **DNG Converter** | Converts camera raw files to a publicly documented raw format | One family of formats, with no comparison report, no copies and no catalog |
| **Bridge** | Browses asset files, edits their metadata, renames in batches | Describes and finds files. It has no fingerprints, places, risks or audits |
| **Lightroom Classic** catalog | Catalogs photographs, backs up the catalog, reports photographs it can no longer find | A working catalog for editing pictures. The backup is of the catalog, and only pictures are covered |
| **Media Encoder** | Converts video and audio between formats | Conversion for delivery, without a test of what was lost |
| **Creative Cloud** storage | Syncs files between devices and keeps earlier versions for a time | One copy service. Anne's Keep can register such a service as one place among several and verify what is there |
| **Experience Manager Assets** | Manages an organization's media files for publishing | Asset management for marketing teams on a server |
| **Content Authenticity** | Records who made a media file and what tools touched it | Provenance of a file at the time it was made. Anne's Keep records what has happened to a file since, and whether it is still whole |
| **Digital Editions** | Reads e-books, including ones with usage restrictions | A reader. Anne's Keep reports usage restrictions as a risk and does not remove them |

## 3. Nearest relatives elsewhere

These are named so that readers can judge the overlap themselves. Each does part of the job, most of them for institutions. Anne's Keep borrows no code, text or interface from any of them.

| Kind of tool | Examples (nominative use) | The slice it covers | What Anne's Keep adds |
|---|---|---|---|
| Preservation systems for institutions | Archivematica, Preservica, Rosetta | The whole preservation workflow, on servers, run by trained staff | The same ideas on one device for people with no staff: no server, plain words, a copy rule, handover |
| Format identification and validation | DROID, Siegfried, JHOVE, veraPDF, MediaInfo | What a file is; whether it obeys its format's rules | The result becomes a status, a risk with reasons, and a next step |
| Format registers | PRONOM, the Library of Congress format descriptions | Facts about formats | A small register of its own, in plain words, that the user can correct, feeding a rating whose reasons are shown |
| Fixity and packaging tools | Fixity, Bagger and other BagIt tools, checksum utilities | Manifests; checking a folder against one | Fixity per copy and per place, a schedule, healing from another copy, and a record of every check |
| Backup and sync programs | Time Machine, File History, restic, Borg, Duplicati; cloud sync services | Making and restoring copies | Knowing what the copies are copies of, whether each still matches, and whether the set meets a stated rule. Backup programs remain the right tool for making nightly copies |
| Recovery records | PAR2 tools | Repairing limited damage from stored parity data | Optional, as one command among the copy commands |
| Converters | LibreOffice, pandoc, ImageMagick, FFmpeg | Changing format | A comparison of the result with the original, a statement of loss, and a person's acceptance |
| Collection tools for archives | BitCurator, ePADD, web-archiving tools such as Webrecorder | Disk images, email collections, web captures | One holding that can contain all three beside ordinary files |
| Photograph and media managers | digiKam and similar | Describing and finding pictures | All file types; survival is the subject, not browsing |
| Records-management systems | products for enterprises | Retention schedules, holds, disposal | The same three ideas at household and small-office size, with no stated legal periods |
| Digital-legacy services and emergency access in password managers | services from account providers and password managers | Passing accounts and passwords to a named person | Passing the files, with a guide to what they are and how to open them. Anne's Keep records where keys are kept, not the keys |
| File-repair tools | many, among them the author's earlier recovery programs | Getting content out of one damaged file | Repair as one step in a record: the damaged original stays, the repaired file is a rendition with a report |

## 4. What is new in the combination

1. **One model at household size:** item, copy, rendition, risk, holding — the same for a shoebox of photographs, a manuscript and a club's minute books.
2. **Status that the app can justify and that decays.** An item is Sound only while verified copies and passed checks justify it, and turns Stale by itself when a check is overdue.
3. **Risks come with their reasons.** Every risk names the facts it rests on, in a register the user can read and correct, and the commands that would reduce it.
4. **A conversion counts only when it is compared.** The Sameness Check tests a rendition against its original by content and writes a Loss Statement. A person accepts a stated loss or rejects the rendition.
5. **The Stranger Test:** how much of the holding could be read with nothing but a text editor, a web browser and an unzip tool.
6. **The Single Point Check:** everything that would be lost with one named drive, account or password.
7. **The catalog travels with every copy,** in a plain-text form, so that the holding can be rebuilt from any place that survives and any copy can be checked without the app.
8. **Letting go is recorded.** Release keeps the reason, the date and the fingerprint; duplicates are released only when byte-identical and never down to nothing.
9. **Handover is tested.** The packet is opened as a stranger would open it, and what could not be understood is reported.
10. **Gates for AI:** a model's guess at a format counts only if the app's own reader then opens the file, and a suggested date or name is shown only if the app finds it in the item ([AI-PLAN.md](AI-PLAN.md)).

## 5. Where the ideas come from

The practices are older than computers, and the vocabulary is generic.

- **Two copies, a durable container, and a stated purpose.** Keeping a record in more than one copy so that it outlasts its makers is ancient. Jeremiah 32:14 (KJV): "Take these evidences, this evidence of the purchase, both which is sealed, and this evidence which is open; and put them in an earthen vessel, that they may continue many days." The passage records a deed kept as a sealed copy and an open copy in a vessel chosen to last. The app's copy rule, its attention to the medium, and the jar in its icon come from this tradition.
- **Archival practice:** recording where papers came from and who held them, keeping the order they arrived in, describing groups before items, judging what has lasting value, and restricting access for a time.
- **Digital-preservation practice:** fingerprints checked on a schedule, identifying formats by their content, rating the risk of a format, converting to open formats while keeping the original, and logging every action taken on a file.
- **Backup practice:** several copies on different kinds of medium in different places, reading a copy back after writing it, and practicing a restore before it is needed.
- **Records management:** deciding in advance how long each kind of record is kept, holding what must not be destroyed, and destroying the rest with a record.
- **Library cataloguing:** a small set of descriptive fields, one agreed form for each name, and lists of subjects.
- **Data recovery:** working on an image of a failing disk and never on the disk, never writing to the damaged original, and salvaging what can be read.
- **Estate practice:** an inventory and a letter of instruction for the people who will have to deal with one's things.
