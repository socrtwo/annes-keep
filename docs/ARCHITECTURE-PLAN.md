# Architecture plan

> **Plan. There is no code yet.** This is the intended design. It follows the sister apps wherever the job is the same (shell, platform layer, AI providers, recovery) and describes in detail only what is particular to Anne's Keep.

## Layers

| Layer | Contents | Shared with the suite? |
|---|---|---|
| Shell | Command registry, ribbon, classic menu bar, Quick Access Bar, command search, customization, Backstage, macros | Yes |
| Platform | TypeScript, Vite, Capacitor (Android, iOS), Electron (desktop), PWA; file access; keychain; background workers | Yes |
| Readers | One read-only reader per file type, each able to say "this opens", "this opens in part" or "this does not open", and to hand out text, pages, pixels, cells, rows or playing time for comparison | Reuses the suite's document, workbook, PDF, picture, mail, database and GEDCOM readers |
| Writers | The sister apps' writers, called to make renditions | Yes |
| Holding engine | Catalog store, journal, fingerprints, format identification, the format register, risk rules, status rules, places and copies, audits | New |
| Comparators | One per kind of content, for the Sameness Check | New |
| Views | Shelf, Item, Risk Board, Copy Map, Calendar, Lineage, Timeline, Folder | New |
| Reports | Finding aid, item list, format guide, handover packet, deposit package, condition and audit reports | New, writing through Anne's Pen, Grid, Folio, Loom and Chart |
| AI | Provider adapters, setup wizard, ensemble, history; the three gates | Adapters shared; the gates are new |

Everything runs on the device. There is no server component; the optional suite relay (a shared holding) is a stretch goal.

## The holding is a catalog, not a container

Anne's Keep does not swallow files. Items stay where they are, on whatever disks they are on, and the holding records them. This is deliberate: a preservation tool that had to be opened to reach the files would itself be the single point of failure it warns about. Three consequences:

- Every copy at every place is an ordinary file in an ordinary folder that any computer can read.
- Every place carries a plain-text manifest (below) and a copy of the catalog as text, so that nothing depends on the `.keep` file surviving.
- If Anne's Keep disappeared, the files, their fingerprints and their descriptions would still be there, in formats that pass its own Stranger Test.

## The holding file (`.keep`)

A ZIP container, so that a holding can be inspected and repaired with ordinary tools:

```
holding.sqlite       items, parts, places, copies, renditions, risks, descriptions, rules, audits, events
journal/             append-only change log, one small file per session
register/            the format register in use (a dated copy), with the user's corrections
derived/             extracted text, thumbnails, the search index; can be rebuilt
manifest.json        format version, policy, hash list of the entries above
```

## What is written at each place

```
<place root>/
  ...the copies, in the folder layout the user chose...
  KEEP/
    manifest-sha256.txt     one line per file: the SHA-256 in hexadecimal, two spaces, the relative path
    catalog.json            the descriptions, arrangement, events and policy for what is stored here
    catalog.txt             the same, as readable text
    README.txt              what this folder is and how to check it by hand
```

The manifest uses the line format of the common checksum tools, so that a copy can be verified on any system without Anne's Keep. `README.txt` says so and gives the commands. *Save Catalog to Every Place* (`file.saveEverywhere`) refreshes these files at every place that can be reached.

## Data model

| Record | Key fields |
|---|---|
| **Item** | id, reference number, kind (file, group, thing with no file), group it belongs to, description fields, preservation copy, status, keep-until, hold, restriction, confidential flag |
| **Part** | id, item id, relative path, size, file dates, byte hash, content hash, identified format and version, the rule that identified it |
| **Place** | id, name, kind of medium, where it is, who can reach it, away from home or not, date into service, service life set for it, last verified, state (in service, retired, lost) |
| **Copy** | part id, place id, path at the place, written at, verified at, result of the last verification, state (good, damaged and set aside, gone) |
| **Rendition** | id, item id, made from (a part or another rendition), purpose (lasting format, plain text, page pictures, reading copy, repaired), tool and version, comparison result, Loss Statement, accepted by and when |
| **Risk** | id, item id, kind, level (High, Medium, Low), the facts it rests on, commands that would reduce it, state (open, reduced, accepted with reason, closed) |
| **Rule** | the policy: copy rule, audit interval per place, lasting formats per kind of content, which risks are High; retention rules |
| **Audit** | id, when, who, places covered, files read, differences found, actions taken |
| **Event** | id, when, who, kind (take-in, identification, fixity check, copy written, copy verified, heal, rendition made, comparison, repair, description change, release, transfer), subject, outcome, tool and version |

The Event table is the permanent history of what was done to each item. Its shape follows the general idea of preservation event records in the published preservation-metadata standards; it is implemented from the public documents and claims conformance to none of them.

## Fingerprints

Two hashes for each part:

- **Byte hash:** SHA-256 of the file's bytes. This is what the manifest holds and what the Fixity Check compares. It is computed in a streaming background worker, so that files larger than memory can be hashed and a long run can be paused and resumed.
- **Content hash:** a hash of the content as the reader extracts it (the text, the page pictures, the cell values, the decoded pixels or samples), independent of the container. Two files with the same content hash and different byte hashes are *likely duplicates* (the same picture re-saved, the same document re-zipped) and are shown as such. They are never treated as identical.

Only the byte hash decides that two files are the same. *Release Duplicates* requires equal byte hashes, computed again at that moment from the files as they are now.

## Format identification

A file is identified by content: signature bytes at stated offsets, then the container's structure (for example, a ZIP whose entries make it a word-processor document, a workbook or an e-book), then the format's version. The file extension is recorded and compared (`assess.extension`) and never decides. The rule that matched and the alternatives considered are kept with the part and shown by *Show Identification Data*.

The identification rules and the format register are data files in the repository, written for this project and openly licensed. Each register entry holds dated facts about a format:

| Fact | Used by |
|---|---|
| Is the specification published, and where | Format Risk; Format Guide |
| Is it an open standard, a published vendor format or undocumented | Format Risk |
| Are there independent readers, and is one of them in the suite | Format Risk; Open Check |
| Is the content compressed, and is the compression lossy | Format Risk; rendition planning |
| Can it hold a password, encryption or usage restrictions | Lock Check |
| Can it refer to fonts, files or web addresses outside itself | Dependency Check |
| Can it be read with a text editor, a web browser or an unzip tool | Stranger Test |
| When was it introduced, and is the last program that wrote it still available | Format Risk; Help ▸ How Long Things Last |
| Identifiers for the same format in public registers | export; cross-reference only |

Every fact has a date and an origin. A user's correction is kept beside the shipped value and wins in that holding. The register is not a prediction; it holds facts, and the rating rules that use them are few and printed in Help.

## Risk rules

Each risk rule is a pure function from the facts about an item (its parts, formats, copies, places, renditions and the register) and the policy to zero or more findings. A finding has a kind, a level, the facts it rests on in words, and the commands that would reduce it. Rules do not use AI and do not change the holding.

| Risk kind | Found by | Reduced by |
|---|---|---|
| Format at risk | Format Risk | a verified rendition in a lasting format; or acceptance |
| Does not open, or opens in part | Open Check, Structure Check | Repair Item; Heal from Another Copy |
| Locked | Lock Check | recording where the key is kept; an unlocked rendition made by the owner |
| Depends on something outside itself | Dependency Check | Embed What It Depends On; Group as One Item |
| Too few copies, media or places | Copy Rule Check | Send Copy To; Complete the Copy Rule |
| Copy not verified within the interval | audit schedule | Verify Place |
| Medium past its service life | Media Age Check | Move Copy; Retire Place |
| Name unsafe on other systems | File Name Check | Make File Names Safe (on renditions and copies) |
| Everything rests on one thing | Single Point Check | another place; a second key holder |
| Undescribed | Description Check | Description |
| Incomplete group | Completeness Check | finding the missing part; a note that it never existed |

A person can **accept** a risk with a written reason. An accepted risk no longer lowers the status, is listed in every Condition Report, and is shown again at every audit.

## Status rules

Status is computed, not typed. The rules are small and will be covered by tests before any interface is built, because they are the product. They are applied in this order; the first that fits gives the status.

| Status | Rule |
|---|---|
| Released | A person released the item, with a reason |
| Missing | No copy of the preservation copy can be found at any place that is in service |
| Damaged | Copies can be found, and none of them matches its fingerprint or opens |
| Unassessed | The format is not identified, or the checks have not been run since take-in |
| At Risk | An intact copy exists, and at least one open risk is High |
| Stale | No open High risk, and either a verification or audit is overdue, or a file has changed since it was last fingerprinted |
| Watch | An intact copy exists, and the only open risks are Medium or Low |
| Sound | No open risk: it opens, the copy rule is met, and every counted copy was verified within its interval |
| Secured | Sound, and the preservation copy is in a format the policy names as lasting, or a rendition in such a format has passed the Sameness Check or has an accepted Loss Statement |

Further rules: a group's status is the worst status among its members; a copy at a place that could not be reached at the last audit counts as unverified, not as missing, until *Report Lost Place* is run; a thing with no file can be Sound when its location was confirmed within the interval, and can never be Secured.

A person can release an item, accept a risk or a loss, and set which file is the preservation copy. A person cannot set Sound or Secured directly; they follow from the checks.

## The Sameness Check

One comparator per kind of content. Each is a pure function from an original and a rendition to a list of differences, and each difference has a place, a kind and a size. None uses AI.

| Content | What is compared |
|---|---|
| Text documents | The words in reading order; the count of pages, headings, tables, footnotes, pictures and comments; tracked changes present or flattened; fonts named and fonts embedded |
| Page-faithful documents | The above, plus each page rendered and compared as a picture within a stated tolerance |
| Workbooks | Every cell's value; every formula's result recomputed; the count of sheets, names, charts; number formats that change what is displayed |
| Pictures | Dimensions, color depth and profile; pixels exactly for lossless targets, and by a stated measure for lossy sources; the embedded details carried over |
| Sound | Playing time, channels, sample rate; samples exactly for lossless targets |
| Tables and databases | Tables, columns and types; row counts; a hash of each table's rows in key order |
| Mail | Message count; headers; body text; attachments by byte hash |
| Family tree files | Persons, families, events and source citations by count and by content |
| Web captures | Pages captured; text; pictures by byte hash |
| Plain-text renditions | That every word of the original's text is present, in order |

The result is **Same** (no difference), **Same in content** (differences only in things the policy says do not matter, listed), or **Different**, with a **Loss Statement** that lists each difference in plain words. A rendition with a Loss Statement counts toward Secured only when a person accepts it (`rendition.acceptLoss`), and what was accepted is stored with the rendition.

*What Would Be Lost* (`rendition.lossPreview`) is a different thing: the known limits of a target format, read from the register before any conversion runs.

## Places, copies and audits

- **Writing a copy** is three steps: write, read back from the place, compare with the byte hash. A copy counts only after the third.
- **Verifying a place** hashes what is there and compares it with the manifest and the catalog. It can run on any device the place is attached to. The result returns to the holding the next time the two are together, or by *Record Outside Check*.
- **Healing** replaces a damaged copy with a verified intact one from another place. The damaged file is renamed and set aside at the place until the user removes it; it may be the only copy of some part of the content.
- **The copy rule** is a small expression: at least *n* good copies, on at least *m* kinds of medium, with at least *k* at places marked away from home. The default is 3, 2 and 1. *Complete the Copy Rule* solves for the fewest writes that satisfy it with the places available.
- **An audit** verifies every place that is due, runs the risk rules again, shows the accepted risks again, and writes one Audit record. Reminders go through Anne's Post or the system calendar. The app never assumes that a reminder was seen: an overdue audit turns the affected items Stale.
- **Recovery records** (optional, later): error-correcting data stored beside a copy, written from the published mathematics, from which limited damage can be repaired when no other copy is at hand.

## Platform limits

Stated here so that the plan does not promise what a platform will not allow:

- **Desktop builds** (Electron) can read any folder and drive the user can, make disk images, and run scheduled audits from the command line.
- **Android and iOS** reach only the folders the system's file picker grants, and removable drives only where the system exposes them. Long hashing runs depend on the system allowing background work.
- **The web build** uses the browser's folder access where the browser has it, and otherwise works on files the user selects one batch at a time. It cannot verify a place by itself on a schedule.

A holding made on one platform opens on all of them. What a platform cannot reach is shown as "not reachable from this device", never as missing.

## Journal and history

Every change to the holding is one journal entry: who, when, what, before and after. Undo, History, Versions, Compare Holdings, the Change Report and the Checked sign-off (which clears when later entries touch the item) are all views of the journal. Events are the subset of the journal that describes what was done to an item's files; they are never undone, only followed by further events.

## Repair

- **A damaged item** is handed to the recovery engine of the sister app for its type. The repaired file is added as a rendition with the purpose *repaired* and a Repair Report; the damaged original stays, and its status stays Damaged until a person sets the repaired file as the preservation copy.
- **A damaged copy** with an intact copy elsewhere is healed, as above.
- **A damaged holding:** the ZIP is salvaged entry by entry (the suite's ZIP salvage). If `holding.sqlite` is unreadable it is rebuilt by replaying `journal/`. If the journal is also gone, the holding is rebuilt from the `KEEP/catalog.json` files at the places that can be reached, newest first, and the user is told which changes since then are lost. *Open and Repair* writes a new file and a repair report.

## The AI gates

Three functions with no model in them, used by the AI commands that propose something testable: the identification gate (try the app's own reader for the guessed format), the catalog gate (look for the proposed date or name at the named spot in the item), and the decoding gate (decode with the proposed character set and test the result). Proposals that fail never reach the interface. See [AI-PLAN.md](AI-PLAN.md).

## Accessibility and languages

Status is shown by a mark and a word as well as a color. All panes work by keyboard and expose their structure to screen readers. File names and descriptions may be in any script and direction. The interface is written in American English first, with the suite's translation mechanism. The plain-text files written at each place and in the Handover Packet are UTF-8 with no markup, so that they read aloud and print without a program.
