# CarbonLens — SWDM v4 Website Carbon & Energy Auditor

**CarbonLens** is a full-stack web sustainability auditing platform that measures the real-time carbon footprint of any live website using the **Sustainable Web Design Model Version 4 (SWDM v4)** and **The Green Web Foundation API**.

## Features
- **Live DNS & Domain Validation:** Rejects malformed or non-existent domains before auditing.
- **Resource-Level Payload Breakdown:** Categorizes transferred bytes across HTML, JavaScript, CSS, and Images with an interactive Chart.js donut chart.
- **SWDM v4 Carbon & Energy Engine:** Calculates operational + embodied emissions across Data Centers, Networks, and User Devices using `494 gCO2e/kWh` global grid intensity.
- **Head-to-Head Website Comparison:** Audits two websites in parallel to highlight the cleaner site and percentage carbon savings.
- **Annual Impact Simulator & Eco-Badge:** Simulates annual CO2, kWh, car driving distance, and tree offsets for 1k–500k monthly visitors, plus generates an embeddable HTML eco-badge.

## Quick Start
```bash
npm install
npm start
```
Open `http://localhost:3000` in your browser.
