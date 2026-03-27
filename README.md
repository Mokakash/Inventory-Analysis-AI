# 🔧 Inventory Analysis AI
An AI-powered inventory decision tool that replaces a manual, Excel-heavy workflow with an automated analysis engine — delivering actionable discontinuation recommendations and AI-written manager summaries in seconds.

---

## 🧩 The Problem
Wholesale distributors managing thousands of SKUs across multiple warehouse locations face a recurring challenge: identifying which items to discontinue, discount, or reorder requires pulling data from an ERP (like NetSuite, Oracle, ...), manually applying complex business rules in Excel (multiple files, multiple analysis), and then writing up findings for management — a process that could take hours every cycle.

---

## ✅ The Solution
This tool ingests a raw Inventory CSV export (exported from NetSuite) and automatically:
- Applies **5 category flags** (Never Sold, On Sale & Slow, Discontinued, Odd Size, Overstock & Slow)
- Calculates a **Weighted Average Demand** using a 4-2-1 adjusted model (30/90/365 sales window buckets)
- Computes a **Demand - Est. of Month Supply** for each SKU
- Consolidates **multi-location rows** into a single SKU-level view
- Assigns a **Priority score (1=Worst)** and **Risk Score** to every flagged item
- Generates an **AI-written manager summary** via the Claude API
- Exports a **formatted two-tab Excel file** (Location-Based + SKU-Based)

All of this runs locally in the browser — no backend, no server, no installation required.

---

## ⚙️ Configurable Settings Panel
The tool includes a fully configurable settings panel (click the ⚙️ button in the top right) — no code editing required.

| Setting Group | What You Can Configure |
|---------------|----------------------|
| **Exclusion Rules** | Classes to exclude, Brands to exclude (auto-filtered by class), New item window (months) |
| **Category Flag Thresholds** | Cat 2 slow sales limits, Cat 4 percentile cutoff, Cat 5 months of supply + all slow sales windows |
| **Risk Score Weights** | All 9 individual weight values (Never Sold, No Sales windows, per flag bonus, On Order penalty, Low Stock) |

- Changes apply **immediately** — click Save & Apply and the analysis re-runs on your loaded data instantly
- Settings **persist across sessions** via browser localStorage
- **Reset to Defaults** restores all original values with one click

---

## 🚀 How to Use
1. Clone or download this repo
2. Open `inventory_analysis_tool.html` in any modern browser (Chrome or Edge recommended)
3. Upload your inventory CSV export (have the fields you see in my "sample_inventory.csv" file before using the tool)
4. Review the stats dashboard and AI-generated summary
5. (Optional) Click ⚙️ Settings to adjust exclusions or thresholds, then Save & Apply
6. Download the full Excel report or flagged-items-only report

> 💡 A sample dataset is included in the `/data` folder to test the tool without real company data.

---

## 📊 Business Logic

### Category Flags
| Flag | Rule |
|------|------|
| Cat 1 - Never Sold | ALL Time sales = 0 |
| Cat 2 - On Sale & Slow | On Sale = Yes AND no sales in 6mo AND all-time < 50 |
| Cat 3 - Discontinued | Discontinued Item = Yes |
| Cat 4 - Odd Size | Raw Size is in bottom 25th percentile of 12mo sales for its category (Wheel/Tire calculated separately as their sizes are different — tool handles this automatically) |
| Cat 5 - Overstock & Slow | Months of supply ≥ 3 AND slow sales thresholds met across all time windows |

### Weighted Average Demand Formula
```
Weighted Avg = ROUND(((0-30 Days × 4) + ((31-90 Days / 2) × 2) + ((91-365 Days / 9) × 1)) / 7, 2)
```
Recent sales are weighted more heavily (4x) than older sales (1x), giving a demand-adjusted daily rate.

### Priority Scoring (1 = Worst)
| Priority | Condition |
|----------|-----------|
| 1 | Never sold AND 2+ category flags, OR 3+ flags |
| 2 | Never sold (single flag) |
| 3 | Exactly 2 category flags |
| 4 | No sales last 6 months, OR exactly 1 flag |
| 5 | All other flagged items |

---

## 🗂 Repository Structure
```
Inventory-Analysis-AI/
├── inventory_analysis_tool.html   ← the tool (open in browser to run)
├── changelog.md                   ← version history
├── data/
│   └── sample_inventory.csv       ← anonymized sample data for testing
└── README.md
```

---

## 🛠 Built With
- **Vanilla HTML/CSS/JavaScript** — runs locally, zero dependencies to install and it's FREE to use
- **PapaParse** — CSV parsing
- **SheetJS (xlsx)** — Excel export with formatting and borders
- **Anthropic Claude API** — AI-generated manager summaries
- **NetSuite** — ERP data source (CSV export)

---

## 👤 Author
Built by **Moka Kashinejad** — Head of Data & Analytics | AI & Data Strategy

[LinkedIn](https://linkedin.com/in/moka-kashinejad) · [GitHub](https://github.com/Mokakash)
