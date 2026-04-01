# OpenCredit Platform

A transparent, educational credit risk analysis tool that incorporates behavioral economics, alternative data, and FICO-aligned financial modeling to provide a comprehensive and realistic credit risk assessment.

## The Thesis Was Right

This platform was built in 2025 on a single premise: credit scoring is a black box, and that is a problem.

On 17 March 2026, SCHUFA - Germany's largest credit bureau - was compelled by a European Court of Justice ruling to publicly acknowledge exactly that. Under the ruling, SCHUFA replaced its opaque model (which used up to 100 criteria consumers could not see or verify) with a new transparent 12-criteria system, consolidated six industry-specific scores into one, switched from a percentage scale to a 100-999 point scale, and made the score freely viewable online for the first time in its history.

Consumers had previously been unable to understand, verify, or challenge how their scores were calculated. The ECJ ruled this was legally insufficient under GDPR. SCHUFA's reform was not voluntary - it was a court-mandated correction.

OpenCredit modeled transparent, explainable credit scoring before it was mandated. Every formula, every weight, every calculation step is visible in the Model Logic tab. That is not just an educational choice. As of March 2026, it is the direction the entire industry has been told to move.

Read SCHUFA's official announcement: https://www.schufa.de/newsroom/pressemitteilungen/neue-schufa-score-transparent-leicht-nachzurechnen/index.jsp

## What SCHUFA's Reform Still Does Not Solve

Even the reformed SCHUFA model remains limited to credit transaction history: which accounts exist, whether payments were missed, and how many credit applications were made. It does not incorporate income, savings, cash flow, financial habits, or any forward-looking indicators - because credit bureaus simply do not hold that data.

OpenCredit was designed from the start to go further:

- Cash flow and income stability - the most direct measure of actual repayment capacity
- Emergency fund depth - a borrower's buffer against unexpected financial shocks
- Behavioural economics signals - budgeting habits, financial goal-setting, and proactive planning
- Alternative assets - with risk-adjusted treatment (crypto at 50%, bullion at 90%)
- Macroeconomic and sector stress testing - forward-looking risk, not just historical payment data

Traditional bureaus score what happened in the past. This model asks: given your full financial picture today, how resilient are you to what could happen tomorrow?

## Features

### Multi-Dimensional Risk Analysis

**Payment History (40% Weight):** The most critical factor, covering credit cards, loans, rent, and utilities.

**Financial Health (30% Weight):** Comprehensive analysis of income, assets (including bullion and crypto with risk-adjusted haircuts), and debts.

**Behavioral and Stability (30% Weight):** Assesses financial habits (budgeting, goals) and life stability (employment, residency).

**Alternative Data Integration:** Incorporates modern data points like utility payment history and bank account cash flow - data points SCHUFA's bureau model cannot access.

**Country Risk Adjustments:** PPP-adjusted calculations with country-specific risk factors for the USA, Germany, and India.

### Dual-Perspective Interface

**Borrower View:** See your estimated score, understand what it means, and get a personalized report on how to improve it.

**Lender View:** See the financial metrics a lender would focus on, including risk-adjusted limits and Basel III-aligned metrics like Probability of Default (PD) and Expected Loss (EL).

### SCHUFA Score Simulator

An educational simulator built on SCHUFA's publicly announced 12 criteria (March 2026). Enter only the data a credit bureau actually holds - account history, address stability, credit applications - and see an estimated SCHUFA-style score alongside your OpenCredit score. The same person can look very different under each model, especially if they are asset-rich but credit-thin, recently relocated, or early in their credit history.

**Important:** SCHUFA has published its criteria but not its weights or formula. This simulator uses estimated weights derived from general credit risk principles and is clearly labelled as such. It is an independent educational tool with no affiliation to SCHUFA.

### Advanced Modeling and Transparency

**Economic Stress Testing:** Simulates the impact of a combined macroeconomic (country-specific) and sector-specific (industry) downturn on your score.

**Score Simulator:** Adjust inputs and recalculate to model how changes to financial behaviour affect borrowing capacity.

**Interactive Peer Comparison:** A bell curve chart that simulates your score against a typical population distribution for your selected country.

**Complete Transparency:** A Model Logic tab detailing every step of the calculation, including formulas, values, and the rationale behind every weight - including a direct comparison to the new SCHUFA 12-criteria model.

**Personalized Improvement Plan:** Generates a custom report with specific, actionable steps to improve your score.

**Self-Contained:** Runs as a single `index.html` file in any modern web browser with no installation required.

## Technology Stack

- **Core Logic:** JavaScript (ES6+)
- **Interface:** React 18 (run via in-browser Babel compiler)
- **Styling:** Tailwind CSS (loaded via CDN)
- **Visualizations:** Inline SVG components
- **Deployment:** Vercel (with server-side security headers via `vercel.json`)

## Risk Assessment Methodology

The model is designed to mirror the principles of established scoring systems like FICO, while extending beyond what bureau-only models can capture.

### Core Risk Components

**Payment History (40% weight):** The single most important factor. Evaluates your track record of paying bills on time across credit and non-credit accounts. Directly comparable to the payment default criterion in SCHUFA's new model.

**Financial Health (30% weight):** Analogous to FICO's "Amounts Owed." Assesses overall financial stability and capacity. Key metrics include Debt-to-Income (DTI) ratio, asset leverage, and liquid savings. This entire component has no equivalent in SCHUFA's bureau-data model.

**Behavioral and Stability (30% weight):** A proxy for FICO's "Length of Credit History," "New Credit," and "Credit Mix," extended to include proactive financial management and demographic stability. Partially overlaps with SCHUFA's address stability and account age criteria.

### OpenCredit vs. New SCHUFA 12-Criteria Model

| SCHUFA Criterion | SCHUFA Data Source | OpenCredit Coverage |
|---|---|---|
| Payment defaults (Negativmerkmale) | Bureau records | Payment History component (40% weight) |
| Insolvency entries | Court and bureau records | Not modelled - no bureau data used by design |
| Age of oldest credit account | Bureau records | Employment tenure and residency stability used as proxies |
| Years at current address | Bureau records | Residency status input in Demographics tab |
| Credit card and giro applications (12 months) | Bureau enquiry records | Not modelled - no bureau data used by design |
| Non-bank credit applications (12 months) | Bureau enquiry records | Not modelled - no bureau data used by design |
| Instalment loans taken (12 months) | Bureau records | Captured in secured and unsecured debt inputs |
| Number of active credit accounts | Bureau records | Partially captured via unsecured debt and payment inputs |

OpenCredit additionally models income, assets, cash flow, emergency fund depth, budgeting habits, and financial goals - dimensions the SCHUFA model does not include because credit bureaus do not hold that data.

### Score Scale Comparison (Approximate)

| OpenCredit | Category | US FICO | India CIBIL | Germany SCHUFA (new, points) |
|---|---|---|---|---|
| 85-100 | Excellent | 780-850 | 800+ | 900-999 |
| 75-84 | Very Good | 720-779 | 750-799 | 800-899 |
| 65-74 | Good | 680-719 | 700-749 | 700-799 |
| 55-64 | Fair | 620-679 | 650-699 | 600-699 |
| below 55 | Poor | below 620 | below 650 | below 600 |

Note: SCHUFA migrated to a 100-999 point scale on 17 March 2026, replacing the previous percentage-based Basisscore. Mapping is approximate - OpenCredit and SCHUFA use fundamentally different methodologies.

### Economic Stress Testing

Combines two factors to calculate a stress-adjusted score:

- **Macroeconomic Country Risk:** A simulated risk factor based on the selected country (e.g. market shock in the USA, energy crisis in Germany).
- **Sector-Specific Industry Risk:** A simulated risk factor based on the user's industry (e.g. higher risk for Technology and Retail, lower risk for Healthcare).

### Peer Comparison Simulation

The bell curve chart is a realistic simulation based on publicly available statistical data for each country.

- **USA:** Modeled on FICO Score distribution data from Experian.
- **Germany:** Modeled on SCHUFA's published score class distribution.
- **India:** Modeled on analyses of CIBIL score ranges from major financial institutions.

## How to Use

**Online:** The platform is deployed on Vercel. Open it in any modern web browser — no installation required.

**Locally:** Clone the repository and open `index.html` directly in Chrome, Firefox, or Edge. No build step needed.

## Model Assumptions and Limitations

- **Not statistically validated:** The model's logic is grounded in published financial principles, but it has not been backtested against a real-world dataset of loan outcomes.
- **Self-reported inputs:** Accuracy depends entirely on the honesty of the user. SCHUFA uses verified bureau records. OpenCredit uses what you tell it.
- **Static and deterministic:** Provides a snapshot. Does not account for dynamic macroeconomic factors not already captured in the stress test.
- **Linear relationships:** Assumes mostly linear relationships between factors and risk. Real-world models are more complex.
- **Estimated SCHUFA weights:** The SCHUFA simulator uses estimated weights. SCHUFA's actual formula and weights have not been published.

## Important Disclaimer

**Educational Purpose:** This tool is designed for educational and illustrative purposes only.

**Not Financial Advice:** The score generated is based on a transparent, generalized model and is not an official credit score. It does not constitute financial, investment, or credit advice.

**No Official Affiliation:** The calculations are not affiliated with, endorsed by, or connected to any official credit rating agency like SCHUFA, CRISIL, Experian, Equifax, or TransUnion. The SCHUFA Score Simulator is an independent educational estimate only.

**Simulated Comparison:** The peer comparison chart is a simulation based on publicly available statistical data and does not reflect live user data.

Always consult with a qualified financial professional and refer to your official credit report for actual lending decisions.

## Privacy

All calculations run entirely in your browser. No data is ever transmitted to a server, stored in a database, or shared with any third party. No cookies are set and no analytics are collected.

The only external connections are:
- CDN delivery of React 18.3.1, Babel 7.26.4, and Tailwind CSS (unpkg.com, cdn.tailwindcss.com)
- Google Fonts (fonts.googleapis.com / fonts.gstatic.com) for the Inter typeface

If you prefer zero external connections, self-host the font and pre-compile the JSX with the Babel CLI or Vite.

## License

This project is released under the [Apache License 2.0](LICENSE). See `LICENSE` for full terms.

## Security

See [SECURITY.md](SECURITY.md) for the vulnerability disclosure policy and dependency information.

---

Built with care for financial literacy and transparency.
