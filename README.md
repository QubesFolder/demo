# QubesFolder Demo Model: 1 Billion Rows Benchmark

This repository contains the declarative model definition [tutorial.qf](tutorial.qf) for the **QubesFolder** high-performance analytical core.

It is designed to demonstrate **sub-second latency** on complex financial aggregations over **1 billion rows** using commodity hardware (e.g., a standard laptop with 4 cores / 8GB RAM).

## 📊 Model Statistics

| Component | Count | Details |
| :--- | :--- | :--- |
| **Fact Table (Sales)** | 1,000,000,000 rows | Main transactional data |
| **Exchange Rates** | 722 rows | Multi-currency support |
| **Dimensions** | 7 | Deep hierarchies (Period, Product, Client, etc.) |
| **Measures** | 6 | Amount, Qty, Price, Tax, Payment, Debt |
| **Potential Cube Size** | ~2.28 × 10¹² cells | Full cardinality of the multidimensional space |

### Dimensional Structure
*   **Period:** 171 elements, depth 4 (All → Year → Quarter → Month)
*   **Product:** 55 elements, depth 3 (All → Category → SKU)
*   **Client:** 136 elements, depth 4 (All → Segment → Industry → Company)
*   **Contract:** 1,006 elements, depth 3 (All → Type → ID)
*   **Site:** 296 elements, depth 4 (All → Continent → Country → City)
*   **Currency:** 6 elements (USD, EUR, CNY, JPY, GBP, RUR)

## 📝 Model Syntax (`tutorial.qf`)

QubesFolder uses a concise, declarative syntax to define multidimensional models. The engine translates these definitions into SQL queries for ClickHouse.

**Key Concepts:**
*   `DEFINE DIMENSION`: Analytical axes with hierarchical trees.
*   `DEFINE CUBE`: Logical sets of measures qualified by dimensions.
*   `DEFINE VIEW`: Predefined presentation layouts (Rows/Columns).

*(See `tutorial.qf` for full source code)*

## 🏗 Architecture Notes

*   **Computation Pushdown:** All heavy aggregations are executed directly in ClickHouse.
*   **On-Demand Aggregation:** Only the required slice of the 2.28 trillion-cell space is calculated.
*   **System-Level Transactional Guarantees:** Logical transactions ensure that all user changes are Atomic, Isolated, and Consistent, regardless of the underlying ClickHouse cluster topology (including sharded configurations).

## 📄 License

This demo model is provided for benchmarking and evaluation purposes under the **Creative Commons Attribution-NonCommercial 4.0 International Public License**.

© QubesFolder. All rights reserved.
