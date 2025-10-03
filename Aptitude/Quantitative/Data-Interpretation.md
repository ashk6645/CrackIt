# Data Interpretation

>Status: 🟢 Complete — comprehensive guide with formats, strategies, solved example, and practice drill.

## 🚀 Quick Overview

Data Interpretation (DI) assesses your ability to read, process, and derive insights from structured or semi-structured data (tables, charts, caselets). Success depends on speed, accuracy, and approximation skill.

---

## 📊 Common DI Formats

| Format | Features | Typical Skills |
|--------|----------|----------------|
| Table | Multi-row/column | Row/column aggregation |
| Bar Chart | Comparative quantities | Relative difference & scaling |
| Line Graph | Trend over time | Rate of change |
| Pie Chart | Whole-to-part | Percentage composition |
| Stacked Chart | Layered contribution | Part + cumulative |
| Caselet | Paragraph narrative | Data extraction & structuring |
| Mixed Set | Combo of charts | Cross-reference |

---

## 🧠 Core Skills

- Percentage change: $(\text{New} - \text{Old})/\text{Old} \times 100$
- Ratio compression: Reduce early to simplify later steps
- Average = Total / Count
- Weighted average for grouped data
- Growth factor chaining for multi-year percentage changes

---

## 🛠️ Rapid Parsing Checklist

1. Scan axes / headings → note units (thousand, million, %)
2. Identify outliers (largest, smallest)
3. Pre-calc key totals (row sums / column sums)
4. Mark repeating ratios (e.g., 120:80 → 3:2)
5. Decide precision: exact vs approximation acceptable

---

## 🎯 Strategic Techniques

| Scenario | Technique | Why |
|----------|-----------|-----|
| Large numbers | Unit normalization | Avoid overflow errors |
| Close values | Ratio rather than subtraction | Faster relative comparison |
| Multi-year growth | Chain factors $(1+r_1)(1+r_2)$ | Avoid additive error |
| Pie chart | Convert angles ↔ % (360° ↔ 100%) | Faster segment estimation |
| Caselet | Tabulate before solving | Reduces rereads |

---

## 🧑‍💻 Sample Mini Set (Table)

Sales (in $\text{thousands}$) of Products A & B across Regions:

| Region | A | B |
|--------|---|---|
| North  | 120 | 150 |
| South  | 100 | 90 |
| East   | 80  | 110 |
| West   | 140 | 130 |

Questions:
1. Total sales of Product A?
2. Ratio of total B to total A?
3. % contribution of West (A+B combined)?
4. Region with highest A:B ratio?
5. If next year A grows 10% in all regions, new total A?

Solutions:
1. A total = 120+100+80+140 = 440
2. B total = 150+90+110+130 = 480 → 480:440 = 12:11
3. West combined = 140+130=270; Grand total = 440+480=920 → 270/920 ≈ 29.35%
4. Compute ratios: N 120:150=4:5, S 100:90=10:9, E 80:110=8:11, W 140:130=14:13 → Highest A:B = South
5. New A = 440 × 1.10 = 484

---

## � Practice Drill (12 Questions)

Use the same table above unless specified.

1. Difference between highest and lowest A sales.
2. Average sales of Product B.
3. If East B rises by 20%, new B total?
4. If West A drops by 10%, new A total?
5. Combined % share of North region.
6. Growth factor from 440 to 484 in %.
7. If a pie chart used, angle for South (A+B combined)?
8. CAGR for A if 3-year growth from 400 to 484?
9. Median of A values.
10. Weighted average price if A units weighted: North 2, South 1, East 1, West 3 (use A values).
11. Replace South B with 95; new B average?
12. If total target next year = 1000 (A+B), required % increase over 920?

---

## 📚 Additional Resources

- [Data Interpretation Basics (BYJU'S)](https://byjus.com/bank-exam/data-interpretation/)
- [Approximation Tricks (YouTube)](https://www.youtube.com/results?search_query=di+approximation+tricks)
- [Mock DI Sets (Career Launcher)](https://www.careerlauncher.com/cat/)

---

## 🎯 Answer Key

1. 140-80=60  2. 480/4=120  3. 110×1.2=132 ⇒ new total 480-110+132=502  4. 140→126 ⇒ new A total 426  5. North share = (120+150)/920 = 270/920 ≈ 29.35%  6. (484-440)/440 = 10%  7. South total = 190; 190/920×360 ≈ 74.35°  8. CAGR = (484/400)^{1/3}-1 ≈ (1.21)^{1/3}-1 ≈ 0.065 ~6.5%  9. A sorted: 80,100,120,140 ⇒ median = (100+120)/2=110  10. Weighted avg = (2·120 +1·100 +1·80 +3·140)/(2+1+1+3)= (240+100+80+420)/7=840/7=120  11. New avg = (480 - 90 + 95)/4 = 485/4=121.25  12. (1000-920)/920 ≈ 8.70%

---

>**Last Updated**: October 2025 | **Contributor**: CrackIt Team
