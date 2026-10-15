# Awesome In-House Legal [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of open-source projects that do real work for in-house legal teams: contracts, e-signature, legal AI, legal operations, investigations, compliance, and the datasets used to evaluate legal AI tools.

Curated by [IN-HOUSE APAC](https://inhouseapac.com), the membership community for in-house legal counsel across Asia-Pacific. Every entry was verified against its live repository, then reviewed a second time through one question: would a time-poor General Counsel value knowing this exists? Entries that read well but failed that test were cut. Where open source has no credible answer, we say so instead of padding. Star counts and activity notes are as of June 2026.

**A note on licenses.** Several projects here use AGPL, BSL, or fair-code licenses. Those are fine for self-hosted internal use in most cases, but review the license before embedding any of them in a product or service. You are the legal team; this is the one diligence step you cannot skip.

## Contents

- [Document Automation and Assembly](#document-automation-and-assembly)
- [E-Signature](#e-signature)
- [Contract Review](#contract-review)
- [Legal AI and NLP](#legal-ai-and-nlp)
- [Legal Operations and Knowledge](#legal-operations-and-knowledge)
- [Investigations and E-Discovery](#investigations-and-e-discovery)
- [Compliance, Privacy and Governance](#compliance-privacy-and-governance)
- [Legal Datasets and Benchmarks](#legal-datasets-and-benchmarks)
- [Where Open Source Has No Good Answer](#where-open-source-has-no-good-answer)
- [Related Lists](#related-lists)
- [Contributing](#contributing)

## Document Automation and Assembly

- [docassemble](https://github.com/jhpyle/docassemble) - Guided-interview and document assembly engine built by a lawyer-programmer; turns repeat documents (NDAs, policies, intake forms) into self-service questionnaires that output finished DOCX/PDF. The closest thing to an open-source standard in legal document automation. `Python` `MIT` `~950★`
- [docxtemplater](https://github.com/open-xml-templating/docxtemplater) - Developer library your IT team can use to generate Word, PowerPoint, and Excel files from templates legal controls, with placeholders, loops, and conditions. Mature and widely used, though advanced features such as image and HTML insertion require paid modules, so budget for a small license even though the core is free. `JavaScript` `~3.6k★`
- [Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF) - Self-hosted PDF toolbox: merge, split, convert, OCR, sign, redact. Covers the most common daily requests legal ops actually gets, with confidential documents staying on your own infrastructure. Core is MIT; some desktop and SaaS components are proprietary. `Java/TypeScript` `MIT core` `~80.6k★`

On templates rather than tools: [oneNDA](https://www.onenda.org) (the standardised NDA adopted by 600+ companies) has no canonical GitHub repository, but it pairs naturally with the tools above as the template they assemble.

## E-Signature

- [DocuSeal](https://github.com/docusealco/docuseal) - Self-hostable DocuSign alternative with drag-and-drop templates, multi-signer routing, and API automation. No per-envelope fees, and signed documents stay on your infrastructure. The default pick in this category. `Ruby` `AGPL-3.0` `~17.1k★`
- [Documenso](https://github.com/documenso/documenso) - Polished open-source signing platform with full audit trails, available self-hosted or as a paid hosted service for teams that want the open-source escape hatch without running their own server. The strongest alternative to DocuSeal. `TypeScript` `AGPL-3.0` `~13.3k★`
- [LibreSign](https://github.com/LibreSign/libresign) - Digital signing inside Nextcloud, with workflows, roles, and audit logs. The right answer only where the company already runs Nextcloud for files. `PHP` `AGPL-3.0` `~770★`

**Legal validity caveat.** Electronic signature law varies widely across APAC. Several jurisdictions recognise standard electronic signatures for routine commercial contracts but require certified or qualified signatures, issued through licensed local providers, for specific document classes such as property, employment, or regulatory filings. A self-hosted tool produces a standard electronic signature only. Confirm enforceability and evidentiary weight per jurisdiction and document type before moving any document class off your incumbent provider.

## Contract Review

- [OpenContracts](https://github.com/Open-Source-Legal/OpenContracts) - Self-hosted platform where your team uploads contracts, annotates them, and asks questions across the whole set, with every AI answer pinned to the exact clause it came from rather than a black-box chat response. Needs corporate IT to deploy and run, but the payoff is contract intelligence that never leaves your infrastructure. `Python/TypeScript` `MIT` `~1.4k★`
- [LegalQuants lq-ai](https://github.com/LegalQuants/lq-ai) - Early-stage watch-list entry: a self-hosted workbench for playbook-driven first-pass contract review (NDA, MSA, and DPA playbooks included), able to run fully air-gapped against local models. Weeks old as of mid-2026; pilot it on low-stakes work and reassess, and keep it out of the production path for now. `Python` `Apache-2.0` `~65★`

## Legal AI and NLP

**Use now, with IT:**

- [Presidio](https://github.com/microsoft/presidio) - Microsoft's PII detection and de-identification framework for text, images, and structured data. The standard answer to "redact the personal data before it goes to the LLM", relevant under PDPA, PIPL, and APPI alike. `Python` `MIT` `~8.6k★`

**Jurisdiction reference points for vendor evaluation** (you will never run these yourself; you cite them in vendor meetings):

- [ChatLaw](https://github.com/PKU-YuanGroup/ChatLaw) - Open legal LLM family from Peking University fine-tuned for mainland PRC law, with released weights. The benchmark question to put to any vendor claiming China legal-AI capability: how do you compare against the open academic state of the art, and how do you control hallucinated citations, a failure mode the ChatLaw team itself documents. `Python` `AGPL-3.0` `~7.5k★`
- [OpenNyAI](https://github.com/OpenNyAI/Opennyai) - NLP pipeline for Indian legal documents: named entity recognition, extractive summarisation, and rhetorical role labelling of judgments. The rare open tooling that speaks the jurisdiction, and a yardstick for India-focused vendor claims. `Python` `MIT` `~95★`
- [SaulLM](https://huggingface.co/Equall) - The first open-weights LLM family adapted specifically for law (7B to 141B, trained on 30B+ legal tokens), from Equall. Hosted on Hugging Face rather than GitHub. The English-language counterpart to ChatLaw when asking vendors how their proprietary model compares to the open state of the art. `MIT weights`

**Historical context: what contract AI is made of** (do not deploy; read to understand what vendors sell):

- [ContraxSuite](https://github.com/LexPredict/lexpredict-contraxsuite) - The original open-source contract analytics platform (ingestion, OCR, ML clause extraction, review UI), dormant since 2022. Its value now is as an anatomy lesson: walking through what it does is a fast way to understand what CLM and contract-AI vendors are actually selling you, layer by layer. `AGPL-3.0` `~180★`
- [LexNLP](https://github.com/LexPredict/lexpredict-lexnlp) - Information extraction library for legal text (dates, money, durations, citations, clause types) that defined the pre-LLM toolkit for contract analytics. Effectively frozen since 2022; treat it as a reference for what extraction vendors automate under the hood, and note the AGPL license if anyone proposes embedding it. `Python` `AGPL-3.0` `~780★`

## Legal Operations and Knowledge

- [n8n](https://github.com/n8n-io/n8n) - Workflow automation with 400+ integrations and native AI capabilities. The legal-ops glue for intake routing, contract-approval handoffs, and matter-status notifications; self-hosting keeps privileged data inside the firewall. `TypeScript` `Fair-code` `~192k★`
- [Outline](https://github.com/outline/outline) - Fast, collaborative team knowledge base with granular permissions. A clean home for legal playbooks, fallback positions, and self-serve FAQs the business can search instead of emailing legal. `TypeScript` `BSL-1.1` `~39k★`
- [BookStack](https://github.com/BookStackApp/BookStack) - Self-hosted wiki organised into books, chapters, and pages, with role-based access. Choose this over Outline when IT wants a simpler PHP stack or your library is rigidly hierarchical (one book per contract type or jurisdiction playbook); choose Outline for faster search and a more modern editor. `PHP` `MIT` `~18.8k★`
- [Formbricks](https://github.com/formbricks/formbricks) - Open-source survey and form platform. Replaces ad-hoc email with structured legal intake (contract requests, incident reports) that pipes straight into a triage workflow while data stays on your server. `TypeScript` `AGPL-3.0` `~12.4k★`
- [legal-function-operating-system](https://github.com/sebastianfoerste/legal-function-operating-system) - Deterministic rules (no LLM in the decision path) that turn incoming legal requests into a risk rating, priority, owner, SLA, approval tier and external-counsel decision, plus a board pack. A readable, testable triage model for a first legal hire or GC. Early-stage: bundled data is synthetic, it reads JSON rather than a live CLM, consequential decisions need human review, and there is no PyPI package yet. `Python` `MIT` `~2★`

## Investigations and E-Discovery

- [Aleph](https://github.com/alephdata/aleph) - Searches and browses large collections of documents and structured data, surfacing the people and companies inside them. Built for investigative journalism; equally suited to internal investigations and due diligence. Original OCCRP development has wound down; the actively maintained fork is [OpenAleph](https://github.com/openaleph/openaleph) from the Data and Research Center, which is the version to deploy. `Python/JavaScript` `MIT` `~2.4k★`
- [Datashare](https://github.com/ICIJ/datashare) - Self-hosted document search from the ICIJ with OCR, named-entity extraction, and batch search. Battle-tested at Panama and Pandora Papers scale; useful for investigations, subject access requests, and discovery scoping. `Java` `AGPL-3.0` `~740★`
- [FreeEed](https://github.com/shmsoft/FreeEed) - Open-source e-discovery processing engine (Tika, Lucene, Solr) with OCR and review support, maintained by a very small team. Useful for early case assessment and internal-investigation triage to size custodian data before engaging a paid platform; for contested litigation, expect process defensibility to be challenged and budget for a supported tool. `Java` `Apache-2.0` `~140★`
- [CourtListener](https://github.com/freelawproject/courtlistener) - Free Law Project's searchable archive of US court opinions, oral arguments, judges, and PACER filings, with free docket alerts. Use the hosted service at [courtlistener.com](https://www.courtlistener.com); relevant to APAC teams with US litigation or counterparty-monitoring exposure. The repo matters only if you want to run your own instance. `Python` `~950★`

## Compliance, Privacy and Governance

- [CISO Assistant](https://github.com/intuitem/ciso-assistant-community) - GRC platform covering risk assessment, audit, and compliance management with built-in support for 150+ frameworks (ISO 27001, SOC 2, NIS2, DORA, GDPR, PCI DSS). A free, self-hostable system of record for compliance posture. `Python` `AGPL-3.0` `~4.1k★`
- [GlobaLeaks](https://github.com/globaleaks/globaleaks-whistleblowing-software) - The canonical open-source whistleblowing platform: secure, anonymous reporting channels an organisation can stand up without a SaaS vendor. Directly relevant as speak-up channel requirements spread across the EU, Australia, Japan, and the wider region. Very actively maintained. `Python` `AGPL-3.0` `~1.5k★`
- [CNIL PIA](https://github.com/LINCnil/pia) - The French data protection regulator's own open-source tool for conducting Data Protection Impact Assessments, deployable as a web or desktop app. Regulator-authored methodology that maps cleanly onto DPIA obligations in GDPR-style APAC privacy laws. Releases are infrequent (last major release 2024) though the repo stays alive. `TypeScript` `GPL-3.0` `~290★`
- [Fides](https://github.com/ethyca/fides) - Privacy engineering platform for data mapping, consent management, and automated fulfilment of access and deletion requests. Legal sets the requirements; engineering deploys it and wires the connectors, and several advanced features sit behind Ethyca's paid tier. Best read as the tool you hand to IT when DSAR volume outgrows spreadsheets. `Python/TypeScript` `Apache-2.0` `~460★`
- [Open Terms Archive](https://github.com/OpenTermsArchive/engine) - Tracks the terms of service and privacy policies of online services and keeps a versioned, timestamped archive of every change. Subscribe to the public instance or run your own to catch unilateral amendments to key vendor terms when they happen, with a documented record to point to in a dispute. `JavaScript` `EUPL-1.2` `~130★`
- [CookieConsent](https://github.com/orestbida/cookieconsent) - Dependency-free cookie consent banner with granular per-category consent, widely deployed and actively maintained (Klaro is a BSD-licensed alternative). A fast, no-fee way to get a properly configured banner across corporate sites and microsites; compliance still depends on your cookie audit, configuration, and consent record-keeping, which a banner alone does not provide. `JavaScript` `MIT` `~5.5k★`
- [Giskard](https://github.com/Giskard-AI/giskard) - Evaluation and testing library for LLM systems, including scanning for hallucination, bias, and security failures. Legal and AI-governance owners do not run it themselves; its value is as the concrete testing standard you require engineering or vendors to run, so your AI policy produces evidence instead of attestations. `Python` `Apache-2.0` `~5.4k★`

## Legal Datasets and Benchmarks

How do you know whether a legal AI tool is any good? You test it against these, or require your vendor to.

- [CUAD](https://github.com/TheAtticusProject/cuad) - The Contract Understanding Atticus Dataset: 500+ commercial contracts expert-annotated across 41 clause categories. The standard benchmark for whether a contract-review AI can actually find the assignment, change-of-control, and indemnity clauses you care about. `Dataset, CC BY 4.0`
- [MAUD](https://github.com/TheAtticusProject/maud) - The Merger Agreement Understanding Dataset, from the same Atticus Project as CUAD: expert annotations on public merger agreements built from the ABA Deal Points Study. The benchmark to cite when evaluating AI for M&A deal work. The repo itself carries no license file; the dataset is distributed by the Atticus Project. `Dataset` `~94★`
- [ContractNLI](https://stanfordnlp.github.io/contract-nli/) - Stanford's benchmark testing whether a system can determine what an NDA actually permits, prohibits, or stays silent on, across 607 annotated NDAs. NDA review is the first use case every legal AI vendor pitches; this is the test for it. ([GitHub](https://github.com/stanfordnlp/contract-nli)) `Dataset, CC BY 4.0`
- [LegalBench](https://github.com/HazyResearch/legalbench) - Open-science benchmark of 160+ legal reasoning tasks contributed by 40+ lawyers and academics. The most load-bearing public yardstick for "is this LLM actually good at legal reasoning?" `Benchmark`
- [Pile of Law](https://github.com/Breakend/PileOfLaw) - A roughly 256GB open corpus of legal and administrative text, mostly US, used to pretrain legal language models. You will never download it. Its value is as a vocabulary item: when a vendor says their model was "trained on legal data", this is the reference point for asking what data, under what licenses, and with what privacy filtering. `Dataset`
- [LawBench](https://github.com/open-compass/LawBench) - 20 tasks across memorisation, understanding, and application for evaluating LLMs on Chinese law, with published results for 51 models. GPT-4 topped out at 52 percent zero-shot, a useful calibration on how far legal AI still has to go. `Benchmark, Apache-2.0`
- [LBox Open](https://github.com/lbox-kr/lbox-open) - Multi-task benchmark and 150k-precedent corpus for Korean legal language understanding and judgment prediction. The principal open dataset for evaluating legal AI on Korean law. Data licensed CC BY-NC, which limits commercial reuse of the corpus itself. `Dataset, CC BY-NC 4.0`
- [contract-review-eval-harness](https://github.com/sebastianfoerste/contract-review-eval-harness) - Scores a contract-review tool's output against a hand-authored answer set for clause coverage, risk severity and citation grounding; any quote that is not an exact span of the contract is an automatic reject. Puts numbers behind a vendor's "the AI reviews contracts" claim. Early-stage: the bundled contracts are synthetic, the answers come from one annotator, and there is no PyPI package yet. `Python` `MIT` `~2★`

For Japan, the established evaluation resource is the annual [COLIEE](https://coliee.org) competition, built partly on Japanese bar exam materials; its datasets are distributed by application rather than on GitHub, so it appears here as a pointer rather than an entry.

## Where Open Source Has No Good Answer

A curated list should say where the cupboard is bare instead of padding the gap. As of June 2026:

- **Contract lifecycle management.** There is no production-grade open-source CLM: the post-signature repository with renewal dates, obligations, and reporting. Budget for a commercial tool here.
- **Entity management and cap tables.** Nothing credible is actively maintained. The best-known open attempt has stalled, and corporate records are the wrong place to accept maintenance risk.
- **E-billing and legal spend.** No credible open-source platform exists beyond small format utilities.
- **Southeast Asian legal NLP.** Thailand, Vietnam, Indonesia, and the Philippines have essentially no credible open legal NLP tooling or benchmarks. Vendors claiming these jurisdictions are working without public yardsticks; ask them what they test against.

## Related Lists

- [awesome-legal-skills](https://github.com/lawve-ai/awesome-legal-skills) - Curated catalog of 40+ portable AI agent skills for legal work (contract review, privacy, employment, corporate), maintained by Lawvable. A different layer of the stack: instructions for AI agents rather than deployable software. `CC BY-NC-ND 4.0` `~415★`
- [awesome-legaltech](https://github.com/Vaquill-AI/awesome-legaltech) - Broad community index of legaltech resources across 60+ jurisdictions: platforms, AI models, APIs, MCP servers, companies. Wider and shallower than this list; useful as a discovery layer. `~114★`

## Contributing

Suggestions are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) for the curation standards, then open an issue or pull request.

## About

Maintained by [IN-HOUSE APAC](https://inhouseapac.com), the membership community for in-house legal counsel across Asia-Pacific. For commercial legal AI tools, see our [Legal AI Directory](https://inhouseapac.com).

Licensed under [CC0 1.0](LICENSE).
