# Bitcoin-Performance-Volatility-Analysis-2010-2024
This portfolio project analyzes daily Bitcoin price data from July 27, 2010 to May 22, 2024 using PostgreSQL.  
The goal is to understand how Bitcoin behaves as a financial asset over time by examining:

- Its best and worst single days across the past 14 years
- Its best and worst months across the past 14 years
- How extreme daily volatility compares with more modest **longer-term averages

Instead of focusing on hype, this project takes a practical, data-driven view of Bitcoin as a volatile asset whose behavior becomes more stable when analyzed over longer time horizons.

---

## Dataset

Source: Bitcoin daily historical data from Kaggle  
Rows: 5,059 days of trading activity  
Fields:

- `start_date` – start date of the daily record  
- `end_date` – end date of the daily record (typically same as start_date)  
- `open_price` – price at the start of the day  
- `high_price` – highest price during the day  
- `low_price` – lowest price during the day  
- `close_price` – price at the end of the day  
- `volume` – total trading volume that day  
- `market_cap` – total market value of Bitcoin that day  

Database:PostgreSQL  
Table name:`bitcoin_daily`

---

## Business Questions

This project focuses on simple, clear questions that a financial or analytics team might ask:

1. What was Bitcoin’s best and worst single trading day (based on percentage move from open to close)?
2. Which month had the strongest average intraday gain, and which had the weakest?
3. How does Bitcoin’s extreme daily volatility compare to its average monthly behavior?
4. What does this say about Bitcoin as a long-term asset versus a short-term trading instrument?

---

## Key Metrics & Definitions

- **Daily Return (%):**  
  \[
  \text{daily return} = \frac{\text{close\_price} - \text{open\_price}}{\text{open\_price}} \times 100
  \]
  Measures the intraday move from open to close.

- **Average Monthly Return (%):**  
  The average of daily returns within each calendar month.

- **Monthly Volatility (%):**  
  Standard deviation of daily returns within each month (used in the analysis, though not all numbers are shown here).

---

## Summary of Findings

### 1️⃣ Best & Worst Single Days (Intraday Return)

- **Best day:**  
  **2013-11-18 — +41.68%**  
  Bitcoin gained over 40% in a single trading day, during an early speculative surge period.

- **Worst day:**  
  **2020-03-12 — −40.44%**  
  This coincides with the global market panic at the onset of COVID-19, when many assets sold off sharply and simultaneously.

These results highlight Bitcoin’s extreme day-to-day price swings. Individual days can show dramatic gains or losses, especially during periods of macroeconomic stress or speculative booms.

---

### 2️⃣ Best & Worst Months (Average Intraday Return)

Using average daily intraday returns aggregated by month:

- **Best month:**  
  **2013-11 — +6.12% average intraday return**

- **Worst month:**  
  **2022-06 — −1.43% average intraday return**

Despite huge single-day moves, the *average intraday performance over an entire month* is surprisingly modest. This supports a more balanced view:

> Bitcoin is highly volatile at the daily level, but when returns are averaged over longer periods, the net movement is much smaller.

---

### 3️⃣ Early Data Behavior (2010–2012)

From 2010 through roughly 2012, the OHLC values (open, high, low, close) in the dataset often show no intraday variation (open_price = close_price for many days).

As a result:

- Intraday return = 0% for those days  
- Average monthly return and measured volatility are **0** for some early months

This reflects:

- Limited liquidity and/or limited price reporting in the early Bitcoin market  
- Not a bug in the SQL logic  

For this reason, **volatility interpretations are more meaningful for later years**, when intraday variation is consistently present.

---

## Skills Demonstrated

### SQL Concepts
- `SELECT`, `WHERE`, `ORDER BY`
- Calculated fields using arithmetic and percentages
- Aggregation with `AVG()` and `STDDEV()`
- Date handling with `DATE_TRUNC('month', ...)`
- Grouping with `GROUP BY` for monthly analysis

### Analytics & Finance Concepts
- Daily vs. monthly views of return
- Volatility and risk interpretation
- Linking data-driven findings to real-world events (speculative surge in 2013, COVID crash in 2020, crypto downturn in 2022)
- Balanced, non-hype communication of cryptocurrency behavior

