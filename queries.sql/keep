* ------------------------------------------------------------------
   Bitcoin Performance & Volatility Analysis (2010–2024)
   Author: Michael Aaron
   Database: PostgreSQL
   Table: bitcoin_daily
   Columns:
       start_date    date
       end_date      date
       open_price    numeric
       high_price    numeric
       low_price     numeric
       close_price   numeric
       volume        numeric
       market_cap    numeric

   Purpose:
   - Analyze Bitcoin’s behavior as a financial asset
   - Measure daily and monthly intraday returns (open → close)
   - Identify best/worst days and months
   - Compare extreme daily volatility with more modest long-term averages
   ------------------------------------------------------------------ */


-- ==================================================================
-- 0. Quick data preview
-- ==================================================================
-- Purpose:
--   Verify that the data loaded correctly and the structure matches
--   the expected columns.
-- ------------------------------------------------------------------

SELECT
    start_date,
    end_date,
    open_price,
    high_price,
    low_price,
    close_price,
    volume,
    market_cap
FROM bitcoin_daily
ORDER BY start_date
LIMIT 10;



-- ==================================================================
-- 1. Calculate daily intraday return (open → close)
-- ==================================================================
-- Definition:
--   daily_return_pct = ((close_price - open_price) / open_price) * 100
--
-- Purpose:
--   Create a reusable expression to understand day-to-day price moves.
--   This SELECT is also useful for checking early data behavior
--   (e.g., periods where open_price = close_price → 0% intraday return).
-- ------------------------------------------------------------------

SELECT
    start_date,
    open_price,
    close_price,
    ROUND(((close_price - open_price) / open_price) * 100, 2) AS daily_return_pct
FROM bitcoin_daily
ORDER BY start_date
LIMIT 20;



-- ==================================================================
-- 2. Best days: highest intraday gains
-- ==================================================================
-- Purpose:
--   Identify the trongest trading days in Bitcoin history
--   in terms of percentage gain from open_price to close_price.
-- ------------------------------------------------------------------

SELECT
    start_date,
    open_price,
    close_price,
    ROUND(((close_price - open_price) / open_price) * 100, 2) AS daily_return_pct
FROM bitcoin_daily
ORDER BY daily_return_pct DESC
LIMIT 10;



-- ==================================================================
-- 3. Worst days: largest intraday losses
-- ==================================================================
-- Purpose:
--   Identify the worst trading days in Bitcoin history
--   in terms of percentage drop from open_price to close_price.
-- ------------------------------------------------------------------

SELECT
    start_date,
    open_price,
    close_price,
    ROUND(((close_price - open_price) / open_price) * 100, 2) AS daily_return_pct
FROM bitcoin_daily
ORDER BY daily_return_pct ASC
LIMIT 10;



-- ==================================================================
-- 4. Monthly average intraday return and volatility
-- ==================================================================
-- Definitions:
--   daily_return_pct = ((close_price - open_price) / open_price) * 100
--   avg_monthly_return_pct = average of daily_return_pct within a month
--   volatility_pct = standard deviation of daily_return_pct within a month
--
-- Notes:
--   - In early years (around 2010–2012), many days have open_price = close_price.
--     That means daily_return_pct = 0 for those days, leading to:
--       * avg_monthly_return_pct = 0
--       * volatility_pct = 0
--     This reflects limited intraday variation in early data, not an error.
-- ------------------------------------------------------------------

SELECT
    DATE_TRUNC('month', start_date) AS month,
    ROUND(AVG(((close_price - open_price) / open_price) * 100), 2) AS avg_monthly_return_pct,
    ROUND(STDDEV(((close_price - open_price) / open_price) * 100), 2) AS volatility_pct
FROM bitcoin_daily
GROUP BY month
ORDER BY month;



-- ==================================================================
-- 5. Best months: highest average intraday return
-- ==================================================================
-- Purpose:
--   Find the calendar month with the highest average daily intraday
--   return (open → close).
-- ------------------------------------------------------------------

SELECT
    month,
    avg_monthly_return_pct
FROM (
    SELECT
        DATE_TRUNC('month', start_date) AS month,
        ROUND(AVG(((close_price - open_price) / open_price) * 100), 2) AS avg_monthly_return_pct
    FROM bitcoin_daily
    GROUP BY month
) m
ORDER BY avg_monthly_return_pct DESC
LIMIT 10;



-- ==================================================================
-- 6. Worst months: lowest average intraday return
-- ==================================================================
-- Purpose:
--   Find the calendar month with the lowest (most negative) average
--   daily intraday return.
-- ------------------------------------------------------------------

SELECT
    month,
    avg_monthly_return_pct
FROM (
    SELECT
        DATE_TRUNC('month', start_date) AS month,
        ROUND(AVG(((close_price - open_price) / open_price) * 100), 2) AS avg_monthly_return_pct
    FROM bitcoin_daily
    GROUP BY month
) m
ORDER BY avg_monthly_return_pct ASC
LIMIT 10;



-- ==================================================================
-- 7. Monthly summary table (for export or reporting)
-- ==================================================================
-- Purpose:
--   Produce a full monthly summary of:
--     - average intraday return
--     - intraday volatility
--   This can be exported to CSV for visualization (e.g., Excel or Tableau)
--   or used directly in dashboards.
-- ------------------------------------------------------------------

SELECT
    DATE_TRUNC('month', start_date) AS month,
    ROUND(AVG(((close_price - open_price) / open_price) * 100), 2) AS avg_monthly_return_pct,
    ROUND(STDDEV(((close_price - open_price) / open_price) * 100), 2) AS volatility_pct
FROM bitcoin_daily
GROUP BY month
ORDER BY month;

/* ------------------------------------------------------------------
   End of script

   Suggested usage:
   - Run sections 0–1 to understand the data.
   - Run sections 2–3 to identify best/worst days.
   - Run sections 4–6 to analyze monthly behavior and extremes.
   - Use section 7 as a basis for visualization or extended reporting.

   This script is meant to accompany:
   - README.md  (project overview)
   - findings.md (written interpretation and context)
   ------------------------------------------------------------------ */
