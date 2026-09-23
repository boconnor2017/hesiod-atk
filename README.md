![header](_atkconfig/header.png)

# About the Hesiod Architecture Toolkit 

The Hesiod Architecture Toolkit (HATK) — version 9.1.1 — is an open source project to assist architects in the creation, publication, and release management of design artifacts. By using this toolkit, technical practitioners remain within the acceptable boundaries of the manifest while using approved AI models to accelerate productivity in the technical writing process.

This repository is an instance of the toolkit, initialized from `MANIFEST.md`. It carries the artifacts produced across the toolkit's five phases: Discovery, Requirements, Design, Planning, and Governance. See `MANIFEST.md` for the full standard governing this repository's structure, naming conventions, document formatting, process flow, and governance standards.

# Quick Start

## Step 1

Download or clone the latest HATK repository from https://github.com/boconnor2017/hesiod-atk.

## Step 2

If you are using an AI agent on your desktop, ask your AI model to initialize a project using the prompt below.

If you are using a cloud based AI model, upload the MANIFEST.md file to your browser, then ask your AI model to initialize a project using the prompt below.

```
Please initialize a new project using the manifest. The project name is <PROJECT NAME>.
```

AI agents will automatically create a local folder structure with necessary templates. Cloud agents will provide the steps to create local folder structure manually and will provide templates for you to download to the appropriate folder.

Per the instructions in the manifest, the AI should prompt you for three confirmations:
1. To ensure the header graphic is updated.
2. To update license ownership.
3. To add research guardrails.

If you have reached this status, move on to step 3.

## Step 3

Using the template from the `01. Discovery` folder, create a new discovery document. Include as much detail as possible including verbatim quotes from the customer. This will be the foundation for the remainder of your documentation.

## Step 4

When your Discovery sessions have ended and all pertinent information for the design has been captured in detail, prompt your AI model as follows:

```
Please generate a first draft of all documents outlined in the manifest. This should include a requirements document, a design document, a planning document, and a governance document. Use all content from Discovery as the initial context for the design.
```

## Step 5

Revise the first drafts of each document. Review the documents accordingly.

# WARNING

You, as the architect, are accountable for these artifacts. You are the owner of these artifacts. You are responsible for understanding and staying within compliance of all relevant AI policies and data security policies.

# Helpful Hint

Do not ever share the raw Markdown files with reviewers or recipients. The AI model is tasked with adding commentary for your eyes only. Convert the Markdown files to an appropriate format (PDF is recommended) before sharing.

# Repository Structure

```
hesiod-atk-9.1.1/
├── _atkconfig/            # Shared assets used across every document (e.g. header.png)
├── _release_notes/        # Version history for this toolkit instance
├── 01. Discovery/
│   ├── _img/               # Images referenced by Discovery-phase documents
│   └── _templates/         # Discovery-phase master templates
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

# License

The Hesiod Architecture Toolkit is open source under the [MIT License](LICENSE).
