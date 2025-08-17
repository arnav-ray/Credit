OpenCredit Platform
A transparent, educational credit risk analysis tool that incorporates behavioral economics, alternative data, and FICO-aligned financial modeling to provide a comprehensive and realistic credit risk assessment.

🚀 Features
Multi-Dimensional Risk Analysis
Financial Health (30% Weight): Comprehensive analysis of income, assets (including bullion & crypto), and debts.

Payment History (40% Weight): The most critical factor, covering credit cards, loans, rent, and utilities.

Behavioral & Stability (30% Weight): Assesses financial habits (budgeting, goals) and life stability (employment, residency).

Alternative Data Integration: Incorporates modern data points like utility payment history and bank account cash flow.

Country Risk Adjustments: PPP-adjusted calculations with country-specific risk factors for the USA, Germany, and India.

Dual-Perspective Interface
Borrower View: See your estimated score, understand what it means, and get a personalized report on how to improve it.

Lender View: See the financial metrics a lender would focus on, including risk-adjusted limits and Basel III-aligned metrics like Probability of Default (PD) and Expected Loss (EL).

Advanced Modeling & Transparency
Economic Stress Testing: Simulates the impact of a combined macroeconomic (country-specific) and sector-specific (industry) downturn on your score.

Interactive Peer Comparison: A bell curve chart that simulates your score against a typical population distribution for your selected country.

Complete Transparency: An "About" section explaining the platform's purpose and a "Model Logic" tab detailing every step of the calculation, including formulas, values, and the rationale behind the weights.

Personalized Improvement Plan: Generates a custom report with specific, actionable steps to improve your score.

Self-Contained: Runs as a single index.html file in any modern web browser with no installation required.

🛠️ Technology Stack
Core Logic: JavaScript (ES6+)

Interface: React 18 (run via in-browser Babel compiler)

Styling: Tailwind CSS (loaded via CDN)

Visualizations: Inline SVG components

📊 Risk Assessment Methodology
The model is designed to mimic the principles of established scoring systems like FICO.

Core Risk Components
Payment History (40% weight): The single most important factor. It evaluates your track record of paying bills on time across various credit and non-credit accounts.

Financial Health (30% weight): Analogous to FICO's "Amounts Owed." This component assesses your overall financial stability and capacity. Key metrics include Debt-to-Income (DTI) ratio, asset leverage, and liquid savings.

Behavioral & Stability Factors (30% weight): A proxy for FICO's "Length of Credit History," "New Credit," and "Credit Mix." This includes proactive financial management (budgeting, goals) and demographic stability (employment tenure).

Economic Stress Testing
The stress test provides a forward-looking risk perspective. It combines two factors to calculate a stressFactor, which is then used to derive a "Stressed Score":

Macroeconomic Country Risk: A simulated risk factor based on the selected country (e.g., market shock in the USA, energy crisis in Germany).

Sector-Specific Industry Risk: A simulated risk factor based on the user's industry of employment (e.g., higher risk for Technology and Retail, lower risk for Healthcare).

Peer Comparison Simulation
The bell curve chart is a realistic simulation, not a live comparison. Its shape is based on publicly available statistical data for each country to provide meaningful context.

USA: Modeled on FICO® Score distribution data from Experian.

Germany: Modeled on SCHUFA's published score class distribution.

India: Modeled on analyses of CIBIL score ranges from major financial institutions.

💻 How to Use
This application is a single, self-contained HTML file. No installation is needed.

Save the Code: Copy the entire code from the index.html file.

Create a File: Paste the code into a new text file on your computer.

Name the File: Save the file with the name index.html.

Open in Browser: Double-click the index.html file to open it in any modern web browser (like Chrome, Firefox, or Edge).

🚨 Important Disclaimer
Educational Purpose: This tool is designed for educational and illustrative purposes only.

Not Financial Advice: The score generated is based on a transparent, generalized model and is not an official credit score. It does not constitute financial, investment, or credit advice.

No Official Affiliation: The calculations are not affiliated with, endorsed by, or connected to any official credit rating agency like SCHUFA, CRISIL, Experian, Equifax, or TransUnion.

Simulated Comparison: The peer comparison chart is a simulation based on publicly available statistical data and does not reflect live user data.

Professional Review Required: Always consult with a qualified financial professional and refer to your official credit report for actual lending decisions.

Built with ❤️ for financial literacy and transparency.
