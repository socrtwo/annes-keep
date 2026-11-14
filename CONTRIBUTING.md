# Contributing to Anne's Keep

Thank you for your interest. Anne's Keep is at the **planning** stage: there is no code yet. The most useful contributions now are:

- **Feedback on the concept and the plan:** missing commands, commands in the wrong place, status or risk rules that give a wrong answer in a situation you know, and corrections to [docs/ORIGINALITY.md](docs/ORIGINALITY.md), [docs/AI-PLAN.md](docs/AI-PLAN.md), [docs/ARCHITECTURE-PLAN.md](docs/ARCHITECTURE-PLAN.md) or [docs/FORMATS-PLAN.md](docs/FORMATS-PLAN.md). To change commands, edit [docs/commands-plan.src.txt](docs/commands-plan.src.txt) and run `python3 scripts/gen-plan.py`; it fails on duplicate ids, unknown origin codes and shortcut conflicts. Open an issue with the *Feature request* template.
- **Knowledge of the work:** if you are an archivist, a records manager or a librarian, if you recover data, or if you have had to sort out the files someone left behind, tell us how you do it and what the plan gets wrong. Describe practices in your own words; do not paste text from standards, manuals or textbooks.
- **Facts about formats:** whether a format's specification is published and where, what reads it, what it depends on. Give a date and say how you know. Do not paste entries from another register.
- **Test cases:** small made-up sets of files that show a problem: a conversion that drops something, a file that is not what its extension says, a pair of copies of which one is damaged. Do not attach other people's private files, real financial or medical records, or files you do not have the right to share.

## Ground rules

- **Clean room.** Do not contribute code, text, templates, sample data, menu text or icons copied from proprietary software, its documentation or its help files. Work from public specifications, permissively licensed open-source references and your own knowledge. See [docs/LEGAL.md](docs/LEGAL.md).
- **Generic names.** Use the generic terms in docs/LEGAL.md (holding, item, copy, place, rendition, risk…) in the interface and code. Do not use the name of a standard as a claim about the app's output.
- **No missing commands.** Every feature is a command in the registry with an id, label, icon, tab and group (or *not in tabs*), so that it can go on the Quick Access Bar, custom tabs, the menu bar, shortcuts and macros and be found by command search.
- **Items are never written.** Nothing changes an item's file. Anything that converts or repairs a file writes a new file.
- **Nothing is deleted without a person, a count and a record.** Only *Remove Released Files* deletes item files, and only after *Release*.
- **Status is computed.** No command may set Sound or Secured directly; they follow from the checks.
- **A conversion counts only when it is compared.** A new writer for a rendition comes with its comparator and with test files that show what it loses.
- **A risk states its facts.** A new risk rule names the facts it rests on and the commands that would reduce it.
- **AI proposes; checks and people decide.** No AI command writes, moves, converts or deletes a file, and every AI result that can be tested passes its gate in docs/AI-PLAN.md before it is shown.
- **The app's own files pass its own tests.** Anything written at a place or in a packet must be readable with a text editor, a web browser or an unzip tool.
- **American English** in the interface, code comments and documentation.
- **Licenses.** Contributions are accepted under the MIT License. New dependencies must use a permissive license (MIT, BSD, Apache 2.0, ISC, public domain, SIL OFL for fonts).

## Checks

```bash
python3 scripts/gen-plan.py          # regenerate docs/COMMANDS-PLAN.md and docs/commands-plan.json
python3 scripts/gen-plan.py --check  # validate the plan and AnnesKeep.meta.json
```

Python 3.10 or later, standard library only. When the application scaffold arrives (milestone M1), it will use Node.js and the same `npm run dev`, `npm test`, `npm run typecheck` and `npm run build` commands as the sister apps.
