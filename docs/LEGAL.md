# Clean-room, trademark, privacy and licensing notes

This file records how Anne's Keep stays clear of other vendors' trademarks and copyrights, what it does and does not promise, and how it treats private information. It follows the practice of the other Anne's Office apps. It is not legal advice.

## Clean room

- Anne's Keep is not modeled on any one program. Its command set comes from long-standing practices (archival arrangement and description, digital preservation, backup, records management, library cataloguing, data recovery, estate inventories), described in the project's own words. See [ORIGINALITY.md](ORIGINALITY.md).
- No code, text, templates, sample data, icons, dialog layouts or help content are copied from any other program, including the programs named in ORIGINALITY.md as nearest relatives.
- File formats are identified and read from public specifications and through the sister apps' readers. Undocumented formats are not reverse engineered from leaked or decompiled code. Where a format has no public description, Anne's Keep keeps and fingerprints the file and says that it cannot open it.
- The format register and the identification rules are written for this project. Public format registers are cited by identifier, for cross-reference. None of their content is copied unless and until its license is confirmed to allow it (an open item in [ROADMAP.md](ROADMAP.md), M0).
- No usage restrictions are circumvented and no passwords are recovered. Protected files open only with their password. The Lock Check reports protection as a risk; it does not remove it.

## Generic terms

The interface uses ordinary descriptive words: holding, item, copy, place, rendition, risk, fingerprint, manifest, audit, release, handover packet, finding aid. Where a trade, a standard or a vendor has its own term, the generic word is used:

| Avoided | Anne's Keep term |
|---|---|
| Names of preservation and records standards used as claims ("compliant", "conformant", "certified") | "common practice", described in plain words in *Help ▸ Common Practice* |
| The name of an archival PDF standard for output that has not been validated against it | "prepared for archiving", as in Anne's Folio |
| "Permanent", "forever", "guaranteed", "future-proof" | lasting format (a stated, limited meaning; see FORMATS-PLAN.md); Sound, Secured (statements about checks that passed, nothing more) |
| "Backup" as a name for what the app does | copy, place, copy rule; "backup" only for other programs and for the practice |
| "Trusted repository" and similar titles | not used |
| "Secure erase", "shred" | Remove Released Files (which deletes files and does not claim that they cannot be recovered) |
| "Will", "bequest" | Wishes (and the packet says that it is not a will) |
| Assistant brand names | AI tab, AI menu |

## What the app does not promise

- **It does not guarantee that anything survives.** A status describes what the checks found the last time they ran. Media fail without warning, formats are abandoned, and a copy that verified last month can be unreadable today. Sound and Secured mean that the stated checks passed on the stated date.
- **It is not a backup service and stores nothing itself.** Every copy is on storage the user provides. If the user has one copy, the app says so; it cannot make the second one without somewhere to put it.
- **A rendition is not the original.** The Sameness Check compares the things listed for it in ARCHITECTURE-PLAN.md and nothing else. A rendition reported Same may still differ in ways the comparison does not test. The original is always kept unless a person releases it.
- **The format register is not a prediction.** It records dated facts about formats, and the rating is a simple rule over those facts.
- **It is not professional advice or certification.** The templates describe common practice. Using them does not make a holding conform to any archival, preservation, records-management or legal standard, and the app says so in each template.
- **It states no legal retention period.** How long a tax, employment, medical or corporate record must be kept depends on the jurisdiction and the circumstances. Retention rules are entered by the user, who should ask a qualified adviser. The app ships with none.
- **Removing files is not secure erasure.** *Remove Released Files* deletes files through the operating system. On most media the data can be recovered afterward with the right tools. The Release Record says what was removed, not that it is unrecoverable.
- **Wishes is not a will.** The Handover Packet is a practical guide. It has no legal effect, and it says so on its first page. It does not transfer ownership, accounts or rights.
- **The Keys and Passwords Note holds whereabouts, not secrets.** It records that an item is locked and where its key is kept. Passwords belong in a password manager or with a trusted person.
- **AI output is labeled and decides nothing.** See [AI-PLAN.md](AI-PLAN.md).

## Private information and the rights of other people

A holding often contains other people's information: family letters, a parent's papers, an office's correspondence, mailboxes with messages from many senders.

- Everything stays on the device and on the places the user chooses, unless the user exports, sends or runs an AI command.
- Items can be marked **confidential**; they are left out of handover packets unless the user includes them one by one, and out of all AI requests.
- *Restrict Until* records that an item is not to be opened or passed on before a date or an event. It is a recorded instruction shown to whoever opens the holding or the packet; it is not encryption.
- *Living People* and *Sensitive Patterns* find details to leave out of what is shared. The living-person rule follows the suite's GEDCOM privacy filter (Anne's Chart). The pattern rules run on the device.
- **Files held for someone else** (`intake.thirdParty`, `file.newEstate`): the user is responsible for having the authority to hold, open, copy or release them. The accession and custody records exist so that this can be shown later.
- **Mailboxes and account exports** contain other people's messages. Keeping one's own copy is ordinary; passing it on in a packet or a deposit may need care, and the packet builder says so when mail is included.
- **Capturing a web site** saves a copy for the user's own keeping. Redistributing someone else's pages may need the publisher's permission.
- **Copyright does not lapse because a file was preserved.** Making renditions for one's own continued access is the purpose of this app; the user is responsible for what the law that applies to them allows, and for what a receiver may do with a handed-over copy. *Rights and Restrictions* records what the user knows.

## Nominative use

The documentation names other products (Adobe Acrobat, Photoshop, Illustrator, InDesign, Premiere, After Effects, Lightroom, Bridge, Media Encoder, DNG Converter, Digital Editions, Experience Manager, Creative Cloud, Content Authenticity, Firefly and Adobe's other products; Microsoft Word, Excel and PowerPoint; Archivematica, Preservica, Rosetta, DROID, Siegfried, JHOVE, veraPDF, MediaInfo, PRONOM, Fixity, Bagger, Time Machine, File History, restic, Borg, Duplicati, PAR2, LibreOffice, pandoc, ImageMagick, FFmpeg, BitCurator, ePADD, Webrecorder, digiKam and others) only to identify file formats, to say what Anne's Keep is *not*, or to let readers compare. This is nominative use; it implies no affiliation, sponsorship or endorsement. The names are trademarks of their respective owners; Adobe and the Adobe product names are trademarks of Adobe Inc., and Microsoft, Word, Excel and PowerPoint are trademarks of Microsoft Corporation.

## Third-party components (planned)

The final list will be generated from `package.json` into a third-party notices file at build time, as in the sister apps. Only permissive licenses are accepted in the base app (MIT, BSD, Apache 2.0, ISC, public domain, SIL OFL for fonts). Each entry below is to be confirmed in M0.

| Component | License |
|---|---|
| SQLite (WASM build, with FTS5) | public domain |
| The platform's own cryptography (Web Crypto, Node crypto) for SHA-2; a permissively licensed streaming SHA-256 where the platform has none | platform; MIT or similar |
| JSZip or a comparable ZIP library | MIT |
| pdf.js (page rendering, as in Anne's Folio) | Apache 2.0 |
| Tesseract.js (OCR, as in Anne's Folio) | Apache 2.0 |
| ONNX Runtime Web, Transformers.js | MIT, Apache 2.0 |
| Material Symbols | Apache 2.0 |
| Capacitor, Electron, electron-builder | MIT |
| The sister apps' readers, writers and recovery engines | MIT (the suite's own) |
| On-device models | each model's own license, shown before download; permissive only |
| The format register and identification rules | written for this project; to be released under a public-domain dedication or a permissive data license |

**Not used:** GPL, LGPL or AGPL code in the app's builds (which rules out bundling the common video converters and the common parity tool; see FORMATS-PLAN.md and the stretch goals in ROADMAP.md); non-commercial-only model weights; format-register content copied from a source whose license has not been confirmed.

## Online services

Anne's Keep works offline. Online services are called only when the user invokes the matching command: Capture Web Site (the site itself), cloud folders registered as places (through the device's own access to them), the chosen AI services (AI tab), model downloads, and update checks (desktop and APK builds, opt-in). Verifying a cloud place means downloading what is there in order to hash it; the app states the amount first.
