# Roadmap

> **Plan. There is no code yet.** Milestones are ordered by dependency, not by date. From M1 on, the release goal for each milestone is a tagged prerelease built for every platform with the CI and release workflows of the sister apps. Command ids refer to [COMMANDS-PLAN.md](COMMANDS-PLAN.md). A command is registered in the app only when it works.

## M0 — Planning (this repository)

- [x] Concept and survey: the Anne's Office apps and Adobe's apps reviewed, nearest relatives named ([ORIGINALITY.md](ORIGINALITY.md)).
- [x] Name, description, topics, keywords, app id and icon color ([AnnesKeep.meta.json](../AnnesKeep.meta.json), `package.json`).
- [x] README, command inventory ([COMMANDS-PLAN.md](COMMANDS-PLAN.md), generated from [commands-plan.src.txt](commands-plan.src.txt)), AI plan ([AI-PLAN.md](AI-PLAN.md)), architecture ([ARCHITECTURE-PLAN.md](ARCHITECTURE-PLAN.md)), formats ([FORMATS-PLAN.md](FORMATS-PLAN.md)), legal notes, license, contributing guide, issue templates, icon.
- [x] `scripts/gen-plan.py` validates ids, origin codes, shortcut conflicts, the required AI commands and the metadata file; planning-stage CI runs it on Linux and Windows.
- [ ] Re-check the Adobe lineup against Adobe's own product catalog. The list in ORIGINALITY.md was carried over from the Anne's Witness survey and was not checked again.
- [ ] Check section 3 of ORIGINALITY.md (nearest relatives) against the current state of those tools. It was written from general knowledge, without a search.
- [ ] Have the wording of each template and of *Help ▸ Common Practice* read by someone who does that work (an archivist, a records manager, someone who has settled an estate) and correct the vocabulary; confirm that the app claims conformance to no standard and states no legal retention period.
- [ ] Write the format register's schema and its first entries, each fact dated and with its origin. Decide whether any content of a public format register may be reused under its license; until that is settled, only its identifiers are cited.
- [ ] Write the status rules and the risk rules as test tables.
- [ ] Specify each comparator of the Sameness Check: what is compared, the tolerances, and the words of the Loss Statement.
- [ ] Build a small openly licensed test corpus: files in old and current formats, a pair of copies of which one is damaged, a document with a missing font and a linked picture, a conversion known to lose something, a made-up disk image.
- [ ] Confirm the license of every on-device model candidate in AI-PLAN.md and of every planned component in LEGAL.md.

## M1 — Shell, the holding file and fingerprints

- Project scaffold from the sister apps: TypeScript, Vite, vitest, Capacitor (Android, iOS), Electron, PWA manifest and service worker, CI and release workflows.
- Suite shell: command registry, ribbon with the 15 tabs, Quick Access Bar, classic menu bar (one menu per tab, including **AI**), Customize Ribbon and Keyboard, command search, Backstage, preferences.
- Holding engine: the `.keep` container, the journal with undo and History (`edit.history`), Versions, autosave and restore, Open and Repair for the holding itself.
- Take In: Add Files, Add Folder, New Holding from Folder, Leave Out, Refresh from Disk. Streaming SHA-256 in background workers; pause and resume.
- Identify Format for a first set of common formats; Extension Mismatch; Format Census.
- Items shown through the first readers: plain text, PDF, pictures. The Shelf and Item views.
- Fixity Check; Find Moved Files; Find Duplicates by byte hash.
- First status rules: Unassessed, Damaged, Missing; Next Item Needing Attention.
- A catalog test comparing the registry with `docs/commands-plan.json`.

**Done when:** a person can point the app at a folder of a few thousand files, close it, change one file, delete another, rename a third, and be told exactly that on Refresh.

## M2 — Assessment and risks

- Readers for documents, workbooks, presentations and archive files; Open Check and Structure Check.
- Lock Check, Dependency Check, Completeness Check, Date Check, File Name Check.
- The format register, Format Notes, Edit Format Register; Format Risk with its reasons.
- The risk rules, the Risks pane, Risk Details, Accept Risk, Reopen Risk; the Risk Board view.
- The Stranger Test.
- Status rules for At Risk and Watch.

**Done when:** for the test corpus, every planted problem (old format, missing font, linked picture, password, bad name, truncated file) is found and explained, and nothing sound is flagged.

## M3 — Places and copies

- Places, New Place, Place Details, Away from Home, the Media Log.
- Send Copy To with read-back and compare; Write Manifest; the `KEEP/` folder; Save Catalog to Every Place.
- Verify Place, Verify by Sample, Compare Two Places, Restore Drill, Record Outside Check.
- Heal from Another Copy; Report Lost Place; Retire Place; Move Copy.
- The copy rule, Copy Rule Check, Complete the Copy Rule, Media Age Check, Single Point Check; the Copy Map view.
- Audit Schedule, Run Audit Now, Audit Records; reminders; the Calendar view.
- Status rules for Sound and Stale. Open and Repair from the catalog copies at the places.
- Hash Calculator and Verify a Manifest, which work with no holding.

**Done when:** a holding with three places can lose any one of them, including the device with the `.keep` file, and be brought back whole from the other two.

## M4 — Description

- Description, People and Organizations, Places Named, Subjects, Dates, Rights and Restrictions; Fill Down, Copy and Paste Description.
- Arrangement, groups, Inherit Description, Number Items, Keep Original Order.
- Read and Use Embedded Details; Describe from File Names; OCR and Extract Text for Search; Find in Whole Holding.
- Accession Record, Custody Note, Mark as Held for Someone Else, Add Item with No File.
- Description Check, Name Authority, Controlled Lists, Mark as Confidential; Link to Person in Tree.
- Find Versions, Group as One Item.
- Finding Aid and Item List (first versions); the Timeline view.

## M5 — Renditions and the Sameness Check

- Readers for mail, databases, family tree files, layouts, sound, video and e-books.
- Lasting Formats, Rendition Plan, What Would Be Lost, Dry Run, Batch Make.
- Make Rendition for text, documents, workbooks, presentations, fixed-page documents and pictures, through the sister apps' writers; Make Plain-Text Rendition; Make Page-Image Rendition; Make Reading Copy; Embed What It Depends On; Make File Names Safe.
- The comparators for those kinds; Sameness Check, Loss Statement, Accept Loss, Reject Rendition, View Side by Side, Round-Trip Check.
- Rendition Lineage and the Lineage view; Set as Preservation Copy; Replace Rendition.
- The Secured status.

**Done when:** for every conversion in the test corpus that is known to lose something, the Loss Statement names the loss, and for every one known to be clean it reports Same.

## M6 — Rescue and repair

- Repair Item through the sister apps' recovery engines; Recover Text Only; Recover Pictures Only; Repair Report; Damage Report.
- Read Disk Image (raw images; FAT, exFAT, NTFS, ISO 9660, UDF, read-only); Make Disk Image on desktop builds.
- Open Archive File for older archive formats; Old Text Encodings; Unidentified Files.
- Add from Another Device, Watch Folder, Add Account Export, Capture Web Site, Add Mailbox; reading WARC.
- New Holding for Someone Else's Files; New Holding from Manifest.

**Done when:** the guided example can be worked from start to finish: a folder from an old computer with a letter in a retired format, photographs of which one copy is damaged, and one USB drive, ending with every item Sound or Secured and one risk accepted in writing.

## M7 — Retention, handover and review

- Renditions and comparators for mail, databases, family tree files, web sites, layouts and sound; writing WARC.
- Keep Until, Retention Rules, Apply Rule, Why Is This Kept, Worth Keeping; holds; Due for Review; the Review Calendar.
- Release, Release Duplicates, Remove Released Files, Release Record, Restore Released Item, Transfer Out.
- Restrict Until, Living People, Sensitive Patterns.
- Format Guide, Where Everything Is, Letter to Whoever Opens This, Keys and Passwords Note, Wishes, People to Contact; Build Handover Packet; Test Packet as a Stranger; Copy for a Person.
- Package for Deposit, Export Catalog, Gift Checklist, Record Receipt.
- Condition Report, Risk Register, Copy Map Report, Audit Report, Change Report, Rendition Report.
- Comments, Mark Described, Mark Checked, Review Queue, Two-Person Rule; Compare, Merge and Split Holdings; Import Descriptions.
- Keep the Sources of a Case (Anne's Witness); Keep a Family Tree's Media (Anne's Chart).
- Macros, Rules, the script editor, the command line audit for scheduled jobs, Query Holding, the Event Log.

**Done when:** a Handover Packet built from the guided example passes *Test Packet as a Stranger*, and a person who has not seen the app can say from the packet alone what is there, what matters and how to open it.

## M8 — AI

- AI tab and AI menu: the suite's setup wizard, provider adapters, AI and Privacy (for the holding, a group and an item), AI History, Stop AI, Several AIs.
- The three gates first (identification, catalog, decoding), built and tested before any AI command. See [AI-PLAN.md](AI-PLAN.md).
- A test that no AI command can reach a command that writes, moves, converts or deletes a file.
- Describe group, then Ask the Holding, then Sort, Rescue and Write.
- The on-device search index, Find Related Items, and on-device Screen for Private Information.

AI comes late on purpose: the app must be complete and useful without it, and every AI command produces proposals for flows that already exist.

## M9 — Stretch goals

- Recovery Records: error-correcting data beside a copy, written from the published mathematics.
- A shared holding over the suite relay for a family or an office working at the same time.
- Export of events and descriptions in the XML forms of the published preservation-metadata and archival-description standards; a database rendition in the published archival format for relational databases.
- Video renditions through a converter the user has installed, with comparison of playing time and sampled frames.
- Reading content credentials attached to a picture and showing them in the description (reading only).
- Trusted timestamps for audit records, from a service of the user's choice.
- More disk-image and file-system formats, where a public description exists.
- Templates and format-register entries contributed by people who do this work.

## Throughout

- **Items are never written.** Every reader is tolerant, and anything that converts or repairs a file writes a new file.
- **Nothing is deleted without a person, a count and a record.**
- **Every milestone ships tests** for the status rules, risk rules and comparators it adds; the rules are the product.
- **The app's own files pass its own tests:** what it writes at each place and in a packet must be readable by the Stranger Test.
- **Accessibility:** status is never shown by color alone; every pane works by keyboard and with a screen reader.
