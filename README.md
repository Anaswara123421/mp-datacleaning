# mp_datacleaning.xlsx — README

## Overview
This workbook contains a cleaned fashion-retail dataset covering product sales, pricing, stock, customer ratings, and returns. It has **3 sheets**, two of which contain data.

| Sheet | Contents | Rows | Columns |
|---|---|---|---|
| `Sheet2` | Main cleaned dataset — one row per product record | 2,176 | 14 |
| `Sheet3` | Return-reason summary (pivot/count table) | 6 | 2 |
| `Sheet1` | Empty | 0 | 0 |

---

## Sheet2 — Main Dataset

Each row represents one product listing/transaction, uniquely identified by `product_id` (no duplicates).

| Column | Type | Description | Values / Range |
|---|---|---|---|
| `product_id` | Text | Unique product identifier | e.g. `FB000001`–`FB002176` |
| `category` | Text | Product category | Accessories, Bottoms, Dresses, Outerwear, Shoes, Tops |
| `brand` | Text | Brand name | Ann Taylor, Banana Republic, Forever21, Gap, H&M, Mango, Uniqlo, Zara |
| `season` | Text | Season tag | Fall, Spring, Summer, Winter |
| `size` | Text | Product size | XS, S, M, L, XL, XXL |
| `color` | Text | Product color | Beige, Black, Blue, Brown, Gray, Green, Navy, Pink, Purple, Red, White |
| `original_price` | Numeric | Original listed price | $15.14 – $249.98 |
| `markdown_percentage` | Numeric | Discount applied (%) | 0.0 – 59.9 |
| `current_price` | Numeric | Price after markdown | $7.29 – $249.98 |
| `purchase_date` | Date | Date of purchase | 2024‑08‑06 to 2025‑08‑06 |
| `stock_quantity` | Integer | Units remaining in stock | 0 – 50 |
| `customer_rating` | Numeric | Customer rating | 1.0 – 5.0 |
| `is_returned` | Text | Whether the item was returned | Yes (320 rows) / No (1,856 rows) |
| `return_reason` | Text | Reason for return (only meaningful when `is_returned` = Yes) | Changed Mind, Color Mismatch, Damaged, Quality Issue, Size Issue, Wrong Item |

**Data quality notes:**
- No missing/null values in any column.
- No duplicate `product_id` values.
- `return_reason` is populated even for non-returned items — for those rows it defaults to "Changed Mind" rather than being blank, so filter on `is_returned = Yes` before analyzing actual return reasons.

---

## Sheet3 — Return Reason Summary

A pre-aggregated count of return reasons (likely a pivot table output).

| return_reason | Count of each |
|---|---|
| Changed Mind | 1,924 |
| Color Mismatch | 46 |
| Size Issue | 60 |
| Damaged | 44 |
| Quality Issue | 55 |
| Wrong Item | 47 |

Note: these counts sum to 2,176 (the full row count of Sheet2), confirming this summary counts `return_reason` across **all** rows — not just the 320 actually-returned items — consistent with the data-quality note above.

---

## Sheet1
Empty — no data or headers present.

## Suggested Uses
- Sales/markdown analysis by category, brand, or season
- Return-rate analysis (320 of 2,176 items returned ≈ 14.7%)
- Price elasticity / markdown impact on customer rating
- Stock-level monitoring by category or brand
