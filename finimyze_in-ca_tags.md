# Finimyze — Why `in-ca` Tags Matter (Ind AS XBRL)

## TL;DR
- **`ind-as:*`** concepts carry the **financial statement numbers** (P&L, BS, CF).
- **`in-ca:*`** concepts carry **India/MCA/Companies-Act context + disclosures + entity metadata**.
- For Finimyze, `in-ca` is **not the valuation math**, but it is often **required to interpret, trust, and present the math correctly**—especially for **professional/enterprise** tiers.

---

## What `in-ca` gives Finimyze
### 1) Correct interpretation of extracted numbers (often *required*)
`in-ca` provides the context needed to avoid silent valuation mistakes:
- **Standalone vs Consolidated** classification (changes entity scope, cashflows, leverage, comparables).
- **Reporting currency** and **rounding level** (₹ vs other currency; lakhs/crores; impacts scaling).
- **Reporting period boundaries** (FY start/end, audit sign date) for time-series comparisons and trailing metrics.
- **Cashflow method** indicator (direct/indirect presentation differences; affects parsing/rendering).

**Why it matters:** Without these, the same `ind-as` numbers can be mis-scaled, mixed across scopes, or mis-compared.

---

### 2) Trust + governance signals (highly valuable for “Risk Profile” + memo)
`in-ca` enables governance/assurance sections that support investor confidence and enterprise controls:
- **Auditor identity + registrations** (audit firm name, FRN, membership IDs).
- **Signature metadata** (date/place of signing, director signing financials).

**Why it matters:** Helps build a “Trust / Governance” layer for free + paid tiers and is important for enterprise audit trails.

---

### 3) Business exposure & risk inputs (useful for risk, narratives, and comparables)
Common high-signal disclosures in `in-ca`:
- **Domestic vs export turnover splits** (goods/services; supports FX risk and geographic diversification narratives).
- **Related party transaction disclosures** (governance and control risk).
- **Capital actions/events** (dividend/buyback/bonus/rights) that can affect equity value interpretation.

**Why it matters:** These support your **“Brief”, “Risk Profile”, “News impact”, and “Analyst memo”** features without requiring extra scraping.

---

## Minimal `in-ca` tag groups to support (recommended v1)
> Not comprehensive—just the high-impact items.

### A) Entity identity & classification
Use for company profile, filtering, peer comparisons:
- `in-ca:CorporateIdentityNumber`
- `in-ca:PermanentAccountNumberOfEntity`
- `in-ca:WhetherCompanyIsListed`
- `in-ca:NatureOfReportStandaloneOrConsolidated`

### B) Reporting basis (currency / rounding / dates)
Use for scaling and time-series correctness:
- `in-ca:ReportingCurrency`
- `in-ca:LevelOfRoundingUsedInFinancialStatements`
- `in-ca:FinancialYearStartDate`
- `in-ca:FinancialYearEndDate`

### C) Cashflow statement metadata
Use for consistent CF rendering/extraction:
- `in-ca:CashAndCashEquivalentsStatementMethod`

### D) Auditor & signing (trust/governance)
Use for risk scoring + memo:
- `in-ca:NameOfAuditFirm`
- `in-ca:AuditorFirmRegistrationNumber`
- `in-ca:AuditorMembershipNumber`
- `in-ca:DateOfSigningOfAuditReport`
- `in-ca:NameOfDirectorSigningFinancialStatements`
- `in-ca:PlaceOfSigningOfFinancialStatements`

### E) Exposure & governance risk disclosures
Use for risk profile and “plain-English” summaries:
- `in-ca:DomesticTurnoverGoodsGross`
- `in-ca:ExportTurnoverGoodsGross`
- `in-ca:DomesticTurnoverServicesGross` *(if present)*
- `in-ca:ExportTurnoverServicesGross` *(if present)*
- Related party transaction concepts (RPT amounts / outstanding balances) *(exact names vary by filing)*

### F) Capital actions (optional but valuable)
Use for memo + shareholder yield narratives:
- Dividend / buyback / bonus / rights issue concepts *(exact names vary by filing)*

---

## What `in-ca` is **not** needed for (safe to deprioritize)
These typically add little valuation value:
- Filing logistics (SRN, registry filing IDs, software used to prepare XBRL).
- Pure document identifiers or signature blocks that don’t add analytical meaning.

---

## How this aligns with Finimyze goals
### Free tier (simpler UI)
`in-ca` supports “explainable” pages:
- **Company identity & report type**
- **Business exposure (domestic/export)**
- **Governance/assurance snapshots**

### Paid tier (professional analysis)
`in-ca` enables:
- **accurate comparables (scope + scaling)**
- **audit trail (metadata + signing)**
- **risk overlays (RPT, export exposure)**

### Enterprise tier (controls + compliance)
`in-ca` supports:
- **standardized ingestion and validation gates**
- **traceability (“where did this come from?”)**
- **repeatable reporting across filings**

---

## Practical implementation note
- Store `in-ca` facts in a separate **Entity/Disclosure** bucket in your canonical model.
- Use `in-ca` primarily for:
  - **scaling rules**, **scope selection**, **risk scoring**, and **memo generation**.
- Keep your valuation math on canonical metrics derived mostly from `ind-as`, with `in-ca` as the **context layer**.

