![header](../_atkconfig/header.png)

# Hesiod Release Notes

| | |
|---|---|
| **Version** | 1.0 [DRAFT] |
| **Author** | [Accountable Human] |
| **Role** | [Human Role] |
| **Reviewers** | [List of Human Reviewers] |
| **Date** | 2026-09-18 |

---

# What's New

Initial scaffold of the Hesiod Architecture Toolkit (hesiod-atk-9.1.1), built from `MANIFEST.md`. This release establishes the toolkit's repository structure and standards rather than any engagement-specific content:

* Repository structure: `_atkconfig/`, `_release_notes/`, and the five phase folders (Discovery, Requirements, Design, Planning, Governance), each with an `_img/` and `_templates/` subfolder.
* `_atkconfig/header.png` — the shared banner image used in every document header.
* `LICENSE` — the toolkit is open source under the MIT License.
* Requirements Template body developed: Vision and Strategy, Path to Production (NIST 500-83 default baseline), Testing Strategy ("Hello World" default baseline), Use Cases (`UC-00N`, enterprise-domain default baseline), Business Requirements (`BR-00N`), and Technical Requirements (`TR-00N`), each per `MANIFEST.md` §14.
* Design Template body developed: Design Summary with per-driver subsections, Releases with per-release subsections (quarterly major / monthly minor / hotfix default cadence, Day 0 = project init), Solution Design, Implementation, and Conclusion, each per `MANIFEST.md` §15.
* Planning Template body developed: Release Plan, Work Breakdown Structure, and Jira Backlog (`US-00N` stories tagged to `BR-00N`/`TR-00N`/`UC-00N` Epics, Atlassian-style Definition of Done, two-week sprint cap), each per `MANIFEST.md` §16.
* Governance Template body developed: Executive Summary, Architect Summary, and a repeatable per-design-decision Impact Assessment block (Context, Work Breakdown Details, Recommendation, Alternatives, Impacts scored across Cost/Timeline/Effort/Functionality), each per `MANIFEST.md` §17.
* Discovery Template body developed: Core Technologies, Reference Guardrails, and Standard Design (each with toolkit-standard default content oriented around VMware Cloud Foundation 9.1.1), plus a Customer Discovery table (Requirement / Owner / Date Captured) for capturing customer-specific requirements. This template is filled in by the architect only — never by the model — per §13.
* All five phase templates are now complete: Discovery (architect-owned), Requirements, Design, Planning, Governance.
* `README.md` rebuilt to the required structure: About the Hesiod Architecture Toolkit, Quick Start, WARNING (architect accountability), Helpful Hint (never share raw Markdown; convert to PDF), plus Repository Structure and License reference sections.
* `README.md` header simplified further (`MANIFEST.md` §18.0): image only now — no title line and no metadata table. The version number moved into the About section's prose instead of a standalone title, since the title was redundant with About.
* Quick Start streamlined from six steps to five, now that the Discovery Template itself carries Core Technologies, Reference Guardrails, Standard Design, and Customer Discovery (§13): Step 3 now covers both scoping and substantive discovery capture in one step (using the Discovery template directly, with verbatim customer/requirement-owner quotes). Step 1 is now just obtaining the repository; Step 2 absorbs the local-vs-cloud-model branching and now also tells the architect to expect three initialization confirmations from the model (header graphic, license ownership, research guardrails) before moving on.
* `MANIFEST.md` §7 (initialization procedure) formalizes the three-confirmation gate Step 2 of the README refers to: the model must confirm the header graphic, license ownership, and research guardrails with the architect before initialization is considered complete.
* `MANIFEST.md` §20 Project Naming added: once a project is initialized with an architect-provided project name, every document produced for that project (the five phase documents and their templates) uses the project's name in place of the literal word "Hesiod" in titles and body prose. `README.md`, the release notes, and `MANIFEST.md` itself are exempt, since they document the toolkit/release rather than the project's design content.
* `MANIFEST.md` §10.3 tightened: a document's References section may only cite sources outside the toolkit's own published documents — citing another Hesiod ATK document as a reference is now explicitly disallowed, since it makes References circular and self-validating.
* `MANIFEST.md` §19 Technical Writing Standard added: a model-agnostic depth and specificity standard (write like a practitioner, forbidden vague/filler patterns, a mandatory traceability self-check before finalizing any document, explicit assumption-licensing, and a worked example calibrating expected depth) — added after cross-model testing showed some models treat the manifest's structural instructions too literally and produce thin, structurally-compliant-but-shallow documents. Cross-referenced from §8 and each of §14–§17's workflow steps.
* `MANIFEST.md` established as the governing standard, covering folder structure, naming conventions, the document header format, non-negotiable "architect in the loop" governance standards (human authorship and accountability, approved research-domain scope, data security, AI disclosure/provenance), documentation standards (architect-only comments, minimal formatting, image storage), the release notes standard, Discovery folder governance (architect-only ingress, requirement owner + verbatim content), the Requirements, Design, Planning, and Governance document standards, the README standard, the Technical Writing Standard, and Project Naming.

# Known Issues

<!-- Architect: add known bugs directly to this list as you find them, even between
     formal releases, so the ATK development team has a persistent record to prioritize
     fixes against. -->

* `header.png` has not been reviewed for accessibility (contrast/alt-text) against the full range of PDF viewers and print conditions.
* `LICENSE` copyright line reflects the project's GitHub URL rather than a named legal entity; revisit if a different attribution is required later.

# Bill of Materials

| Template Name | Template Description | Template Location | Template Type |
|---|---|---|---|
| Discovery Template | Full template for Phase 01 Discovery documents (Core Technologies, Reference Guardrails, Standard Design defaults, Customer Discovery table) — architect-populated only, never model-drafted | 01. Discovery/_templates | Markdown |
| Requirements Template | Full template for Phase 02 Requirements documents (Vision and Strategy, Path to Production, Testing Strategy, Use Cases, Business Requirements, Technical Requirements) | 02. Requirements/_templates | Markdown |
| Design Template | Full template for Phase 03 Design documents (Design Summary/drivers, Releases, Solution Design, Implementation, Conclusion) | 03. Design/_templates | Markdown |
| Planning Template | Full template for Phase 04 Planning documents (Release Plan, Work Breakdown Structure, Jira Backlog) | 04. Planning/_templates | Markdown |
| Governance Template | Full template for Phase 05 Governance documents (Executive Summary, Architect Summary, per-decision Impact Assessment) | 05. Governance/_templates | Markdown |

# References
* [Title](URL)
