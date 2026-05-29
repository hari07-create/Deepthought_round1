# Part B: Sourcing Strategy & 1000-Company Scale-Up Proposal

## Goal

Build a verified list of 1000 companies that match DeepThought's Federer ICP — Indian specialty manufacturers, Rs.50Cr–Rs.500Cr, promoter-driven, differentiated product, technical decision-maker, active growth signals — within 30 calendar days.


---

## Sourcing Strategy

Below are four high-alpha sourcing channels engineered specifically for this ICP.

### 1. DSIR Directory of Recognized In-House R&D Units
* **Mechanism:** The Department of Scientific and Industrial Research (DSIR) grants formal recognition to companies running dedicated, physical, in-house laboratory assets. 
* **Why it fits the ICP:** DeepThought targets differentiated, technical organizations. A DSIR listing serves as empirical evidence of **C3 (Differentiation via IP/R&D)** and implies a **C4 Science-Founder or advanced engineering pedigree**. It automatically filters out non-technical commodity operations.
* **Limitations:** The directory is released in batch PDF documents periodically, meaning bleeding-edge, early-stage firms may experience a data lag before appearing on the official register.

### 2. KIADB / MIDC State Industrial Allotment & Lease Registries
* **Mechanism:** Regional industrial development boards (e.g., KIADB in Karnataka, MIDC in Maharashtra) publish allocation logs whenever a firm leases land inside manufacturing zones like Peenya, Jigani, or Hoskote.
* **Why it fits the ICP:** This perfectly validates the **E1 (Producer)** gate. Traders or distributors do not lease heavy industrial plots. Furthermore, securing a new industrial plot is a definitive proxy flag for **C6 (Growth Signals: Facility Expansion within 18 months)**.
* **Limitations:** Data formatting is highly fragmented across individual state-level portals, requiring custom web scrapers or OCR (Optical Character Recognition) parsing to unify the registries.

### 3. Niche B2B Trade Expo & Industrial Exhibition Catalogs
* **Mechanism:** Scraping past and upcoming exhibitor lists from highly technical conferences (e.g., *ChemExpo India*, *Diagnostic Expo*, *IPCA electronics show*).
* **Why it fits the ICP:** Only risk-taking, growth-mode companies spend capital on exhibition booths to showcase custom capabilities, specialized machinery, or market-shaping innovations (like short MOQ thresholds). This filters out passive, stagnant businesses.
* **Limitations:** Exhibitor directories provide excellent technical signals but lack financial metrics, requiring a secondary pipeline step to filter out entities exceeding the ₹500Cr ceiling.

### 4. LinkedIn Talent Pool Arbitrage (QA/QC & SAP Functional Roles)
* **Mechanism:** Running specialized talent queries to identify mid-sized manufacturing firms employing multiple Quality Assurance (QA/QC) Engineers or internal SAP/ERP Analysts inside designated industrial hubs.
* **Why it fits the ICP:** A firm employing dedicated QA teams and enterprise software specialists has passed the point of loose, founder-dependent intuition and represents high **C7 (Systems Maturity)**. They have actively accepted process infrastructure, making them prime targets for execution consulting.
* **Limitations:** Highly capable tech-founders at lower revenue scales (₹10Cr–₹20Cr) may rely on fractional external consultants for ERP configuration rather than full-time payroll staff, creating minor false negatives.

---

## The 1000-Company Scale-Up Proposal

### 1. Sourcing Funnel Architecture & Target Yields

Building a high-quality list of 1,000 genuinely ICP-qualified companies within 30 days requires an aggressive multi-layered filtration funnel. 

[4,000 Raw Leads] ──(Gate 1: Financial & E1 Filters)──> [1,500 Base Entities] ──(Gate 2: Deep LLM Scoring)──> [1,100 High Confidence] ──(Gate 3: Human QC)──> [1,000 Qualified ICP]


* **Stage 1: Raw Lead Generation (Target: 4,000 Leads | Yield: 100%)**
  * Sourced via automated scraping of the DSIR directory, B2B expo exhibitor tables, and KIADB/MIDC lease registries.
* **Stage 2: Eligibility & Revenue Gate Filtration (Target: 1,500 Entities | Yield: ~37.5%)**
  * Automated programmatic filtration against the ₹50Cr–₹500Cr revenue thresholds, dead URL checks, and trader keyword exclusion.
* **Stage 3: Deep LLM Feature Extraction (Target: 1,100 Entities | Yield: ~73.3%)**
  * Parsing website copy to analyze technical differentiation (C3), management background (C4), and operational systems (C7).
* **Stage 4: Human-in-the-Loop Quality Control (Target: 1,000 Final Pass | Yield: ~90.9%)**
  * Manual review of borderline edge cases, layout validation, and final outreach line compilation.

---

### 2. Four-Week Operational Sprint Plan

#### 📅 Week 1: Sourcing & Universe Aggregation (Days 1–7)
* **Focus:** Build the broad, unrefined lead pool.
* **Tooling Stack:** Python (`BeautifulSoup`, `Selenium`), Scrapy framework, and Google Cloud Vision API for processing scanned industrial documents.
* **Activities:** * Deploy automated scraping workers to gather corporate registries, trade show attendee logs, and state industrial layout sheets.
  * Consolidate names, geographic footprints, and corporate URLs into a unified PostgreSQL staging database.
* **Target Output:** 4,000 raw row entries.

#### 📅 Week 2: Programmatic Gating & Financial Filtering (Days 8–14)
* **Focus:** Eliminate corporate groups, service-only companies, and companies out of the target revenue range.
* **Tooling Stack:** Financial endpoint integrations (Tofler/Zauba API), Python `asyncio`/`aiohttp` for high-throughput HTTP pinging.
* **Activities:**
  * Run company names through commercial database APIs to instantly flag and isolate entities exceeding the ₹500Cr ceiling or falling below ₹10Cr.
  * Script automated keyword checks on page source-code to auto-disqualify pure traders, distributors, and CROs/testing labs.
  * Perform batch asynchronous header requests to cull dead links or single-page placeholder domains.
* **Target Output:** 1,500 verified physical producers within the target mid-market range.

#### 📅 Week 3: Asynchronous LLM Scoring & Parsing (Days 15–21)
* **Focus:** Perform contextual scoring against the Federer criteria (C3, C4, C7).
* **Tooling Stack:** Gemini 1.5 Pro / Claude 3.5 Sonnet Batch API, LangChain / Instructor framework for structured JSON extraction.
* **Activities:**
  * Execute a web crawler to scrape text content from the "About," "Products," "Careers," and "News" tabs of the 1,500 validated domains.
  * Feed clean text blocks to the LLM Batch API using rigid Pydantic structures. Instruct the model to extract and output specific JSON keys:
    * `differentiation_type`: [IP-based / Capability-based / None]
    * `decision_maker_archetype`: [Science-founder / Operator-founder / Non-technical]
    * `systems_infrastructure`: [SAP / Oracle / Custom ERP / None]
    * `growth_signals_count`: Integer tracking new plants, active hiring, or certifications.
* **Target Output:** 1,100 mathematically scored profiles complete with inline evidence quotes.

#### 📅 Week 4: Human-in-the-Loop QC & Personalized Hook Construction (Days 22–30)
* **Focus:** Guarantee data cleanlines and craft high-conversion outreach angles.
* **Tooling Stack:** Internal Retool dashboard, OpenPyXL formatting engine.
* **Activities:**
  * Review borderline entities (companies scoring 40–59) to confirm whether they represent genuine independent producers or complex false positives.
  * Sanitize text descriptions to remove internal newline breaks (`\n`, `\r`) that cause Excel spreadsheet row distortion.
  * Validate that each row contains a non-templated, distinct personalization hook focusing on specific plant metrics, patent numbers, or asset expansions.
* **Target Output:** 1,000 pristine, production-ready, fully verified Federer target companies.

---

### 3. Quality Control & Risk Mitigation Framework

* **Defending Against the "CRO/Testing Lab" Trap:** The web scraper flags keywords like *"Testing Services," "Sample Analysis," "Contract Clinical Trials," and "Fee per sample."* Any entity triggered by these keywords is shunted to a manual verification queue to protect the **E1 Producer** requirement.
* **Managing Borderline Revenue Cases:** Fast-growing specialty companies can break past the ₹500Cr ceiling mid-year. The ingestion pipeline crosschecks recent press releases for keywords like *"record-breaking revenue"* or *"crossed milestone"* to identify and flag these entities for immediate manual review.
* **Preventing LLM Hallucinations:** The parsing system enforces an **Evidence Constraint**. The L