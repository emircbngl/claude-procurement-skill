# Domain: IT Software (SaaS, business software, developer tools)

Heavily B2B-skewed but applies to power-user B2C purchases too. Subscription dominates pricing; vendor lock-in, integration, and compliance dominate risk.

## Research dimensions
- **functional_specs**: feature matrix vs requirements, integration ecosystem (API quality + SDK + native connectors), scaling limits (seats / records / API calls / storage), uptime SLA (99.9% = 8.76hr/yr down; 99.99% = 52min/yr), security certifications (SOC 2 Type II, ISO 27001, ISO 27017, ISO 27018, FedRAMP, HIPAA-eligible) + applicable regional data-protection compliance (GDPR DPA, UK GDPR, CCPA, LGPD, PIPL, PDPA, KVKK, etc.), data residency, RBAC + audit log granularity
- **quality_signals**: G2 / Capterra / TrustRadius ratings + review patterns (filter for verified user reviews), Gartner Magic Quadrant / Forrester Wave position, Hacker News commentary, status-page uptime history, security disclosure record (public CVEs, breach history)
- **economic**: per-seat / per-user / consumption-based / flat / freemium / enterprise-only; annual vs monthly discount (10–20% common); switching cost (data export quality, vendor lock-in); implementation cost (often 1–3× annual license for enterprise rollouts); training cost; ongoing admin cost (FTE for big SaaS)
- **usage_fit**: solo / team (10–50) / midmarket (50–500) / enterprise (500+); horizontal (CRM, ITSM, comms) vs vertical (industry-specific); modern stack (API-first, integrations-led) vs legacy (heavy install, customization)

## Required user inputs (overrides universal)
- **Team size** + **growth trajectory** (per-seat pricing scales fast)
- **Existing stack** for integration requirements (Slack? Salesforce? Jira? Microsoft 365? Google Workspace?)
- **Compliance regime** (applicable regional data-protection law + industry obligations — HIPAA / GDPR / UK GDPR / CCPA / LGPD / PIPL / PDPA / KVKK / SOX / PCI-DSS, etc.) — gates the vendor list
- **Data residency requirements** (EU-only / TR-only / no-China etc.)
- **Procurement constraints** (must use existing approved vendor list, security review process, legal review timeline)
- **Implementation timeline** + change-management bandwidth
- **Budget tier** (free / SMB / mid-market / enterprise) — affects which vendors will quote

## Standards & compatibility axes

| Axis | Values | Compat rule |
|------|--------|-------------|
| **Authentication** | SAML 2.0 / OIDC / OAuth 2.0 / SCIM 2.0 (provisioning), MFA mandatory, passkeys | Enterprise mandates SSO via SAML/OIDC; SCIM auto-provisions/deprovisions; passwords-only = compliance gap |
| **API** | REST (most), GraphQL, gRPC, webhooks; rate limits; OpenAPI spec | API-first = integration leverage; rate-limited or no-API = lock-in risk |
| **Data export** | full CSV / JSON / API / no-export | Any contract without bulk export = data hostage situation |
| **Integration ecosystem** | native connectors (Zapier, Make, n8n, Workato, Tray.io marketplace) | Long-tail integrations via iPaaS; native > iPaaS > custom code |
| **Compliance certifications** | SOC 2 Type II (annual audit), ISO 27001 (ISMS), HIPAA-BAA (US healthcare), GDPR DPA, regional DP-law adherence (UK GDPR, CCPA, LGPD, PIPL, PDPA, KVKK, etc.), PCI-DSS for payments | Certification proof = SOC 2 report + signed DPA + BAA available |
| **Data residency** | US, EU, UK, multi-region; in-region vs replicated | Map to user's compliance requirement |
| **Encryption** | TLS 1.2+ in transit, AES-256 at rest, BYOK / HYOK for keys | BYOK = customer holds keys; HYOK = vendor never sees plaintext |
| **Audit log retention** | 30d / 90d / 1yr / configurable | Compliance often requires 1yr+; check if export to SIEM available |
| **RBAC granularity** | role-based / attribute-based / object-level | Enterprise needs ABAC or fine-grained RBAC |
| **Pricing model** | flat / per-seat / per-active-user / consumption / hybrid | Per-active-user friendlier than per-seat for variable usage |
| **Contract term** | monthly / annual / multi-year; auto-renewal notice | Annual = 10–20% discount; multi-year = additional discount but locks in price |
| **Vendor lock-in score** | data portability, API openness, switching cost | High lock-in = higher walk-away price acceptable; low lock-in = competitive negotiating position |

## Common pitfalls

- **Free tier becomes hostage situation** — invest months in vendor, hit free-tier ceiling, forced into expensive enterprise quote. Choose tools whose paid tier matches realistic future scale.
- **Per-seat pricing explosion** — 10 seats today, 100 next year, paying 10× while only using 50% of seats actively. Look for per-active-user or pooled licensing.
- **Acquihire / acquisition risk** — popular SaaS gets acquired (Salesforce buys Slack, Atlassian buys Trello), pricing/roadmap shifts. Larger vendor = more stable but also more aggressive monetization.
- **SOC 2 Type II "in progress"** — Type I is point-in-time, Type II is operational over 6+ months. "In progress" is not proof.
- **Vendor breach history** — check haveibeenpwned, vendor's transparency reports, news. Some vendors have repeat breaches.
- **No SAML on cheap tier** — common pattern: "enterprise" tier required for SSO, doubling the cost. SSO Tax (sso.tax) tracks this.
- **AI features added without consent for training** — many SaaS now train on customer data by default. Check DPA + AI addendum.
- **Implementation cost ignored** — Salesforce, NetSuite, SAP: implementation often 2–3× annual license. Budget reality check.
- **Open-source self-host vs SaaS** — self-host = no recurring license but ops/security/upgrade burden; SaaS = recurring but managed.
- **Currency exposure** — USD-denominated SaaS billed to TR account = TL exposure to USD/TRY swings. Negotiate TR pricing or fix annual.
- **Auto-renewal trap** — many contracts auto-renew with 30–90 day cancellation window; calendar reminder mandatory.

## Procurement-specific notes (B2B SaaS)

- **RFP / RFQ formal process** — Issue RFI to 5–8 vendors → shortlist 3 → RFP with detailed requirements → demo + reference calls → security review → procurement → legal → POC → contract.
- **Reference calls** — ask vendor for 2–3 customers similar in size/industry; check actual usage and pain points.
- **POC / pilot** — 30–60-day paid pilot common; insist on success criteria upfront.
- **Multi-vendor negotiation** — let vendors know they're in competition; final-quote-to-decision in 1–2 weeks creates urgency.
- **Procurement leverage** — end of vendor's fiscal quarter (often Mar/Jun/Sep/Dec) yields 10–25% discount.
- **MSA + DPA + BAA** — Master Service Agreement, Data Processing Addendum, Business Associate Agreement (US healthcare). All three for regulated workloads.

## Regional sourcing & compliance notes

- **Data-protection law**: vendor must accept the applicable regional DPA — GDPR (EU), UK GDPR, KVKK (Turkey), CCPA / CPRA (California), LGPD (Brazil), PIPEDA (Canada), PDPA (Singapore / Thailand), PIPL (China), APP (Australia), POPIA (South Africa). Verify named data processor list + sub-processor list.
- **Data residency**: many global hyperscalers (AWS, Azure, GCP) offer in-region availability zones (e.g., Frankfurt, London, Paris, Mumbai, Tokyo, Sydney, São Paulo, Istanbul, Bahrain). National sovereign-cloud alternatives exist in some regions for regulated workloads — verify per country.
- **Local SaaS scene**: most regions have local SaaS players that may compete with global tools on price, local language, and local regulatory fit (e.g., Logo / Mikrogen / Netsis in Turkey for ERP; SAP in DACH; local fintech and martech players globally). Evaluate alongside global options.
- **Invoicing / legal-entity issues**: some global SaaS bill only from a single jurisdiction (US, IE, NL), which may complicate VAT recovery, withholding tax, or local-entity accounting requirements. Confirm invoice issuer before signing.
- **Local language / support hours**: global SaaS may lack support in user's language or business hours. Local SaaS often wins on this dimension; factor into vendor risk.

## B2C variant (consumer / power-user software)

- Subscription fatigue real — every app wants monthly
- One-time purchase (Affinity Photo, BBEdit, OmniFocus) becoming rare premium positioning
- Family plans usually 30–50% cheaper per seat
- App Store / Play Store sandbox limits some features; web/standalone may be more capable
- Open source self-host options viable for power-users (Nextcloud, Bitwarden, Joplin, etc.)

## Trusted sources for web fallback

- [G2.com](https://www.g2.com), [Capterra](https://www.capterra.com), [TrustRadius](https://www.trustradius.com) — review aggregators
- [Gartner](https://www.gartner.com) Magic Quadrant + [Forrester Wave](https://www.forrester.com) — paywalled enterprise research
- [GetApp](https://www.getapp.com), [Software Advice](https://www.softwareadvice.com)
- [sso.tax](https://sso.tax) — SaaS that paywall SSO
- [Status pages](https://status.io) — vendor's published uptime
- Vendor's own [Trust Center](https://example.com/trust) — SOC 2, ISO 27001 listing
- [HackerNews `Show HN` + Comments](https://news.ycombinator.com) — developer community sentiment
- [Reddit r/sysadmin, r/devops, r/dataengineering](https://reddit.com/r/sysadmin) — operator feedback
- [LinkedIn / X for vendor competitive intel + recent news](https://www.linkedin.com)
