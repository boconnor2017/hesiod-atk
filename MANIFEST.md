# Hesiod ATK — Repository Manifest

This manifest is the standing specification for initializing a **Hesiod ATK (Architecture Toolkit)** repository. Whenever a new Hesiod ATK project is started, the AI model reads this manifest and reproduces the structure, naming, and formatting standards below exactly — nothing here is optional or a suggestion to adapt per-project unless the human accountable for the project explicitly asks for a deviation.

The current reference instance built from this manifest is `hesiod-atk-9.1.1`. The release number (`x.y.z`) changes over time; treat every occurrence of `x.y.z` below as "the current release number for this toolkit," not a fixed value.

---

## 1. Purpose

The Hesiod ATK repository is where the AI model, acting as draft technical writer, produces the technical artifacts of an architecture engagement across five phases: Discovery, Requirements, Design, Planning, and Governance. This manifest guarantees that every instance of the toolkit — regardless of who initializes it or when — has:

- The same folder structure
- The same file-naming conventions
- The same document header and metadata block
- The same image-linking convention (all images live in-repo; nothing is hotlinked externally)

## 2. Repository naming

The repository root is named:

```
hesiod-atk-<x>.<y>.<z>
```

Example: `hesiod-atk-9.1.1`

`x.y.z` is the release/version number of the toolkit being developed against, not the version of any individual document inside it (see §5 for document versioning).

## 3. Folder structure

Every Hesiod ATK repository has exactly this structure:

```
hesiod-atk-x.y.z/
├── _atkconfig/
├── _release_notes/
├── 01. Discovery/
│   ├── _img/
│   └── _templates/
├── 02. Requirements/
│   ├── _img/
│   └── _templates/
├── 03. Design/
│   ├── _img/
│   └── _templates/
├── 04. Planning/
│   ├── _img/
│   └── _templates/
├── 05. Governance/
│   ├── _img/
│   └── _templates/
└── README.md
```

### Folder purposes

| Folder | Purpose |
|---|---|
| `_atkconfig/` | Shared, repository-wide assets used by every document — most importantly `header.png`, the image used at the top of every template (see §5). Configuration that applies across all phases lives here. |
| `_release_notes/` | Version history for this toolkit instance itself (not for the phase documents). |
| `01. Discovery/` … `05. Governance/` | One folder per toolkit phase, in fixed numeric order. Each phase folder holds the **working documents** for that phase directly at its own root. |
| `<phase>/_img/` | Images referenced by documents in that phase. An image belongs in the `_img/` folder of the phase whose document uses it — never in a different phase's `_img/`, and never referenced by a URL outside the repository. |
| `<phase>/_templates/` | The master template(s) for that phase. Templates are copied out to the phase root (not edited in place) when a new working document is started — see §6. |

Phase folder names are fixed strings, spelled exactly as above, including the two-digit zero-padded number, the period, and the single space before the name: `01. Discovery`, `02. Requirements`, `03. Design`, `04. Planning`, `05. Governance`. Do not add trailing spaces, change numbering, or rename phases.

## 4. Template file naming

Every template file is named:

```
hesiod-atk-<templateName>.md
```

Where `<templateName>` is the lowercase, hyphenated phase name plus `-template`. The five standard templates are:

| Phase | Template path |
|---|---|
| 01. Discovery | `01. Discovery/_templates/hesiod-atk-discovery-template.md` |
| 02. Requirements | `02. Requirements/_templates/hesiod-atk-requirements-template.md` |
| 03. Design | `03. Design/_templates/hesiod-atk-design-template.md` |
| 04. Planning | `04. Planning/_templates/hesiod-atk-planning-template.md` |
| 05. Governance | `05. Governance/_templates/hesiod-atk-governance-template.md` |

Additional templates introduced later (e.g. an ADR template, a meeting-notes template) follow the same convention and are registered in this manifest before being adopted project-wide.

## 5. Document header standard

Every Markdown document produced under this manifest — every template, and every working document created from a template — begins with the following block, and nothing precedes it:

```markdown
![header](../_atkconfig/header.png)

# Hesiod [Document Title]

| | |
|---|---|
| **Version** | 1.0 [DRAFT / INTERNAL REVIEWED / EXTERNAL REVIEWED] |
| **Author** | [Accountable Human] |
| **Role** | [Human Role] |
| **Reviewers** | [List of Human Reviewers] |
| **Date** | [Date] |

---
```

### Why this format

- The header image plus a Markdown metadata table renders as a clean, professional block in any Markdown viewer and converts cleanly to a bordered table in PDF (e.g. via Pandoc), unlike a plain-text or fenced-code metadata block, which most Markdown-to-PDF converters render as an unstyled literal box.
- A horizontal rule (`---`) closes the header before the document body begins.

### Field definitions

| Field | Meaning |
|---|---|
| `[Document Title]` | The document's plain-language title (e.g. "Discovery", "Requirements", "Solution Design"). Follows "Hesiod" in the H1. |
| `Version` | The document's own version number, followed by its review status: `DRAFT`, `INTERNAL REVIEWED`, or `EXTERNAL REVIEWED`. Documents start at `1.0 [DRAFT]`. |
| `Author` | The accountable human who owns the document's content (the AI model drafts; a human is always the accountable author of record). |
| `Role` | That human's role/title on the engagement. |
| `Reviewers` | The human(s) who have reviewed or must review the document. |
| `Date` | The date of the current version. |

### Image path convention in the header

- The header image `header.png` always lives at `_atkconfig/header.png` at the repository root.
- A **template** file lives one level down, in `<phase>/_templates/`, so its header path is `../_atkconfig/header.png`.
- A **working document** created from a template lives directly in `<phase>/` (one level up from the template's original location — see §6), so the same relative path, `../_atkconfig/header.png`, remains correct without editing. This is why templates are written with `../_atkconfig/header.png` rather than `../../_atkconfig/header.png` — the path is written for where the document will live once instantiated, not for the template's own resting place in `_templates/`.

## 6. Images

- All images are stored in-repository. Nothing is linked externally (no hotlinking to external URLs).
- A working document's images live in that phase's `_img/` folder: `<phase>/_img/<filename>`.
- Reference images from a working document (which lives at `<phase>/<doc>.md`) with a path relative to the phase root: `![alt text](_img/<filename>.png)`.
- The one exception is the header image, which is shared repository-wide and lives in `_atkconfig/` (see §5).

## 7. Initializing a new Hesiod ATK repository — the AI model's procedure

When asked to initialize a new Hesiod ATK project, the AI model does the following, in order:

1. **Confirm the release number** (`x.y.z`) for the new instance if it isn't already clear from context, and **capture the project name** the architect provided in the initialization prompt (README §18.2, Step 2) — this is the name used throughout the project per the Project Naming rule (§20).
2. **Create the folder structure** exactly as specified in §3, using the current release number in the root folder name.
3. **Create `README.md`** at the repository root, using the reduced header defined in §18.0 (image only — no title, no metadata table) and the full required structure defined in §18 (About, Quick Start, WARNING, Helpful Hint, plus the Repository Structure and License reference sections). `README.md` always says "Hesiod" regardless of project name (§20).
4. **Create `LICENSE`** at the repository root containing the MIT License text (§10.2).
5. **Populate each phase's `_templates/` folder** with that phase's master template (§4), each containing at minimum the standard header (§5) — with the project name in place of "Hesiod" in the title, per §20 — and the mandatory `# References` footer stub (§10.3). Template bodies beyond the header and References footer are developed separately and adopted into this manifest once finalized — do not invent template body content that hasn't been specified.
6. **Create the release notes file** at `_release_notes/hesiod-atk-x.y.z-release-notes.md` (§12), with the three mandatory sections (What's New, Known Issues, Bill of Materials), the Known Issues architect comment, and the Bill of Materials table populated from whatever templates the repository ships with. The release notes always say "Hesiod" regardless of project name (§20).
7. **Obtain three confirmations from the architect** before initialization is considered complete — this is a hard gate, not an optional courtesy, and README §18.2 (Step 2) tells the architect to expect it:
   - **Header graphic** — confirm whether to update `_atkconfig/header.png` for this project or keep the toolkit default.
   - **License ownership** — confirm the copyright holder/entity to put on the `LICENSE` file (§10.2).
   - **Research guardrails** — confirm the approved reference domains for this project (§10.3) before any AI-assisted research begins. Do not query or cite sources outside that list without explicit permission.
8. **Leave `_atkconfig/` and `_release_notes/` structurally present** — `_atkconfig/` will hold `header.png` and other shared config (added separately since it's a binary asset, and may be updated per the Step 7 confirmation); `_release_notes/` starts empty except for the file created in step 6.
9. **Do not populate `_img/` folders** at init time — they are populated as documents are written and images are added.
10. **Confirm the result** to the person: what was created, where, confirmation that all three Step 7 items were addressed, and what (if anything) is still needed before the templates can be used to draft real documents.

## 8. Using a template to start a working document

When a human or the AI model starts a real document for a phase:

0. Apply the Technical Writing Standard (§19) throughout drafting — it governs the depth and specificity of everything written in the steps below, on top of each document type's required sections (§14–§17).
1. Copy the phase's template from `<phase>/_templates/hesiod-atk-<templateName>.md` to `<phase>/<descriptive-file-name>.md` (directly in the phase folder, not in `_templates/`).
2. Fill in the header fields (§5): title, version/status, author, role, reviewers, date. The title uses the project's name in place of "Hesiod" (§20). An AI model drafting the document sets `Version` to `1.0 [DRAFT]` and never advances it further itself (§10.1).
3. Do not modify the master template in `_templates/` when writing a working document — the template stays clean for future reuse.
4. Any images the new document needs go in `<phase>/_img/` and are linked per §6. If an image is AI-generated, disclose the generating tool per §10.5 and preserve any embedded provenance metadata.
5. Populate the `# References` footer (§10.3) with every source drawn on, restricted to the architect-approved research-domain list.

## 9. Change control for this manifest

This manifest is itself a governed document. Changes to folder structure, naming conventions, or the header standard should be made here first, then propagated to new repository instances going forward. Existing repository instances are not required to retroactively conform unless explicitly migrated.

## 10. Non-negotiable governance standards ("architect in the loop")

The Hesiod ATK exists to accelerate drafting, not to remove human accountability from the artifacts it produces. The following five standards apply to every document produced under this manifest, in every repository instance, without exception. They are guardrails, not defaults — they are not to be relaxed, reworded away, or silently dropped by an AI model acting on this manifest.

### 10.1 AI drafts; the human Author owns

An AI model may be used only to produce a **first draft** of a document. The `Author` named in a document's header (§5) is that document's accountable owner and carries full responsibility for:

- reading and understanding everything the draft contains before it moves past `DRAFT` status,
- conducting or arranging peer review (`INTERNAL REVIEWED` / `EXTERNAL REVIEWED`, per §5),
- and the document's version control going forward.

An AI-drafted document is not considered reviewed, approved, or final merely because it was generated. `Version` status in the header must never be advanced past `1.0 [DRAFT]` by the model itself — only the Author or a designated reviewer advances it.

### 10.2 License

The Hesiod Architecture Toolkit is open source, licensed under the **MIT License**. A `LICENSE` file containing the MIT License text lives at the root of every repository instance (alongside `README.md`). Content and templates produced under this manifest inherit that license unless a specific engagement states otherwise.

### 10.3 Mandatory References section, and domain scope for AI research

Every AI-drafted document must end with a comprehensive list of the sources it drew on, in this exact format:

```markdown
# References
* [Title](URL)
```

Before an AI model does any research for a new project, the **architect must supply a list of acceptable public domains** the model is permitted to query. The model must not pull from, cite, or otherwise use sources outside that approved domain list without the architect's explicit permission. If no domain list has been provided yet, the model must ask for one before researching rather than assuming a default scope. (In practice, the architect typically supplies this list as part of a Discovery scoping document — see §18.2, Step 3 — under a "Reference Guardrails" heading or equivalent.)

Every reference in a `# References` section must point outside the Hesiod ATK toolkit's own published documents. A Requirements, Design, Planning, or Governance document must never cite another document produced under this manifest (e.g. Design citing the Requirements document, or Governance citing Design) as if it were an independent source — doing so makes the References section circular and self-validating, which defeats its purpose. References exist to ground a document in external reality (vendor documentation, standards bodies, published research, etc.), not to point back at the toolkit's own artifacts. Cross-references between the toolkit's own documents belong in the document's body prose (e.g. "as defined in the Requirements document") or in a comment (§11.1), never in the References section.

### 10.4 Data security and confidentiality

The architect operating the AI model is responsible for appropriate data security while using it. Unless the architect states otherwise for a given engagement, the model must assume:

- the AI model is **cloud-based**, and
- prompts and their contents **may be used by the provider for future model training**.

Nothing confidential or proprietary — client data, credentials, unreleased designs, personal data, or anything under an NDA — may be entered into a prompt without the architect's explicit, prior permission. When in doubt, the model should flag the concern and ask rather than proceeding.

### 10.5 AI disclosure and provenance (text and images)

Because these documents carry an "architect in the loop," readers must be able to tell that a draft originated with an AI model rather than mistake it for wholly human-authored, final work:

- **Text:** the `Version` field's `[DRAFT / INTERNAL REVIEWED / EXTERNAL REVIEWED]` status (§5) is itself the primary disclosure mechanism — a document sitting at `DRAFT` signals unreviewed AI-assisted content. Do not remove or obscure this field, and do not backdate or misstate review status.
- **Images and diagrams:** where a document embeds an AI-generated or AI-rendered image (a diagram, a mockup, a banner), note the generating tool/model in the image's alt text or a caption (e.g. `*Diagram generated with the AI model (Sonnet 5).*`), and preserve any provenance metadata the generating tool embeds (e.g. C2PA "Content Credentials," or similar watermarking/metadata standards) rather than stripping it on export or re-save. If the toolchain used to render an image does not support embedded provenance metadata, the caption disclosure above is required in its place.
- This disclosure requirement applies independently of document review status — an image stays marked as AI-generated even after the surrounding document reaches `EXTERNAL REVIEWED`, unless a human materially recreates or redraws it.

## 11. Documentation standards

### 11.1 Comments are an architect-only review channel

The Markdown source of every document is written for the architect, not for reviewers. Reviewers only ever see the PDF the architect exports for internal or external review (§1, §10.1) — they never see the Markdown source or its comments.

Markdown comments (`<!-- like this -->`) are the behind-the-scenes forum for that architect-only layer: notes that need to persist with the document itself rather than living only in a prompt history that gets lost between sessions. Use them for things like open questions for the architect, a rationale the model wants on record, a flag on an assumption made while drafting, or a note on what still needs a citation or a diagram.

Rules:

- Only the AI model or the architect adds comments. A comment is never written as if it were addressed to, or might be seen by, a reviewer.
- Comments must never contain content that belongs in the document body (findings, decisions, references) — they are notes about the document, not part of it.
- Because the architect converts to PDF for review (§1), and standard Markdown→PDF conversion drops HTML comments by default, comments do not need to be manually stripped before export — but the architect should confirm their conversion tool actually drops them before relying on that.
- The `<!-- Document body content goes here. -->` placeholder in each template (§4) is an example of this convention and should be replaced with real body content, or with a real architect-facing note, not left as inert filler.

### 11.2 Minimal formatting

Templates and AI-drafted documents use plain Markdown wherever possible, so the architect isn't cleaning up decorative formatting before a document is ready. Bold, italics, and underline are removed except in the three specific cases below — nowhere else.

**(a) Bold** — removed everywhere except:
  - a figure reference, and
  - the leading summary term of a bullet point.

  ```markdown
  # Figure Example
  **Figure 1** below...

  # Bullet Point Example
  * **Foo:** Bar 1...
  * **Foo:** Bar 2...
  * **Foo:** Bar 3...
  ```

**(b) Italics** — removed everywhere except a reference to an artifact (e.g. another named document or file).

  ```markdown
  # Artifact Example
  As referenced in *This Other Document.docx* section 2b.
  ```

**(c) Underline** — removed everywhere except where Markdown link syntax inherently produces it (i.e. the link itself).

  ```markdown
  # Link Example
  [Hesiod Rocks My Socks](https://github.com/boconnor2017/hesiod)
  ```

No other use of bold, italics, or underline is permitted in Hesiod ATK documents — including for emphasis, headers-within-text, or stylistic effect. Headings carry their own visual weight via Markdown heading levels (`#`, `##`, …) and don't need bold on top of them.

The bolded field labels in the standard header's metadata table (`**Version**`, `**Author**`, etc., §5) are a structural exception: they are fixed table labels, not body prose, and stay bold as specified in §5.

### 11.3 Image storage

Every generated image is stored in the `_img/` folder of the phase it belongs to (§3, §6): a Requirements diagram goes in `02. Requirements/_img/`, a Design diagram in `03. Design/_img/`, and so on for each phase.

The only exception is a global image — one that applies across the whole repository rather than to a single phase's document (e.g. `header.png`). Global images live in `_atkconfig/` (§3), never in a phase's `_img/` folder.

## 12. Release notes

Each Hesiod ATK repository instance carries its own release notes, tracking the state of the toolkit itself (not the architecture engagement's documents).

### 12.1 Location and naming

Release notes live at:

```
hesiod-atk-x.y.z/_release_notes/hesiod-atk-x.y.z-release-notes.md
```

Example: `hesiod-atk-9.1.1/_release_notes/hesiod-atk-9.1.1-release-notes.md`. The release notes file carries the standard header (§5); its `[Document Title]` is "Release Notes."

### 12.2 Mandatory sections

The release notes must contain, at minimum, the following three sections, each as a Markdown H1 (`#`), in this order:

1. **What's New**
2. **Known Issues**
3. **Bill of Materials**

The model may add further H1 sections beyond these three if a release genuinely calls for one, but the release notes are scoped strictly to information about the release itself. They are not the place for instructions, quickstart steps, "hello world" walkthroughs, or any other how-to-use-the-toolkit content — that belongs in `README.md` instead.

As the model updates the toolkit's architecture documents, templates, or structure, it must also update these three sections accordingly, in the same pass, so the release notes stay a living record of release management rather than a one-time snapshot.

#### What's New

A high-level summary of the release: what changed, what was added, and any major bug fixes. Written in plain prose or a bulleted list per §11.2 (bold only for a bullet's leading term, if used).

#### Known Issues

A bulleted list of issues the release is aware of but has deliberately chosen not to address yet (most often due to time constraints or prioritization) — not a place for issues no one has noticed.

This section must always carry the following comment (§11.1) for the architect:

```markdown
<!-- Architect: add known bugs directly to this list as you find them, even between
     formal releases, so the ATK development team has a persistent record to prioritize
     fixes against. -->
```

#### Bill of Materials

A table listing every template shipped with this release, with exactly these four columns, in this order: `Template Name`, `Template Description`, `Template Location`, `Template Type`.

```markdown
# Bill of Materials
| Template Name | Template Description | Template Location | Template Type |
|---|---|---|---|
| Discovery Template | [one-line description] | 01. Discovery/_templates | Markdown |
| Requirements Template | [one-line description] | 02. Requirements/_templates | Markdown |
| Design Template | [one-line description] | 03. Design/_templates | Markdown |
| Planning Template | [one-line description] | 04. Planning/_templates | Markdown |
| Governance Template | [one-line description] | 05. Governance/_templates | Markdown |
```

Add a row for every template that ships with the toolkit, including any beyond the five standard phase templates (§4).

## 13. Discovery folder governance

The `01. Discovery/` folder is the single ingress point for everything downstream — Requirements, Design, Planning, and Governance documents all trace back to what is captured here. That traceability only holds if the Discovery folder's contents are guaranteed to originate from the people who actually hold the requirements, not from the architect or the model reconstructing or paraphrasing them after the fact.

### 13.1 Architect-only, always

The AI model must never write to `01. Discovery/` — not the phase root, not `01. Discovery/_img/`. This is an absolute rule, not a default that can be relaxed for convenience. The one exception is the one-time initial repository scaffold (§7): creating the empty `01. Discovery/`, `01. Discovery/_img/`, and `01. Discovery/_templates/` folders and the header-only Discovery template happens before any real discovery content exists, and is not "writing content" in the sense this rule restricts.

Once a project is underway, populating `01. Discovery/` — raw conversation notes, emails, chat transcripts, meeting recordings' transcripts, or anything else a requirement owner provided — is the architect's job alone. The model may (and should) **read** the Discovery folder's contents to draft downstream documents (§14), but it never creates, edits, or deletes anything inside it.

### 13.2 Every requirement needs two elements

Whatever form the architect chooses for capturing discovery material, each individual requirement captured there must carry:

**(a) An owner who is neither the architect nor a reviewer.** Requirements definition is an ingress function — it has to come from someone with a stake in the outcome, not be generated or attributed after the fact by the people evaluating it. A discovery entry with no identifiable owner, or one that names the architect or a reviewer as the owner, does not satisfy this policy.

**(b) The requirement's content, verbatim, in the owner's own words.** What's captured in Discovery is the accurate historical record of what was actually said or written, at the time it was provided — not a cleaned-up or pre-interpreted version of it. Wording gets refined and validated later, in the Requirements document itself (§14); the Discovery folder is not the place for that refinement to happen.

A lightweight, optional convention the architect may use to keep this consistent across discovery entries:

```markdown
## Requirement Owner
[Name / role — must not be the architect or a reviewer]

## Verbatim Input
> [The owner's exact words, unedited, as provided]
```

This is a suggestion for the architect's own use, not a template the model populates — §13.1 still applies.

## 14. Requirements document standard

### 14.1 Workflow

Once the architect has populated `01. Discovery/` with relevant material, the architect prompts the model to read the Discovery folder's contents and draft a Requirements document from `02. Requirements/_templates/hesiod-atk-requirements-template.md`, following the standard process for starting a working document (§8), including the Technical Writing Standard (§19). The model draws every requirement, use case, and strategic point in the resulting document from what it actually finds in Discovery — it does not invent requirements that have no discovery-folder basis, and it does not omit a requirement that Discovery does contain.

### 14.2 Required sections

A Requirements document contains the following six sections, as second-level headings (`##`), in this order, after the standard header (§5) and before the mandatory References footer (§10.3):

**(a) Vision and Strategy** — a long-term point of view of the design, focused on the desired outcome. A roadmap diagram is acceptable here as long as it's accompanied by a brief summary. Scope and feasibility are explicitly out of place in this section — later sections handle pragmatic constraints; this one is about the destination.

**(b) Path to Production** — specific elements for operational readiness: industry compliance standards (NIST, STIG, PCI, HIPAA, etc.) and pipeline stages (Development, Test, User Acceptance, Production, etc.). Unless the architect specifies otherwise for a given engagement, this toolkit's default compliance baseline is **NIST 500-83**, and the model should draft this section against that baseline by default.

**(c) Testing Strategy** — specific elements for testing. Unless the architect specifies otherwise, this toolkit's default functional baseline is **"Hello World"** — for a private cloud, this means every feature the cloud offers is deployed and usable by an administrative-level user. The model drafts this section against that baseline by default.

**(d) Use Cases** — a two-column Markdown table, `ID` and `Description`, with IDs following `UC-00N` (N starting at 1). Use cases are an opportunity to call out specific things the design must demonstrate — e.g. an integration to an internal third-party system the design needs to prove out before acceptance. Unless the architect specifies otherwise, this toolkit's default functional baseline is integration to the **enterprise domain**: for a private cloud, that means DNS, Active Directory/LDAP, a Certificate Authority, and a password vault (typically CyberArk). The model drafts this section against that baseline by default.

```markdown
## Use Cases
| ID | Description |
|---|---|
| UC-001 | ... |
```

**(e) Business Requirements** — a two-column Markdown table, `ID` and `Description`, with IDs following `BR-00N` (N starting at 1). Unless the architect specifies otherwise, business requirements correlate to things that drive revenue, reduce cost, accelerate the velocity of a service, reduce risk, or improve satisfaction (CSAT for customers, ESAT for employees) for the requirement owner. The model drafts this section against that default correlation.

```markdown
## Business Requirements
| ID | Description |
|---|---|
| BR-001 | ... |
```

**(f) Technical Requirements** — a two-column Markdown table, `ID` and `Description`, with IDs following `TR-00N` (N starting at 1). Unless the architect specifies otherwise, technical requirements correlate to things that measure availability, reliability, performance, capacity, scalability, and manageability (e.g. humans needed per core to manage the cloud) of the implemented design. The model drafts this section against that default correlation.

```markdown
## Technical Requirements
| ID | Description |
|---|---|
| TR-001 | ... |
```

## 15. Design document standard

### 15.1 Workflow

Once the architect prompts the model to develop the design, the model reads the contents of `02. Requirements/` and drafts a Design document from `03. Design/_templates/hesiod-atk-design-template.md`, following the standard process for starting a working document (§8), including the Technical Writing Standard (§19). Every design driver, release, and solution element in the resulting document traces back to something actually present in the Requirements document(s) — the model does not invent requirements at the design stage, and it does not silently drop a technical or business requirement it finds.

### 15.2 Audience

A Design document is written for a technologist — an architect or engineering-level reader with background in the specific technologies the design touches (e.g. vSphere, Linux, Kubernetes, Ansible). Unlike the Requirements document, it does not need to be accessible to a non-technical stakeholder.

### 15.3 Required sections

A Design document contains the following sections, after the standard header (§5) and before the mandatory References footer (§10.3), at the heading levels shown:

**(a) `#` Design Summary** — summarizes the business and technical requirements, capturing common themes and outcomes across them. Written for the technologist audience defined in §15.2.

**(b) `##` *[Design Driver]*** — one `##` subsection of Design Summary per design driver. "Design Drivers" is a placeholder label in the template only — in an actual document, each subsection's heading is the design driver itself (e.g. `## vSphere`, `## Kubernetes`), never the literal word "Design Drivers." A design driver is a Technical Requirement from the Requirements document, categorized by the specific technology it applies to. Its content summarizes that technical requirement and states a measurable target-state outcome for it — the section should answer "if I built something, how would I know that I met the requirement?"

**(c) `#` Releases** — reflects on the overall body of work and breaks it into one or more releases (major and minor), drawing on the Requirements document's Path to Production, Testing Strategy, and Use Cases sections as the basis for that breakdown. Unless the architect specifies otherwise, this toolkit's default release cadence is: major releases quarterly, minor releases monthly, and anything more frequent than that reserved for critical bug fixes. Unless the architect specifies otherwise, Day 0 is the date the project (the repository) was initialized. The model schedules and scopes releases against these defaults.

**(d) `##` *[Release X.Y]*** — one `##` subsection of Releases per release. "Release X.Y" is a placeholder label in the template only — in an actual document, each subsection's heading is the actual release identifier (e.g. `## Release 1.0`, `## Release 1.1`), never the literal text "Release X.Y." This section should answer "if I deliver Release X.Y, how would I know that I met the requirement?" — elaborate on measurable target-state success criteria for that specific release.

**(e) `#` Solution Design** — develops the design itself, with the technical depth the architecture audience (§15.2) needs. It must provide the technical components needed to meet the measurable success criteria of every design driver (§15.3(b)), and must be organized so it satisfies the measurable success criteria of each release (§15.3(d)) in sequence, with the final release representing the finished product in production. Use as many subsections and diagrams as the design actually needs — there is no fixed subsection count. This section answers: "here is what we should build to meet the requirement, and once built, here is the evidence we should capture in our test plan to prove that we met the requirement to the best of our knowledge."

**(f) `#` Implementation** — a guide to actually implementing the design, with the technical depth an engineering audience needs to manually click or CLI their way through installation and configuration. Automation comes later (in Planning, §16 when developed) — this section captures the underlying manual steps first, since those have to exist before they can be automated. Use as many subsections and diagrams as needed. This section answers: "how do I build the thing?"

**(g) `#` Conclusion** — summarizes the design and its desired outcome, lists the design decisions made, and provides a checklist the reader can use to confirm that everything described in Implementation (§15.3(f)) was actually built according to the design.

## 16. Planning document standard

### 16.1 Purpose and ownership

A Planning document answers questions about dates and resources. It is owned by the architect and stays technical in nature — it is not itself a project plan, staffing plan, or financial plan. Instead, it is the formal handoff point from the architect to a project manager: the PM takes the Planning document and uses it to produce those downstream artifacts (project plan, staffing plan, financial plan, etc.), which are outside the scope of this toolkit.

### 16.2 Workflow

Once the architect prompts the model to develop the planning document, the model reads the contents of `03. Design/` and drafts a Planning document from `04. Planning/_templates/hesiod-atk-planning-template.md`, following the standard process for starting a working document (§8), including the Technical Writing Standard (§19). The Release Plan and Work Breakdown Structure below are derived directly from the Design document's Releases (§15.3(c)–(d)) and Implementation (§15.3(f)) sections respectively — the model does not introduce dates, scope, or resourcing detail that isn't traceable back to Design.

### 16.3 Required sections

A Planning document contains the following sections, as second-level headings (`##`), in this order, after the standard header (§5) and before the mandatory References footer (§10.3):

**(a) Release Plan** — built from the Design document's Releases section, to help a project manager understand the business outcomes and critical dates tied to each release.

**(b) Work Breakdown Structure** — built from the Design document's Implementation section, to help a project manager understand the scope of work, order of operations, and skillsets needed to achieve the design's outcomes.

**(c) Jira Backlog** — organizes the Work Breakdown Structure (§16.3(b)) into a backlog of user stories, as a Markdown table:

```markdown
## Jira Backlog
| Story ID | Epic | User Story | Definition of Done |
|---|---|---|---|
| US-001 | BR-001 | As a [role], I want [goal], so that [reason]. | [Completion criteria] |
```

- `Story ID` follows `US-00N` (N starting at 1).
- `Epic` is the ID of the requirement or use case the story delivers against — a Business Requirement (`BR-00N`), Technical Requirement (`TR-00N`), or Use Case (`UC-00N`) ID from the Requirements document (§14.2). Every story must tag back to one of these; a story with no traceable Epic ID does not belong in the backlog.
- `User Story` follows the standard "As a / I want / so that" format.
- `Definition of Done` follows Atlassian's definition-of-done standard for that story — clear, testable completion criteria, not merely a restatement of the story itself.
- No user story may exceed a single two-week sprint of effort. A larger body of work is broken into multiple stories rather than captured as one oversized story.

## 17. Governance document standard

### 17.1 Purpose

A Governance document needs to equip the architect to have an intelligent conversation about the design's impact at every level — from the executive suite down to the individual design decision. It is a narrative aid the architect draws on when preparing readouts and slides; it is never handed directly to an executive or a Chief Architect to read on their own.

### 17.2 Workflow

Once the architect prompts the model to develop the governance document, the model reads the contents of `02. Requirements/`, `03. Design/`, and `04. Planning/`, and drafts a Governance document from `05. Governance/_templates/hesiod-atk-governance-template.md`, following the standard process for starting a working document (§8), including the Technical Writing Standard (§19). Every summary point and every design decision in the resulting document traces back to something actually present across those three folders.

### 17.3 Required sections

A Governance document contains the following sections, after the standard header (§5) and before the mandatory References footer (§10.3):

**(a) `#` Executive Summary** — a C-level (CIO/CTO/CISO) summary, in their language: expected outcomes, expected challenges, the expected timeline of the various releases, and any other "Wall Street Journal"–style framing of the design. Executive readouts of this kind are infrequent — quarterly at most — but the architect needs to be ready to build slides and present on this content at any time. This section frames the narrative for the architect; it does not replace what the architect owns, and the executive will never read this document directly.

**(b) `#` Architect Summary** — a Chief Architect–level summary: the expected components of the design, the threshold for meeting compliance standards, an overview of how each technical requirement is being met by the design, and any blockers to production/operational readiness. As with the Executive Summary, this section frames the narrative for the architect rather than replacing their ownership of it, and the Chief Architect will never read this document directly.

**(c) Impact Assessment** — one `#` heading per design decision, named for the decision itself (not the literal words "Impact Assessment" or "design decision" — see §15.3(b)/(d) for the same placeholder-naming convention used elsewhere in this toolkit). Each decision's heading contains exactly these `##` subsections, in this order:

  - **Context** — a scope statement reflecting on the specifics of this design decision, with particular attention to its measurable success criteria.
  - **Work Breakdown Details** — a scope statement for a non-technical audience, reflecting on the human resources involved in this design decision, with particular attention to the release and release dates it falls under.
  - **Recommendation** — the recommended decision and the justification for why this path is being recommended.
  - **Alternatives** — the alternatives considered, and why each is not being recommended.
  - **Impacts** — assuming the recommendation is approved, the resulting impact as a positive, negative, or neutral change across each of the following dimensions:

    | Dimension | Definition |
    |---|---|
    | Cost | A change in budget (e.g. new hardware required) |
    | Timeline | A change in schedule (e.g. delays from a data center build or supply chain constraints) |
    | Effort | A change in human resources (e.g. more people needed than originally planned) |
    | Functionality | A change in the project's ability to meet a requirement's measurable success criteria |

    Represent this as a table:

    ```markdown
    ## Impacts
    | Dimension | Change | Description |
    |---|---|---|
    | Cost | Positive / Negative / Neutral | [Description] |
    | Timeline | Positive / Negative / Neutral | [Description] |
    | Effort | Positive / Negative / Neutral | [Description] |
    | Functionality | Positive / Negative / Neutral | [Description] |
    ```

## 18. README standard

`README.md` is the first Markdown file the architect interacts with in any Hesiod ATK repository. It carries the instructions for initializing a project and for subsequently moving that project through the toolkit's process flow — it is not a place for engagement-specific content. Every repository instance's `README.md` contains the following sections, after a reduced header, in this order:

### 18.0 Header exception

`README.md` uses only the header image from the standard header (§5) — no title line, no metadata table (Version/Author/Role/Reviewers/Date), and no divider. The title is redundant with the About section immediately below it (which is where the toolkit's version number is stated instead, in prose), and the metadata table's information is already implied by the repository's own version number, authorship, contributor history, and commit dates (§5, §10.1), so restating either in `README.md` would be redundant. `README.md`'s header is therefore just:

```markdown
![header](_atkconfig/header.png)
```

immediately followed by the `# About the Hesiod Architecture Toolkit` section (§18.1) — no other header elements precede it.

### 18.1 `#` About the Hesiod Architecture Toolkit

A short description of the toolkit, including its version number in prose (since README carries no separate title or metadata table to state it), and this repository instance's relationship to the manifest and the five phases. Reference `MANIFEST.md` as the governing standard rather than restating it.

### 18.2 `#` Quick Start

Five `##` steps, in order, walking the architect through a full first pass of the toolkit:

- **Step 1** — obtain the repository (download/clone). Nothing else — no branching on local vs. cloud model here; that distinction is handled in Step 2.
- **Step 2** — initialize the project. A desktop AI agent (with direct filesystem access) is simply asked to initialize using the prompt below; a cloud based AI model instead needs `MANIFEST.md` uploaded first, then the same prompt. A desktop agent creates the local folder structure and templates automatically; a cloud agent instead walks the architect through creating the structure manually and provides templates to download. Either way, per the initialization procedure (§7), the model must prompt the architect for three confirmations before initialization is complete: (1) whether to update the header graphic, (2) the license ownership/copyright holder, and (3) the research guardrails (approved reference domains, §10.3) for this project. Only once those are confirmed does the architect move to Step 3.
- **Step 3** — using the Discovery template (§13, Discovery Template per its own structure — Core Technologies, Reference Guardrails, Standard Design, Customer Discovery), create the discovery document directly in `01. Discovery`, in as much detail as possible, including verbatim quotes from the customer/requirement owner(s) (§13.2). This single step covers both scoping and the substantive discovery capture.
- **Step 4** — once Discovery is complete, prompt the model to generate first drafts of the Requirements, Design, Planning, and Governance documents per the manifest (§14–§17), using Discovery as initial context.
- **Step 5** — the architect revises and reviews the first drafts.

Each step's exact prompt text (Step 2, and Step 4) is given in a fenced code block so the architect can copy it verbatim.

### 18.3 `#` WARNING

A direct statement that the architect is accountable for these artifacts, owns them, and is responsible for staying within compliance of all relevant AI and data security policies — reinforcing §10.1 and §10.4 in the architect's own first point of contact with the repository.

### 18.4 `#` Helpful Hint

A direct reminder never to share raw Markdown files with reviewers or recipients, since the model's commentary (§11.1) is for the architect's eyes only, and to convert to PDF (or another appropriate format) before sharing — reinforcing §1 and §11.1.

### 18.5 Supplementary sections

`README.md` may also carry supplementary reference sections after Helpful Hint — at minimum, a Repository Structure section (the folder tree, per §3) and a License section (linking `LICENSE`, per §10.2). These are reference material, not part of the required Quick Start flow.

## 19. Technical Writing Standard

### 19.1 Purpose

This toolkit is designed to work with whatever AI model the architect has access to — not every architect's environment permits every model. But different models default to different levels of initiative: some infer an unstated expectation of depth and specificity from context; others follow instructions literally and produce the shortest output that technically satisfies them. Every rule in this manifest up to this point defines *structure* — which sections exist, in what order, at what heading level. None of it defines *depth*. A model that is a literal instruction-follower will treat that as license to produce a structurally correct but thin document: real headings, real tables, generic sentences.

This section exists to close that gap, explicitly and mechanically enough that any model — regardless of how literally it follows instructions — produces documents with real technical substance. It applies to every document produced under this manifest (§14–§17), on top of that document type's own required sections.

### 19.2 Write like a practitioner, not like a form

Every AI model executing this manifest is acting as a principal- or staff-level architect with deep, hands-on experience in the specific technologies named in the project's Discovery scoping document (README §18.2, Step 3) — not as a general-purpose assistant summarizing a topic it knows only abstractly. That means:

- Name real things. Prefer a specific product, protocol, port number, API, file format, configuration parameter, sizing figure, or version number over a category or a generality. "The design uses NSX-T with BGP peering over a /30 transit network between the Tier-0 gateway and the physical top-of-rack switches" is compliant; "the design uses appropriate networking configurations" is not.
- Make the call. Where a design decision has to be made, make it, and justify it. Do not present a menu of possibilities as a substitute for a recommendation unless the section is explicitly asking for alternatives (e.g. §17.3(c), Alternatives).
- Never restate the heading or the manifest's own instruction as if it were content. A Context subsection that reads "This section provides context for the design decision" contains no information and does not satisfy §17.3(c). Content must add information beyond what the section's name and the manifest's guidance comment already say.
- Match density to real technical writing, not to the shortest passing answer. A section that a real architect would need several paragraphs, a table, or a diagram to cover properly does not get compressed into two sentences because two sentences are technically responsive.

### 19.3 Forbidden patterns

The following are never acceptable as a substitute for real content, in any document produced under this manifest:

- A sentence that only rephrases the section's heading (e.g. a "Design Summary" section whose only content is "this document summarizes the design").
- A placeholder-flavored hedge presented as if it were a finished statement — "various technologies may be used," "performance will be optimized," "appropriate security controls will be implemented" — without naming which technologies, what the optimization target is, or which controls.
- Reproducing this manifest's own guidance comment (§11.1) as if it were the document's content.
- A table row or list item that is technically present but empty of information (e.g. a Use Case row whose Description is "the system will integrate with the enterprise domain" with no detail on what that integration actually does or requires).
- Ending a section early because the minimum required elements (a header, a table with one row) are technically satisfied, when the underlying subject matter clearly has more to say.

### 19.4 Traceability self-check before finalizing

Before presenting any Requirements, Design, Planning, or Governance document as complete (even as a `DRAFT`), the model performs an explicit self-check pass:

1. List every requirement/use-case ID the input material establishes (every `BR-00N`, `TR-00N`, `UC-00N` from Requirements; every design driver and release from Design; as applicable to the document being drafted).
2. For each one, confirm it is addressed *substantively* somewhere in the document being drafted — not merely mentioned by ID, but actually reasoned about.
3. Where an ID is not substantively addressed, either add the content that addresses it or flag the gap explicitly in a comment (§11.1) for the architect — never silently drop it.

This turns completeness from an implicit expectation into a mechanical task, which a literal instruction-following model can execute reliably even where it wouldn't infer "be thorough" on its own.

### 19.5 Assumptions are required, not avoided

Thin output is often a model being cautious rather than lazy: it doesn't have a specific answer, so it defaults to a vague one rather than committing to something that might be wrong. This toolkit takes the opposite position. Where the Discovery folder's material doesn't specify something a real document of this type would need, the model makes a reasonable, explicit assumption grounded in the project's stated core technologies (README §18.2, Step 3) and standard industry practice for those technologies — states it plainly as an assumption (a comment per §11.1 is a good place for this, or an inline note in the body prose) — and then writes the section with the same specificity it would use if the answer had been given outright. A clearly labeled assumption that turns out to be wrong is cheap for the architect to correct; a vague sentence that avoided committing to anything gives the architect nothing to correct against.

### 19.6 Worked example

The following is an illustrative example only — a sample of the expected depth for one Design Driver subsection (§15.3(b)) and one Impact Assessment decision (§17.3(c)), against a hypothetical technical requirement. It is not part of any template and must never be copied into a real document verbatim; it exists purely to calibrate "how much, and what kind of, substance belongs in a section like this."

> **Example Design Driver — illustrative only**
>
> ## vSphere Cluster Resource Management
>
> Derived from TR-004 ("the design must maintain workload availability through the loss of any single physical host without manual intervention"). The design meets this with a vSphere HA cluster admission control policy reserving one host's worth of capacity ("Host failures cluster tolerates: 1"), combined with DRS in fully automated mode (migration threshold: 3 — moderate) across a minimum four-host cluster, so that a single host failure is absorbed without breaching the reserved capacity or requiring manual VM migration. Measurable target-state success criteria: (1) with any one host placed in maintenance mode or failed, 100% of running workloads remain powered on and reachable within the vMotion-driven rebalance window (target: under 5 minutes for a cluster of this size); (2) CPU and memory admission control never permits scheduled reservations to exceed (N-1) hosts' usable capacity, verified by a failed-host simulation in the Testing Strategy's "Hello World" pass (Requirements §Testing Strategy).
>
> **Example Impact Assessment decision — illustrative only**
>
> # Cluster Sizing: Four Hosts vs. Three Hosts at Go-Live
>
> ## Context
> The N-1 admission control policy required by TR-004 sets a floor on usable capacity per host added to the cluster. At three hosts, N-1 reserves a full third of cluster capacity for failover, which is workable but leaves little headroom for the Use Case UC-002 domain-services workload once reserved capacity is subtracted.
>
> ## Work Breakdown Details
> Sizing beyond three hosts does not change the implementation team's skillset needs, but a fourth host adds approximately one week of additional rack-and-stack and cabling effort during Release 1.0 (Design §Releases), performed by the same infrastructure technician already scheduled for that release.
>
> ## Recommendation
> Four hosts at go-live. This keeps N-1 reserved capacity at 25% of the cluster rather than 33%, leaving enough headroom for UC-002's steady-state load without requiring a mid-release capacity expansion.
>
> ## Alternatives
> Three hosts at go-live, expanding to four in Release 1.1: rejected, because it would require a second hardware delivery and rack-and-stack pass mid-project, and because UC-002's steady-state load would leave the three-host cluster within single-digit percentage points of its admission-control ceiling — too little margin for routine patching maintenance windows.
>
> ## Impacts
> | Dimension | Change | Description |
> |---|---|---|
> | Cost | Negative | One additional host purchased at go-live rather than deferred |
> | Timeline | Neutral | Fourth host ships with the same initial hardware order; no schedule change |
> | Effort | Negative | Approximately one additional week of rack-and-stack/cabling effort in Release 1.0 |
> | Functionality | Positive | Removes the mid-project capacity-expansion risk to UC-002 and improves patching-window headroom |

## 20. Project naming

At initialization (§7), the architect provides a project name (README §18.2, Step 2: `Please initialize a new project using the manifest. The project name is <PROJECT NAME>.`). From that point forward, every document produced under this manifest for that project uses the project name in place of the literal word "Hesiod" — in the document title (§5: `# [Project Name] [Document Title]` instead of `# Hesiod [Document Title]`) and anywhere else "Hesiod" would otherwise appear in that document's body prose.

This applies to the five phase templates (§4) and every working document instantiated from them (§8) — Discovery, Requirements, Design, Planning, and Governance documents all take the project's name, not the toolkit's.

**Exceptions — these always say "Hesiod," regardless of project name:**

- **`README.md`** (§18) — it documents the toolkit and how to use it, not the project's design content.
- **The release notes** (§12) — they track the version history of the toolkit instance itself, not the project's design content.
- **`MANIFEST.md`** itself — it is the standing, reusable specification governing every project built from this toolkit, not content produced for any single project.

The underlying principle, consistent across all three exceptions: a document that explains the toolkit or the release stays branded as Hesiod; a document that *is* the design content the toolkit was used to produce is branded with the project's own name. File and folder naming conventions (§2's `hesiod-atk-x.y.z` repository name, §4's `hesiod-atk-<templateName>.md` template file names) are unaffected by this rule — those are the toolkit's own structural conventions, independent of what any given project is named.

*This manifest reflects `hesiod-atk-9.1.1` as its reference instance as of 2026-09-18.*
