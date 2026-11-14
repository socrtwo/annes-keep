# Anne's Keep

*Part of the Anne's Office suite: [Anne's Pen](https://github.com/socrtwo/annes-pen) (documents), [Anne's Grid](https://github.com/socrtwo/annes-grid) (spreadsheets), [Anne's Post](https://github.com/socrtwo/annes-post) (email), [Anne's Stage](https://github.com/socrtwo/annes-stage) (presentations), [Anne's Loom](https://github.com/socrtwo/annes-loom) (web sites), [Anne's Press](https://github.com/socrtwo/annes-press) (desktop publishing), [Anne's Folio](https://github.com/socrtwo/annes-folio) (PDF), [Anne's Lens](https://github.com/socrtwo/annes-lens) (pictures), [Anne's Base](https://github.com/socrtwo/annes-base) (databases), [Anne's Chart](https://github.com/socrtwo/annes-chart) (diagrams and family trees), [Anne's Test](https://github.com/socrtwo/annes-test) (web security), [Anne's Witness](https://github.com/socrtwo/annes-witness) (evidence) and **Anne's Keep** (preservation).*

**Make it last.** Anne's Keep is an original, open-source preservation workbench for Android, iOS, Windows, macOS, Linux, ChromeOS and the web. The other apps in the suite help you *make* things, and Anne's Witness shows how you know what they say. Anne's Keep answers the question that is asked ten, thirty or a hundred years later, usually by someone else: **can we still open it?**

You point it at the files you care about: a family's photographs and letters, a household's papers, the working files of a book, the records of a small office. It tells you what each file really is, whether it still opens, where every copy is and whether each copy is still good. It lists what threatens each one, with the reason. It makes copies in formats that are likely to stay readable and tests that each copy still says what the original says. It reminds you to check again. When the time comes, it packs the whole thing so that a person who never met you can find their way around it. It shares the suite's goal, **no missing commands**: every feature is a command that can go on the Quick Access Bar, on your own tab, in the classic menu bar, on a keyboard shortcut or in a macro, and is found by command search. It has an **AI** tab and an **AI** menu, with one rule: the AI may describe and suggest, but only a check the app computes counts, and only a person lets anything go.

> **Status: planning. There is no code yet.** This repository holds the plan: the concept, the command inventory (319 commands on 15 tabs), the AI plan, the file and architecture plans, and the roadmap. Issues and discussion are welcome.

## Why this app exists

No app in the Anne's Office suite, and no Adobe app, does this job; [docs/ORIGINALITY.md](docs/ORIGINALITY.md) goes through both lineups one by one. The work itself is well understood. Archives and libraries do it with staff and with systems built for institutions. Almost everyone else does it by hope:

- A **family** has forty years of photographs on one aging hard disk, and letters in a word-processor format that nothing on the new computer opens.
- An **executor** or a grown child is handed a laptop, a box of unlabeled drives and no account of what is on them or what matters.
- A **writer or researcher** has the files of a finished book, with linked pictures and fonts, and will need them again for a new edition in fifteen years.
- A **small office, church or club** must keep some records for a set number of years, may destroy others, and has no record of which is which.
- Someone has a **backup** and has never tried to restore from it.
- Someone **converted** everything to a newer format and never checked what the conversion dropped.

These are the same task. Anne's Keep is one tool for it.

## The five things in a holding

| Thing | What it is |
|---|---|
| **Item** | A file, or a group of files that make sense only together (a page layout with its pictures, a web site folder, a mailbox). Items are fingerprinted and never altered. An item can also be a thing with no file, such as a box of prints, so that the holding covers what is not digital. |
| **Copy** | One stored instance of an item at a **place**: this device, a drive, a disc, a cloud folder, another person's house. A copy remembers its place, its medium, and when it was last read back and compared with the fingerprint. |
| **Rendition** | A new file made from an item so that its content survives: a lasting format, a plain-text version, page pictures, a repaired file. A rendition remembers what it was made from, by which tool, and what the comparison with the original found. |
| **Risk** | Something that threatens an item, found by the app, with the facts it rests on: a format with no public specification, a font that is not embedded, a password nobody has written down, a single copy, a disc past its service life. |
| **Holding** | The file that holds all of the above, plus the descriptions, the policy, the audit records and the history (`.keep`). The holding is a catalog: the files stay where they are. |

Each item has a status that the app can justify at any time: **Unassessed** (not yet identified or checked), **Damaged** (no intact copy can be reached), **Missing** (no copy can be found), **At Risk** (intact, with a High risk open), **Watch** (intact, with lesser risks open), **Sound** (no open risk, enough verified copies), **Secured** (Sound, and in a lasting format or with a verified rendition in one), **Stale** (a check is overdue, or a file changed after it was fingerprinted) or **Released** (a person decided not to keep it, with a reason).

## Features and plan

- **Take in without disturbing.** Add files, folders, mailboxes, web site captures, account exports, phone and camera contents, disk images of old media, and things with no file at all. Files stay where they are. Where each batch came from, who held it before and the order it arrived in are recorded.
- **Checks the app computes itself, with no AI.** Identify Format (by content, not by extension), Open Check, Structure Check, Lock Check, Dependency Check, Fixity Check, Format Risk (from a format register you can read and correct), Copy Rule Check, Media Age Check, File Name Check, Single Point Check (what would be lost if one drive, account or password were lost) and the **Stranger Test** (how much of the holding a person with no special software could read).
- **Copies you can count on.** Places are registered with their medium and age. *Send Copy To* writes, reads back and compares before a copy counts. Every copy carries a plain-text manifest that can be checked without this app. *Verify Place*, *Restore Drill*, *Heal from Another Copy* and scheduled audits keep the count honest. The default rule is three copies on two kinds of medium with one away from home, and you can change it.
- **Renditions that are tested.** A rendition in a lasting format is made through the sister app that owns the file type. The **Sameness Check** then compares it with the original by content (words, page count, pixels, cell values and formula results, rows, playing time) and writes a **Loss Statement**. A rendition counts toward Secured only when the comparison passes or a person accepts the stated loss. The original is always kept.
- **Damaged files.** A damaged item goes to the suite recovery engine of its type. The repaired file is added as a rendition, with a report of what was and was not recovered; the damaged original stays. A damaged holding is rebuilt from its journal and from the catalog copies kept at every place.
- **Description a stranger can use.** Titles, dates, people, places, subjects, rights and restrictions, arranged as groups within groups that pass their description down. Details already inside the files are read and offered. The original order is kept however you rearrange.
- **Keeping and letting go, on the record.** Keep-until dates, retention rules, holds, review dates, and *Release*: a recorded decision not to keep something, with its reason and fingerprint. The app ships with no rule that states a legal period.
- **Handing over.** A Finding Aid, an Item List, a Format Guide, *Where Everything Is*, a Keys and Passwords Note (where each key is kept, never the key), and a **Handover Packet**: a folder that explains itself in plain text and as a web page that open on any computer. *Test Packet as a Stranger* opens it with the holding closed and reports what could not be understood.
- **AI tab and AI menu** with 36 commands: Ask the Holding, Draft Description, Suggest Dates, Transcribe, Suggest Arrangement, Guess Unidentified Format, Draft Handover Letter and the suite's provider setup, privacy settings, history and several-AIs modes. AI results are proposals. The app itself tests each one that can be tested before showing it, and no AI command changes, moves, converts or releases a file. See [docs/AI-PLAN.md](docs/AI-PLAN.md).
- **Private by default.** Everything works offline. Items can be marked confidential, which keeps them out of handover packets and every AI request. Details of living people can be left out of anything you share.

The full inventory is in [docs/COMMANDS-PLAN.md](docs/COMMANDS-PLAN.md).

## What it is not

- Not a backup program and not a storage service. It has no storage of its own and does not copy a whole disk every night. It knows what the copies are copies *of*, verifies them, and says when the rule is broken. A backup you already make can be registered as a place.
- Not a file manager or a photograph organizer; it describes and protects files and leaves browsing and editing to the apps that own them.
- Not a converter only. A conversion that was not compared with its original is not counted.
- Not a repository system for institutions. It borrows their practice for one person, a family or a small office, and claims conformance to no standard.
- Not a promise. Nothing can guarantee that a file will be readable in fifty years. Anne's Keep reports what threatens it, what was done about it, and when it was last checked.
- Not legal, tax, records or estate advice. *Wishes* is not a will. See [docs/LEGAL.md](docs/LEGAL.md).

## Platforms (planned)

As for the sister apps, each release will have builds for **Android** (APK and AAB), **iOS/iPadOS** (an unsigned .ipa you sign with your Apple ID), **Windows** (installer or portable), **macOS** (universal), **Linux** (AppImage or .deb for x64, arm64 and armv7l, which covers Raspberry Pi OS), **ChromeOS** and the **web** (static files; offline-capable and installable). Reading whole drives and making disk images are planned for the desktop builds only; phones and browsers reach only the folders their file pickers grant. See [docs/ROADMAP.md](docs/ROADMAP.md) and [docs/ARCHITECTURE-PLAN.md](docs/ARCHITECTURE-PLAN.md).

## The Anne's Office suite

| App | What it is | What Anne's Keep does with it |
|---|---|---|
| [Anne's Pen](https://github.com/socrtwo/annes-pen) | Word processor | Opens documents to test them; writes document, PDF and plain-text renditions; repairs damaged documents; receives the Finding Aid |
| [Anne's Grid](https://github.com/socrtwo/annes-grid) | Spreadsheet | Opens workbooks; compares cell values and formula results in the Sameness Check; writes workbook and CSV renditions; receives the Item List |
| [Anne's Post](https://github.com/socrtwo/annes-post) | Email | Mailboxes as items; message renditions; audit and review reminders; sends packets |
| [Anne's Stage](https://github.com/socrtwo/annes-stage) | Presentations | Opens presentations; page-picture and PDF renditions |
| [Anne's Loom](https://github.com/socrtwo/annes-loom) | Web sites | Captures web sites; site folders as grouped items; the packet's web-page guide |
| [Anne's Press](https://github.com/socrtwo/annes-press) | Desktop publishing | A layout with its linked pictures and fonts as one item; the Dependency Check |
| [Anne's Folio](https://github.com/socrtwo/annes-folio) | PDF | Opens and repairs PDFs; writes PDF renditions and reports what stands in the way of archival conformance |
| [Anne's Lens](https://github.com/socrtwo/annes-lens) | Pictures | Opens and salvages pictures; lossless renditions; embedded details; scanning; its fixity manifests can be imported |
| [Anne's Base](https://github.com/socrtwo/annes-base) | Databases | Opens databases; table renditions compared by row count and content; receives the catalog |
| [Anne's Chart](https://github.com/socrtwo/annes-chart) | Diagrams, family trees | Links items to persons in a tree; keeps a tree's media; draws the Copy Map and lineage diagrams |
| [Anne's Test](https://github.com/socrtwo/annes-test) | Web security | Scan reports and fix records as items to keep |
| [Anne's Witness](https://github.com/socrtwo/annes-witness) | Evidence | Keeps the sources of a case and keeps the two apps' fingerprints in step |
| **Anne's Keep** | Preservation (this project) | https://github.com/socrtwo/annes-keep |

## Documentation

| File | Contents |
|---|---|
| [docs/ORIGINALITY.md](docs/ORIGINALITY.md) | The survey of the Anne's Office apps and Adobe's apps, why this is not a copy of any of them, its nearest relatives elsewhere, and where its ideas come from |
| [docs/COMMANDS-PLAN.md](docs/COMMANDS-PLAN.md) | The planned command inventory, tab by tab, with ids, shortcuts and origins (generated) |
| [docs/commands-plan.json](docs/commands-plan.json) | The same data as JSON, for the future catalog test (generated) |
| [docs/AI-PLAN.md](docs/AI-PLAN.md) | The AI tab and AI menu: what each command does and sends, the rules, privacy |
| [docs/ARCHITECTURE-PLAN.md](docs/ARCHITECTURE-PLAN.md) | The holding file, fingerprints, format identification, the status rules, the Sameness Check, the journal, repair |
| [docs/FORMATS-PLAN.md](docs/FORMATS-PLAN.md) | What can be an item, which renditions are planned and what each comparison tests, what is exported and imported |
| [docs/ROADMAP.md](docs/ROADMAP.md) | Milestones |
| [docs/LEGAL.md](docs/LEGAL.md) | Clean-room, trademark, privacy and licensing notes |
| [AnnesKeep.meta.json](AnnesKeep.meta.json) | Repository description, topics, keywords, app id and icon color |

The command plan is generated: edit [docs/commands-plan.src.txt](docs/commands-plan.src.txt) and run `python3 scripts/gen-plan.py` (it also checks ids, origins, shortcut conflicts and the metadata file). It needs only Python 3.10 or later.

## Project language

The interface, code comments and documentation use American English.

## License

[MIT](LICENSE). Copyright (c) 2026 Paul D Pruitt.

## Legal

Anne's Keep is an independent, clean-room project released under the MIT License. It is not affiliated with, endorsed by, or sponsored by Adobe, Microsoft, the makers of any other program named in this repository, any archive, library or standards body, or any AI provider. Product names appear only to describe file-format compatibility or to say what Anne's Keep is not (nominative use); they are trademarks of their owners. The interface, icons, templates, sample holdings and text will be original or openly licensed. See [docs/LEGAL.md](docs/LEGAL.md).
