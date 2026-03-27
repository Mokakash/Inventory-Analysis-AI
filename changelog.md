# Changelog

All notable changes to Inventory AI Tool are documented here.
Format: `[version] - YYYY-MM-DD — description`

---

## [2.0] - 2026-03-27
### Added
- Configurable settings panel (⚙️ button in header) with Save & Apply
- Class multi-select exclusion — exclude entire classes from discontinuation recommendations
- Brand multi-select exclusion — dynamically filters to only show brands from non-excluded classes
- New item window configurable (default 3 months) — controls Newer vs Older Inventory labeling
- All category flag thresholds configurable: Cat 2 (On Sale & Slow), Cat 4 (Odd Size percentile), Cat 5 (Overstock & Slow — months of supply + all slow sales limits)
- All 9 risk score weights configurable (Never Sold, No Sales windows, per flag, Cat 4/5 bonuses, On Order penalty, Low Stock bonus)
- Settings persist across sessions via localStorage
- Reset to Defaults button — restores all thresholds and clears exclusions
- Status bar confirms active exclusions after every run
- Save & Apply immediately re-runs analysis without needing to re-upload file

---

## [1.2] - 2026-03-25
### Added
- Combined single tool: Location-Based + SKU-Based analysis in one file
- Two-tab Excel export (Location-Based Data + SKU-Based Data) using SheetJS
- Cat 4 - Odd Size: calculates 25th percentile of 12-month sales by Raw Size, split by Class (Wheel vs Tire)
- Cat 5 - Overstock & Slow: Weighted Avg Demand 4-2-1 (30/90/365) + months of supply > 3 AND slow sales conditions
- Demand - Est. of Month Supply column with 4 outcome LET logic
- Side-by-side manager summaries — separate Location-Level and SKU-Level insights
- Stats dashboard updated with Cat 4 and Cat 5 counts
- Borders and number formatting in Excel export (decimals for cost/price, 1000 separator for quantities)
- All formula column headers renamed to match original Excel template exactly

### Fixed
- Priority 3 bug — condition order corrected in scoring logic
- Broken emoji character in Reason column replaced with plain text [On Order]
- Download blocked in Claude.ai sandbox — tool runs locally as .html file
- 0-30 Days trailing space handled for both column name variants

---

## [1.1] - 2026-03-25
### Added
- SKU-level consolidation tool (tool-v2): consolidates multi-location rows into single SKU rows
- Aggregation logic: SUM for quantities, MAX for costs & last-dates, MIN for first-dates
- Max of Location Average Cost column positioned after Average Cost
- Location Available / On Order / On Water header simplification in SKU tab
- Inventory Location populated with "All Locations" in SKU tab
- Flagged-only download option sorted by Risk Score

---

## [1.0] - 2026-03-25
### Added
- Initial location-level analysis tool
- CSV upload and parsing via PapaParse
- Cat 1 (Never Sold), Cat 2 (On Sale & Slow), Cat 3 (Discontinued) category flagging
- Recommend Discontinue logic with full exclusion rules (Assembly, New Items, Amani brand)
- Priority scoring (1=Worst) and Risk Score
- AI-generated manager summary via Anthropic Claude API
- Stats dashboard (total SKUs, flagged, priority 1, never sold, on order)
- Top 100 flagged items table sorted by risk score
- CSV download of full results
