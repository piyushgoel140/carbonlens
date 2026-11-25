# CarbonLens — Real-Time Website Carbon & Energy Auditor

**CarbonLens** is a lightweight full-stack web application that audits any live website URL in real time to measure its page weight, check renewable energy hosting status, and calculate carbon dioxide emissions ($\text{gCO}_2\text{e}$) per page view using the **Sustainable Web Design (SWD)** methodology.

---

## Features
- **Real-Time Page Weight Auditing:** Downloads target HTML and inspects linked `<script>`, `<link rel="stylesheet">`, and `<img>` assets to compute total transferred bytes.
- **DNS & Domain Validation:** Verifies live domain syntax and DNS resolution before auditing, immediately rejecting invalid or non-existent URLs.
- **Green Hosting Verification:** Integrates **The Green Web Foundation API** to verify whether the target server runs on renewable energy infrastructure (`332 gCO2/kWh` vs. `442 gCO2/kWh` standard grid).
- **SWD Carbon Calculation & Eco-Grading:** Computes energy consumption (`kWh`), carbon emissions per visit (`gCO2e`), annual carbon impact (`kg/year` at 10,000 monthly views), and assigns an **A+ to F** sustainability grade.
- **Actionable Optimization Tips:** Generates tailored recommendations (asset compression, image lazy-loading, green hosting migration) based on audit metrics.

---

## Tech Stack
- **Backend:** Node.js (v20 LTS), Express.js
- **HTTP & HTML Parsing:** Axios, Cheerio, Node `dns.promises`
- **External API:** The Green Web Foundation Greencheck API v3
- **Frontend:** HTML5, Tailwind CSS, Vanilla JavaScript
- **Deployment:** GitHub & Render Cloud Platform

---

## Carbon Calculation Formula (SWD Model)
1. **Effective Data Transfer (GB):**  
   $$\text{Effective Data (GB)} = \frac{\text{Total Bytes}}{1024^3} \times 0.755$$
   *(Accounts for 75% first-time visitors loading 100% of assets and 25% returning visitors loading 2% cached assets.)*
2. **Operational Energy per Visit (kWh):**  
   $$\text{Energy (kWh)} = \text{Effective Data (GB)} \times 0.81$$
3. **Carbon Emissions per Page View ($\text{gCO}_2\text{e}$):**  
   $$\text{CO}_2\text{ (g)} = \text{Energy (kWh)} \times \text{Grid Intensity}$$

---

## Local Setup & Installation
```bash
# 1. Clone the repository
git clone [https://github.com/](https://github.com/)piyushgoel40/carbonlens.git
cd carbonlens

# 2. Install dependencies
npm install

# 3. Start the server
npm start
