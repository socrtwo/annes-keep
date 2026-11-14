# AI plan

> **Plan. There is no code yet.** This document fixes what the **AI** tab and the **AI** menu will do, which services they use, and the rules for accuracy, privacy and cost. The AI menu is the same list of commands in the classic menu bar; anything said here about the tab applies to the menu. Command ids are in [COMMANDS-PLAN.md](COMMANDS-PLAN.md#ai).

The AI tab is optional. Anne's Keep is complete without it, and nothing is sent anywhere until you run an AI command. Every AI command is an ordinary command: it can go on the Quick Access Bar, on a custom tab, in the menu bar, on a shortcut or in a macro.

## The rule: the AI may describe and suggest; only a computed check counts, and only a person lets go

This app exists so that files outlast the people and programs that made them. A language model is fluent and can be confidently wrong, including about what a file is, what a conversion lost and what is safe to delete. A preservation tool that let a model's word decide any of those would put the files at the mercy of its mistakes. So:

1. **AI never touches a file.** No AI command changes, moves, renames, converts, repairs, copies or deletes an item, a copy or a rendition. AI commands write only proposals: draft descriptions, suggested groups, suggested next steps.
2. **AI never decides what is the same and never decides what may go.** Duplicates are found by fingerprint. A rendition is compared with its original by the Sameness Check, which has no model in it. *Release* and *Remove Released Files* are run by a person, and the output of an AI command can never start them.
3. **AI does not set status and does not rate risk.** Status and risk follow from the checks in the Assess tab and the facts in the format register. *Explain This Risk* and *Explain Loss Statement* restate a computed result in plain words; they cannot change it and add no facts to it.
4. **What can be tested is tested before it is shown.** Three gates, each an ordinary function with no model in it:
   - **The identification gate.** *Guess Unidentified Format* proposes what a file might be. The app then tries its own reader and structure check for that format. Only if the file really opens as that format is the identification recorded, and it is recorded as "identified by structure", with the guess noted as how the app came to try it. A guess that fails is discarded and counted in AI History.
   - **The catalog gate.** *Suggest Dates* and *Suggest People and Places* must return, with each value, the spot in the item where it is written and the exact words there. The app looks at that spot through the same reader the interface uses and checks that the words are there. A value that is not found is dropped. A date or a name that a model inferred rather than read is not offered by these commands at all.
   - **The decoding gate.** *Suggest Text Encoding* proposes a character set for garbled text. The app decodes with it and checks that the result is valid in that character set and decodes without replacement characters. The bytes of the item are never changed; the encoding is recorded as a note about how to read them.
5. **AI writing is labeled and kept apart.** A drafted description sits beside the description fields, marked as AI-written, until a person accepts it. An accepted draft is recorded as accepted by that person and as having begun as an AI draft. Summaries, picture descriptions, transcriptions and translations are stored as aids and are always labeled.
6. **Answers come from the holding.** *Ask the Holding* answers only from the catalog and from the text of the items. Each sentence of the answer names the items it rests on, and a sentence that rests on none is not shown. "Not in this holding" is a normal, expected answer.
7. **Opinions are labeled as opinions.** *Explain This Format* and *Suggest Repair Route* draw on a model's general knowledge. Their output is marked as such, goes to notes or to-dos, and never enters the format register, which holds only dated facts with their origin.

## What the AI tab does

| Group | Commands | What is sent (default) |
|---|---|---|
| **Ask** | Ask the Holding, Explain This Format, Explain This Risk, Explain Loss Statement | the question and the catalog entries and passages that the on-device search selected; for the Explain commands, the format's register entry, the risk's facts or the Loss Statement |
| **Describe** | Draft Description, Suggest Dates, Suggest People and Places, Describe Picture, Transcribe, Summarize Item, Translate Description | the item, page or picture you chose; for Translate, the description text only |
| **Sort** | Suggest Arrangement, Suggest What Belongs Together, Find Related Items, Suggest Record Types, Screen for Private Information | file names, folder paths, formats, dates and existing descriptions; Find Related Items and Screen for Private Information run on the device only and send nothing |
| **Rescue** | Guess Unidentified Format, Suggest Repair Route, Suggest Text Encoding, Read Media Label | the file's name, size, first bytes and readable strings (Guess); the Damage Report (Suggest Repair Route); a sample of the garbled bytes (Encoding); the photograph of the label |
| **Write** | Draft Finding Aid Introduction, Draft Format Guide, Draft Handover Letter, Draft Rendition Plan, Draft Condition Summary, Run on Selection | descriptions; register entries; the points you listed; the list of formats in the selection and the conversions the app offers; computed statuses and risks |
| **Providers** | Set Up AI, Providers and Models, Active AI, AI and Privacy, Several AIs, Choose AIs, Show AI Discussion, AI History, Stop AI, Delete Downloaded Models | nothing |

### Guess Unidentified Format in detail

1. The app's own identification (`assess.identify`) has already failed for this file. It needed no service.
2. The file's name, extension, size, dates, its first and last bytes in hexadecimal, a list of readable strings found in it, and the names of the files beside it go to the text model, with instructions to return, as structured output, up to five candidate formats in order, each with the reason.
3. **The identification gate:** for each candidate the app has a reader or a structure check for, it tries it. The first candidate that opens is recorded.
4. If a candidate is plausible but the app has no reader for it, the candidate is shown as an *unconfirmed suggestion* in the Unidentified Files list, labeled as an AI opinion. The item stays Unassessed.
5. If nothing survives, the pane says so and offers *Recover Text Only*.

### Draft Description in detail

The app first fills what it can without a service: embedded details, dates and names from file names, and extracted or recognized text. *Draft Description* then proposes a title and a few sentences. The draft is shown beside the fields with the passages it was drawn from. Fields that hold a fact which can be read in the item (a date written on a letter, a name in a caption) go through the catalog gate; free-text description cannot be tested and stays labeled as AI-written until a person accepts or rewrites it. The command never fills rights, restrictions or keep-until dates.

### Draft Rendition Plan in detail

The model is given the list of formats in the selection, the holding's lasting-format choices and the list of conversions the app can perform, each with its known losses. It may only arrange those conversions into a plan; a step naming a conversion the app does not offer is dropped. The result is a plan like one a person would write with *Rendition Plan*. Nothing runs until a person runs it, and every rendition then goes through the Sameness Check like any other.

## Setting up

**AI ▸ Set Up AI** is the suite's wizard. It

1. lists services grouped as *Free · on device*, *Free · your computer* (Ollama, LM Studio, llama.cpp server and other OpenAI-compatible local servers), *Free tier*, *Free trial* and *Paid*;
2. links to each service's key page and checks the key with a tiny test request;
3. fetches the service's model list where one is published, so that models are chosen by name and not from a list frozen into the app;
4. shows what each command will send and, for paid services, links to the current price page.

Service terms, free tiers and model names change often; the wizard links to each service's current pages and does not promise limits or prices.

### Services (planned adapters)

The suite's shared adapters: Anthropic, OpenAI, Google Gemini, Mistral, Groq, OpenRouter, Azure OpenAI, AWS Bedrock, and any OpenAI-compatible endpoint (which covers the local servers). Structured output (JSON schema or tool calling) is required for every command that passes a gate; a service that cannot return it is not offered for those commands. Describe Picture, Transcribe and Read Media Label need a model that accepts images.

## On the device

Small models run in the app (ONNX Runtime Web or Transformers.js; WebGPU where available, WASM otherwise) for:

- **the search index** (embeddings of descriptions and extracted text), so that *Find Related Items* works with no service and *Ask the Holding* sends only the few entries and passages it needs;
- **Screen for Private Information**, which must work with no service at all;
- an optional small text model for simple drafts when no service is set up.

Each model's license is shown before download, and only permissively licensed weights are offered (see [LEGAL.md](LEGAL.md)). *Delete Downloaded Models* removes them.

## Several AIs

The text commands can use the suite's ensemble modes (one AI combines the others' answers, or the AIs deliberate until they agree), as specified for the suite in [Anne's Base's ENSEMBLE.md](https://github.com/socrtwo/annes-base/blob/main/docs/ENSEMBLE.md). In Anne's Keep, each member's proposals pass the gates separately, and the pane shows which members proposed each one. Agreement among models is shown as information. It is not a check, and it never changes a status or a risk.

## What the app will not do

- Let any AI command change, move, convert, repair, copy or delete a file.
- Release an item, remove a copy or reduce the number of copies on a model's suggestion.
- Treat two files as duplicates because a model said they are alike.
- Record a format identification that the app's own reader did not confirm.
- Show a suggested date or name that the app could not find written in the item.
- Name a person from a face. *Describe Picture* describes what is visible; names come only from writing in or with the item, or from a person.
- Accept a rendition, a loss or a risk on a person's behalf.
- Put a model's general knowledge into the format register.
- Fill a gap. If a word, date or figure is unreadable, AI transcription marks it unclear; it does not supply a likely value. A repaired file never contains text that a model reconstructed.
- Send an item marked **confidential**, or any part of it or of its description, to any service. Such items are skipped by every AI command, including the on-device index that feeds them.
- Send the contents of a password-protected holding to any service unless that holding's own setting allows it.
- Send the Keys and Passwords Note, the Wishes or the People to Contact list to any service, under any setting.

## Privacy and keys

*AI and Privacy* (`ai.privacy`) is set for the holding, and can be tightened for a group or an item, with **Descriptions only** as the default: commands send file names, formats, dates and catalog text, never the files. **Excerpts** (the passages a command needs) and **Whole items** (needed for Transcribe, Describe Picture and Draft Description of an undescribed item) are asked for when a command needs them. Each group and each item can also be set to *never send*.

Keys are stored in the platform keychain (Android Keystore, iOS Keychain, Windows Credential Manager, macOS Keychain, libsecret on Linux; on the web, encrypted in the browser with a passphrase), never in the holding file or in exported settings. **AI History** (`ai.history`) records, for each holding, what was sent, to which service, what came back, and how many proposals the gates discarded; it can be cleared.

## Cost

Before a command that covers many items runs, the app states how many requests it will make. Paid services charge for each; with Several AIs, each member is a separate request. A holding can have tens of thousands of items, so the batch commands always state the count first and can be stopped and resumed.
