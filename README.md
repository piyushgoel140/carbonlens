# 🌿 CarbonLens — Real-Time Website Carbon & Energy Auditor (SWDM v4)

[![Live Demo](https://img.shields.io/badge/Live_Demo-Render_Cloud-10B981?style=for-the-badge&logo=render&logoColor=white)](https://carbonlens-ytk3.onrender.com)
[![Methodology](https://img.shields.io/badge/Model-SWDM_v4_(494_gCO2%2FkWh)-0284C7?style=for-the-badge)](https://sustainablewebdesign.org/calculating-digital-emissions/)
[![Node.js](https://img.shields.io/badge/Runtime-Node.js_v20_LTS-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)

**Live Web App:** 👉 **[https://carbonlens-ytk3.onrender.com](https://carbonlens-ytk3.onrender.com)**  
*(Note: Hosted on Render's free tier—if the server has been idle, allow ~30 seconds on the first request for cold-start wake-up.)*

**CarbonLens** is a full-stack web sustainability auditing platform that measures the real-time environmental footprint of any live website. By inspecting transferred page weights across HTML, JavaScript, CSS, and Images and verifying renewable hosting infrastructure via **The Green Web Foundation API**, CarbonLens translates raw network telemetry into actionable carbon metrics using the **Sustainable Web Design Model Version 4 (SWDM v4)**.

---

## ✨ Key Features

- **Live DNS & Domain Validation:** Verifies URL syntax and resolves live DNS records (`dns.promises`) prior to auditing, immediately disqualifying malformed or non-existent domains.
- **Resource-Level Payload Breakdown:** Parses DOM tags (`<script>`, `<link rel="stylesheet">`, `<img>`) and inspects HTTP `Content-Length` headers to visualize exact kilobyte splits in an interactive **Chart.js** donut chart.
- **SWDM v4 Operational + Embodied Carbon Engine:** Computes both operational electricity emissions (`0.194 kWh/GB`) and hardware manufacturing embodied emissions (`0.106 kWh/GB`) across **End-User Devices (54%)**, **Transmission Networks (24%)**, and **Data Centers (22%)**.
- **Green Hosting Verification:** Queries **The Green Web Foundation Greencheck API v3** in real time to verify whether target servers run on renewable energy.
- **Head-to-Head Website Comparison (`VS` Mode):** Audits two competing domains in parallel (`Promise.all`) to determine which website is cleaner and by what percentage.
- **Interactive Annual Impact Simulator:** Simulates yearly CO2 (`kg`), electricity (`kWh`), equivalent petrol car driving distance (`km`), and trees required to offset emissions across `1,000` to `500,000` monthly page views.
- **Embeddable Eco-Badge & Local Scan History:** Generates a 1-click copyable sustainability badge snippet and stores recent audits in browser `localStorage`.

---

## 🏗️ System Architecture

```text
[User Browser / Mobile UI] (Tailwind CSS + Chart.js)
          │
          ├──► POST /api/audit   { url }
          └──► POST /api/compare { urlA, urlB }
                    │
                    ▼
   [Node.js + Express Backend (server.js)]
     ├─ 1. URL Normalizer & Live DNS Lookup (dns.promises)
     ├─ 2. HTTP Fetch & Cheerio Asset Categorizer (HTML, JS, CSS, Images)
     ├─ 3. Green Web Foundation API Check (Renewable Hosting Status)
     └─ 4. SWDM v4 Calculation Engine (Operational + Embodied gCO2e)
                    │
                    ▼
   [JSON Telemetry Response & Interactive Dashboard]
```

---

## 📐 Carbon Calculation Methodology (SWDM v4)

CarbonLens implements the peer-reviewed **Sustainable Web Design Model Version 4 (SWDM v4)** with the global average grid carbon intensity of **494 gCO2e/kWh**:

1. **Effective Data Transfer (GB):**  
   Accounts for 75% first-time visitors (100% asset download) and 25% returning visitors (2% cached download):
   `Effective Data (GB) = (Total Bytes / 1024^3) * 0.755`

2. **Operational & Embodied Emissions (gCO2e):**  
   `Operational (g) = Effective Data (GB) * [0.055 * (1 - G) + 0.059 + 0.080] * 494`  
   `Embodied (g) = Effective Data (GB) * [0.012 + 0.013 + 0.081] * 494`  
   *(where `G = 1` if verified as a Green Host, eliminating operational data center emissions, and `G = 0` otherwise).*

3. **Total Carbon Footprint per Page View:**  
   `CO2 per View (g) = Operational (g) + Embodied (g)`

### Digital Carbon Rating Scale

| Eco Grade | CO2 per Page View (gCO2e) | Global Benchmark |
| :--- | :--- | :--- |
| **A+** | <= 0.040 g | Cleaner than 95% of web pages globally |
| **A** | 0.041 g - 0.079 g | Cleaner than 85% of web pages globally |
| **B** | 0.080 g - 0.145 g | Above-average carbon efficiency |
| **C** | 0.146 g - 0.209 g | Near global median webpage footprint |
| **D** | 0.210 g - 0.278 g | Heavy payload; asset optimization advised |
| **E / F** | > 0.278 g | High carbon footprint; critical optimization needed |

---

## 🔌 REST API Endpoints

### `POST /api/audit`
Audits a single website URL and returns full SWDM v4 metrics, resource breakdown, and recommendations.
```json
{ "url": "wikipedia.org" }
```

### `POST /api/compare`
Audits two websites in parallel and returns side-by-side telemetry.
```json
{ "urlA": "wikipedia.org", "urlB": "bbc.com" }
```

---

## 🛠️ Tech Stack & Project Structure

- **Backend:** Node.js (v20 LTS), Express.js, `dns.promises`
- **Scraping & HTTP Inspection:** Axios, Cheerio
- **External API:** The Green Web Foundation Greencheck API v3
- **Frontend & Visualizations:** HTML5, Tailwind CSS, Chart.js v4, Vanilla ES6+ JavaScript
- **Cloud Hosting:** GitHub & Render Web Services

```text
carbonlens/
├── package.json          # Dependencies (express, axios, cheerio) and start script
├── server.js             # Express REST API, DNS validator, Green Web API & SWDM v4 engine
├── README.md             # Project documentation
├── .gitignore            # Excludes node_modules and environment logs
└── public/
    └── index.html        # Responsive dashboard, Chart.js donut, simulator & VS compare UI
```

---

## 🚀 Running Locally

```bash
git clone https://github.com/piyushgoel140/carbonlens.git
cd carbonlens
npm install
npm start
```
Open **`http://localhost:3000`** in your browser.

---

## ⚠️ Known Limitations & Future Scope
- **Static DOM Inspection:** Uses Cheerio to inspect initial HTML and linked static assets rather than executing a full headless Chromium instance; scroll-triggered lazy-loaded assets are not captured yet.
- **Future Enhancements:** Puppeteer/Playwright waterfall auditing, MongoDB historical trend persistence, and a GitHub Action CI/CD carbon-budget gate.

---

## 🎓 Academic Context
Developed as a **7th-Semester B.Tech (Computer Science & Engineering) Minor Project** at the **Institute of Innovation in Technology and Management (IITM), Janakpuri** (Affiliated to **Maharshi Dayanand University, Rohtak**).
