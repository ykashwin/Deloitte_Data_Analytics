# Daikibo Industrials: Telemetry Operational Audit & Forensic Pay Equity Analysis

This repository contains the end-to-end analytical deliverables, interactive diagnostic dashboards, and forensic pay-equity classifications conducted for **Daikibo Industrials** as part of the Deloitte Technology Consulting Virtual Experience.

---

## 1. Executive Summary & Core Findings

### Track 1: Factory Telemetry & Equipment Downtime Analysis
- **Dataset:** 160,704 unified telemetry messages logged at 10-minute heartbeat intervals across 4 manufacturing plants during May 2021.
- **Downtime Metric:** Each unhealthy status ping corresponds to 10 minutes of operational downtime (`SUM(Unhealthy)`).
- **Core Insights:**
  1. **Primary Operational Bottleneck (Question 1):** **Daikibo Factory Seiko** (Osaka, Japan) recorded the highest downtime fleet-wide at **480 minutes** (followed by Shenzhen at 420 mins, Meiyo at 110 mins, and Berlin at 20 mins).
  2. **Root Failure Mechanism (Question 2):** Applying cross-filtering to Seiko isolates **LaserWelder** as the sole contributor, accounting for **100% (480 minutes)** of all downtime in the plant. All other 8 equipment classes at Seiko operated with zero recorded downtime.

### Track 2: Forensic Gender Pay Equity Investigation
- **Dataset:** 37 compensation benchmarks across 4 factory sites and 11 distinct operational and executive tiers.
- **Metric Scale:** Equality Score ranging from `-100` to `+100` (where `0` denotes parity).
- **Core Insights:**
  1. **Management & Executive Disparity:** Upper management tiers (C-Level, VP, Director, and Senior Manager) universally skew deeply negative (`-14` to `-26`), falling into **Unfair** and **Highly Discriminative** classifications across all locations.
  2. **Shop-Floor Parity:** Technical and shop-floor production roles (Sr. Engineer, Engineer, Jr. Engineer, and Machine Operator) sit squarely within the **Fair** boundary ($\pm 10$).

---

## 2. Repository Structure

```text
├── README.md                                  # Executive briefing and architectural overview
├── Daikibo_Equality_Table_Completed.xlsx     # Forensic pay equity classification table (Excel)
├── daikibo_telemetry_tableau_dashboard.png    # Interactive Tableau diagnostic dashboard screenshot
└── data/
    ├── Task 5 Equality Table.xlsx            # Baseline pay equity input data
    └── daikibo-telemetry-data.json.zip        # Raw 10-minute telemetry heartbeat dataset
```

---

## 3. Telemetry Dashboard Specification

- **Tool:** Tableau Desktop / Tableau Public
- **Calculated Field (`Unhealthy`):**
  ```tableau
  IF [status] = "unhealthy" THEN 10 ELSE 0 END
  ```
- **Visual Design:**
  - **Sheet 1 (`Down Time per Factory`):** Bar chart tracking `SUM(Unhealthy)` against `Factory`, configured with **Use as Filter: ON**.
  - **Sheet 2 (`Down Time per Device Type`):** Bar chart tracking `SUM(Unhealthy)` against `Device Type`.
  - **Interactive Action:** Selecting `daikibo-factory-seiko` in Sheet 1 dynamically filters Sheet 2 to display the device downtime distribution specifically for the Osaka facility.

![Tableau Dashboard](daikibo_telemetry_tableau_dashboard.png)

---

## 4. Forensic Pay Equity Classification Framework

- **Classification Rules:**
  - **Fair:** Scores between `-10` and `+10` (inclusive).
  - **Unfair:** Scores between `-20` and `-11`, or `+11` and `+20`.
  - **Highly Discriminative:** Scores `<-20` or `>+20`.

- **Excel Formula (`D2:D38`):**
  ```excel
  =IF(OR(C2<-20, C2>20), "Highly Discriminative", IF(OR(C2<-10, C2>10), "Unfair", "Fair"))
  ```

### Consolidated Pay Equity Matrix

| Factory | Job Role | Equality Score | Equality Class |
| :--- | :--- | :---: | :--- |
| **Daikibo Factory Meiyo** | C-Level | -25 | Highly Discriminative |
| **Daikibo Factory Meiyo** | VP | -26 | Highly Discriminative |
| **Daikibo Factory Meiyo** | Director | -19 | Unfair |
| **Daikibo Factory Meiyo** | Sr. Manager | -15 | Unfair |
| **Daikibo Factory Meiyo** | Manager | -14 | Unfair |
| **Daikibo Factory Meiyo** | Jr. Manager | -20 | Unfair |
| **Daikibo Factory Meiyo** | Sr. Engineer | -5 | Fair |
| **Daikibo Factory Meiyo** | Engineer | -8 | Fair |
| **Daikibo Factory Meiyo** | Jr. Engineer | 3 | Fair |
| **Daikibo Factory Meiyo** | Operational Support | -22 | Highly Discriminative |
| **Daikibo Factory Meiyo** | Machine Operator | -7 | Fair |
| **Daikibo Factory Seiko** | VP | -19 | Unfair |
| **Daikibo Factory Seiko** | Director | -10 | Fair |
| **Daikibo Factory Seiko** | Sr. Manager | -21 | Highly Discriminative |
| **Daikibo Factory Seiko** | Manager | -21 | Highly Discriminative |
| **Daikibo Factory Seiko** | Jr. Manager | -24 | Highly Discriminative |
| **Daikibo Factory Seiko** | Sr. Engineer | -4 | Fair |
| **Daikibo Factory Seiko** | Engineer | -7 | Fair |
| **Daikibo Factory Seiko** | Jr. Engineer | 4 | Fair |
| **Daikibo Factory Seiko** | Operational Support | -19 | Unfair |
| **Daikibo Factory Seiko** | Machine Operator | -5 | Fair |
| **Daikibo Berlin** | Sr. Manager | -15 | Unfair |
| **Daikibo Berlin** | Manager | -16 | Unfair |
| **Daikibo Berlin** | Jr. Manager | -17 | Unfair |
| **Daikibo Berlin** | Sr. Engineer | 4 | Fair |
| **Daikibo Berlin** | Engineer | 2 | Fair |
| **Daikibo Berlin** | Jr. Engineer | 4 | Fair |
| **Daikibo Berlin** | Operational Support | 0 | Fair |
| **Daikibo Berlin** | Machine Operator | -6 | Fair |
| **Daikibo Shenzhen** | Sr. Manager | -21 | Highly Discriminative |
| **Daikibo Shenzhen** | Manager | -19 | Unfair |
| **Daikibo Shenzhen** | Jr. Manager | -20 | Unfair |
| **Daikibo Shenzhen** | Sr. Engineer | -5 | Fair |
| **Daikibo Shenzhen** | Engineer | -4 | Fair |
| **Daikibo Shenzhen** | Jr. Engineer | 3 | Fair |
| **Daikibo Shenzhen** | Operational Support | -7 | Fair |
| **Daikibo Shenzhen** | Machine Operator | -7 | Fair |

---

## 5. Strategic Recommendations

1. **Targeted Maintenance Overhaul (Seiko):** Dispatch OEM field technicians specifically for the **LaserWelder** line in Osaka; general preventative maintenance across the other 8 machine classes is currently delivering 100% operational uptime.
2. **Executive Compensation Audit:** Immediately freeze discretionary variable compensation adjustments across leadership tiers until external parity benchmarks are established for VP and Senior Manager bands.
