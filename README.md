# week-1-questioHow many users do we have?

On average, how many orders do we receive per hour?

SELECT ROUND(SUM(total_orders) / 24, 0) AS avg_hourly_orders FROM 
(
  SELECT TO_CHAR(created_at, 'hh') AS hour_created,
  COUNT(order_id) AS total_orders
  FROM DEV_DB.DBT_PSBAUMANUCSCEDU.STG_ORDERS
  GROUP BY hour_created
  
  15 per hour

On average, how long does an order take from being placed to being delivered?

SELECT ROUND(AVG(DATEDIFF(days, created_at, delivered_at)),0) AS average_days_to_delivery
FROM DEV_DB.DBT_PSBAUMANUCSCEDU.STG_ORDERS
WHERE delivered_at IS NOT NULL;

4 d


How many users have only made one purchase? Two purchases? Three+ purchases?

SELECT COUNT(*) FROM (
    SELECT COUNT(order_id) AS nbr_orders, user_id
    FROM DEV_DB.DBT_PSBAUMANUCSCEDU.STG_ORDERS
    GROUP BY user_id
    HAVING nbr_orders = 1,2,3
)
25
28
71

On average, how many unique sessions do we have per hour?

SELECT ROUND(SUM(total_sessions) / 24, 0) AS avg_hourly_sessions FROM 
(
  SELECT TO_CHAR(created_at, 'hh') AS hour_created,
  COUNT(session_id) AS total_sessions
  FROM DEV_DB.DBT_PSBAUMANUCSCEDU.STG_EVENTS
  GROUP BY hour_created
) 
148
