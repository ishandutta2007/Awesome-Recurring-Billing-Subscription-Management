# Awesome-Recurring-Billing-Subscription-Management

# Awesome Recurring Billing & Subscription Management

> A curated list of top Recurring Billing and Subscription Management platforms — both SaaS/Hosted commercial solutions and open-source alternatives for managing plans, invoices, payments, and revenue.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [Stripe Billing](#stripe-billing)
  - [Chargebee](#chargebee)
  - [Zuora](#zuora)
  - [Recurly](#recurly)
  - [Paddle](#paddle)
  - [Maxio](#maxio)
  - [Zoho Subscriptions](#zoho-subscriptions)
  - [Rebilly](#rebilly)
- [Open-Source Software](#-open-source-software)
  - [Lago](#lago)
  - [Kill Bill](#kill-bill)
  - [Flexprice](#flexprice)
  - [Invoice Ninja](#invoice-ninja)
  - [Akaunting](#akaunting)
  - [stapel-billing](#stapel-billing)
  - [BillCycle](#billcycle)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Recurring Billing and Subscription Management platforms. These are not open-source but are included as reference points for feature comparison.

### Stripe Billing
**Type:** Billing layer on top of Stripe payments
Stripe Billing is the lowest-friction option for teams already processing payments through Stripe: no new gateway, no new reconciliation surface, and one vendor for both payments and billing. It handles subscriptions, simple metered models, and invoicing with built-in Smart Retries, proration, and a hosted customer portal. **Trade-off:** You remain the merchant of record and own global tax compliance end to end; complex catalogs require custom engineering, and fees stack across processing, billing, and tax tooling.

### Chargebee
**Type:** Mature subscription management with usage add-ons
Chargebee is a mature subscription management platform known for handling almost every edge case in recurring billing logic, including complex trials, grandfathering, and multi-tier pricing. It offers robust invoicing, dunning, proration, and revenue reporting, with strong CRM and ERP integrations. **Trade-off:** It is not a merchant of record—you still manage your own payment gateway and tax compliance. Fees are additive to gateway costs.

### Zuora
**Type:** Enterprise monetization and revenue recognition
Zuora is the enterprise standard for subscription billing with deep revenue recognition (RevPro) capabilities, multi-entity support, and CPQ for large, complex organizations. It is designed for global scale and can handle multi-year deals, multiple currencies, and custom invoicing workflows. **Trade-off:** Enterprise-only pricing with complex implementation that typically requires a specialized system integrator; it is overkill for early or mid-stage SaaS.

### Recurly
**Type:** Subscription management with revenue recovery focus
Recurly is the closest like-for-like alternative to Chargebee: gateway-agnostic subscription management with a strong reputation for dunning and involuntary-churn recovery. Its recovery engine uses machine learning to determine the best time to retry failed transactions, and it has strong support for digital wallets. Pricing starts at $249/month plus 0.9% of billing volume.

### Paddle
**Type:** Merchant of Record for SaaS
Paddle acts as a merchant of record, handling payment processing, tax compliance, and subscription billing on your behalf. This removes the burden of global tax registration and remittance, making it attractive for indie SaaS and small teams selling internationally. Pricing is a percentage of revenue.

### Maxio
**Type:** Billing and financial operations for B2B SaaS
Maxio combines subscription billing with financial operations, targeting B2B SaaS companies with complex contracts, usage, and revenue recognition needs. It emerged from the merger of SaaSOptics and Chargify.

### Zoho Subscriptions
**Type:** Subscription billing within Zoho ecosystem
Zoho Subscriptions provides recurring billing, invoicing, and subscription management as part of the broader Zoho suite. It is the natural choice for organizations already using Zoho CRM or Books, with tight integration into the Zoho ecosystem.

### Rebilly
**Type:** Subscription and payment administration
Rebilly provides subscription management and payment operations with a focus on flexible payment gateway integrations and subscription lifecycle control. It is often evaluated alongside Recurly and Chargebee for mid-market subscription businesses.

---

## 🟩 Open-Source Software

Self-hosted, community-driven Recurring Billing and Subscription Management tools. The open-source ecosystem has matured significantly, with Lago and Kill Bill leading adoption.

### Lago
**Stack:** Ruby / PostgreSQL / Redis / ClickHouse | **License:** AGPL-3.0
Lago is the most widely adopted open-source billing platform, with **11k GitHub stars** and a Repoly health score of **96/100** with active development (62 commits in 90 days) [citation:2][citation:5]. It handles usage-based, subscription, prepaid, and hybrid pricing on a single engine. The community edition is free to self-host, but **the customer portal, role-based access, and on-prem deployment sit in Lago Premium** (quote-only) [citation:2]. Lago does not process payments itself—it calculates charges, generates invoices, and connects to Stripe, Adyen, and GoCardless for collection. **Important architectural note:** The free Docker/Postgres/Redis stack is not the architecture behind Lago's throughput figures; at high volumes, they moved events to ClickHouse with Kafka in front, keeping Postgres for everything else [citation:14]. **AGPLv3 has real terms:** the network clause means offering modified Lago as a service to third parties triggers source obligations [citation:14].  
**Best for:** Teams wanting the most established open-source billing engine with genuine usage metering and hybrid pricing, accepting AGPL licensing and the operational overhead of running the full stack.

### Kill Bill
**Stack:** Java / MySQL/MariaDB/PostgreSQL | **License:** Apache-2.0
Kill Bill is the most mature open-source subscription billing platform, **in production since 2010** and released under the permissive **Apache 2.0** license [citation:6][citation:15]. It manages the full subscription lifecycle: catalog (products, plans, phases, price lists), subscriptions, plan changes (immediate or end-of-term with automatic proration and credits), invoices, payments, and overdue accounts [citation:9]. It supports flat recurring, one-time fees, trials, multi-phase plans, tiered usage, seat-based quantities, add-ons, and bundles. Payment plugins exist for Stripe, Braintree (including PayPal), Adyen, and others, with tax plugins for Avalara AvaTax, Vertex, and Kintsugi [citation:9]. **Kaui** is the admin UI providing MRR, churn, subscription, invoice, and payment reports [citation:9]. **Trade-off:** Every operational cost applies in full with no vendor to escalate to; complexity is noted as a potential disadvantage, and documentation can be lacking in detail for some users [citation:8]. Aviate is the enterprise offer built on Kill Bill by the same team, adding a control plane, metering modules, and Level 3 support [citation:6].  
**Best for:** Teams with a strong platform function that have already decided to own billing operations and want a permissively licensed (Apache-2.0) alternative to AGPL, with deep catalog and plan-change control.

### Flexprice
**Stack:** Go / Kafka | **License:** AGPL-3.0
Flexprice is enterprise-grade open-source usage-based billing infrastructure for AI and SaaS companies, deployable in your own VPC, on-prem, or on Flexprice's managed cloud [citation:2]. Its key differentiator is that it is **the only project on one comparison list that puts both enterprise contract billing and real-time usage metering in the free tier** [citation:2]. Features include parent-child account hierarchies with pooled credits and commitments, ramped contracts, contract versioning with amendment history, audit trails on every pricing change, and an MCP server exposing every API operation to coding agents [citation:2]. It processes up to **1M events/sec** with Go + Kafka, and supports payment gateways including Stripe, Razorpay, Moyasar, and Nomod [citation:2]. **Trade-off:** The Kafka streaming dependency means you need someone who knows Kafka on the team [citation:2].  
**Best for:** AI and SaaS teams that need enterprise contract billing and real-time usage metering in one self-hostable system, billing customers across regions.

### Invoice Ninja
**Stack:** PHP / Laravel / MySQL | **License:** Elastic-2.0 (source-available)
Invoice Ninja is a powerful invoicing and billing tool that also handles subscriptions and recurring billing, with a health score of 96/100 and very active development (461-472 commits in 90 days) [citation:5][citation:11]. **Important caveat:** It is source-available under the **Elastic License 2.0**, not OSI-approved open source, which limits commercial reuse and redistribution [citation:5][citation:11].  
**Best for:** Teams primarily needing invoicing with basic recurring billing, accepting the source-available licensing terms.

### Akaunting
**Stack:** PHP | **License:** BUSL-1.1 (source-available)
Akaunting is accounting software designed for small businesses and freelancers, with a health score of 86/100 [citation:11]. It provides administrative tools for managing invoices, expenses, and basic financial operations. Like Invoice Ninja, it is source-available under a non-OSI license (BUSL-1.1), which limits commercial reuse.  
**Best for:** Small businesses wanting a self-hosted accounting admin interface with basic invoicing, accepting the restrictive license.

### stapel-billing
**Stack:** Python / Django | **License:** MIT
stapel-billing is a Django app providing payments and billing with per-user credit wallets, one-off credit packages, and recurring subscription plans [citation:12]. It includes Stripe-backed checkout and a self-service customer portal, idempotent webhooks, and a service-to-service debit endpoint. Part of the Stapel framework of composable Django apps, it can be deployed as a monolith or microservice.  
**Best for:** Django teams wanting a billing component with a built-in self-service portal, deployable within their existing Python stack.

### BillCycle
**Stack:** Python / FastAPI / PostgreSQL / Celery | **License:** Open Source
BillCycle is a subscription and usage-based billing engine for SaaS and subscription box e-commerce, handling complex recurring billing, plan upgrades/downgrades, and usage metering [citation:3]. It uses a state machine pattern with event sourcing, with Celery Beat for background jobs. **Important:** The PyPI release is v1.0.0 (10.9 kB) and the technical implementation is noted as "pending in next iteration" [citation:3].  
**Best for:** Developers wanting a reference architecture for a state-machine-based billing engine, accepting that the published release is early-stage.

---

## 📊 Comparison at a Glance

| Software | License | Stack | Usage Metering | Payment Processing | Self-Hosted | Best For |
|----------|---------|-------|----------------|---------------------|-------------|----------|
| **Stripe Billing** | Proprietary | Cloud | ✅ (Simple) | ✅ (Stripe) | ❌ | Stripe-native teams |
| **Chargebee** | Proprietary | Cloud | ✅ (Add-on) | Via gateway | ❌ | Subscription-first + overages |
| **Zuora** | Proprietary | Cloud | ✅ | Via gateway | ❌ | Enterprise revenue recognition |
| **Recurly** | Proprietary | Cloud | (Limited) | Via gateway | ❌ | Dunning + churn recovery |
| **Paddle** | Proprietary | Cloud | (Check) | ✅ (MoR) | ❌ | Global SaaS tax handling |
| **Lago** | AGPL-3.0 | Ruby/Postgres | ✅ Deep | Via gateway | ✅ | Proven OSS billing |
| **Kill Bill** | Apache-2.0 | Java | ✅ (Plugins) | Via plugins | ✅ | Permissive OSS + complex catalogs |
| **Flexprice** | AGPL-3.0 | Go/Kafka | ✅ 1M/sec | Via gateway | ✅ | AI/SaaS enterprise contracts |
| **Invoice Ninja** | Elastic-2.0 | PHP/MySQL | (Limited) | Via gateway | ✅ | Invoicing + basic recurring |
| **stapel-billing** | MIT | Django | (Credits) | ✅ Stripe | ✅ | Django billing + portal |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Recurring Billing or Subscription Management tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source (or clearly note if it is source-available but not OSI-approved, as with Invoice Ninja and Akaunting). Note that the open-source ecosystem is led by **Lago** (most established, 11k stars, health 96/100) and **Kill Bill** (Apache-2.0, production since 2010, deep catalog control). **Flexprice** is the notable entrant for AI/SaaS teams needing enterprise contract billing and high-volume metering in the free tier, accepting the Kafka operational dependency [citation:2]. For teams with hard data residency or regulatory requirements, Lago and Kill Bill remain the most battle-tested self-hosted options.

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
