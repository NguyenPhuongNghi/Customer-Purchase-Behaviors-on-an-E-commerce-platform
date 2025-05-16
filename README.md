# Customer Purchase Behaviors on Google Merchandise Store in 2017
**:pushpin: Link BigQuery: [link](https://console.cloud.google.com/bigquery?sq=42610209294:a6a3284128924aa7a42d825d87cbe07c)**
## 1. Project Overview
- This project aims to analyze customer purchase behaviors by querying large-scale e-commerce session data stored in Google BigQuery.
- The goal is to understand customer interactions, conversion funnel efficiency (from product view to add-to-cart to purchase), and provide actionable insights to optimize marketing and sales strategies.

## 2. Dataset Description
- Source: Public Google Analytics sample dataset (bigquery-public-data.google_analytics_sample.ga_sessions_2017*).
- Period Analyzed: 2017.
- Volume: Millions of session records including user behaviors, product views, cart additions, and transactions.
- Key Fields: date, fullVisitorId, hits.product.productRevenue, hits.eCommerceAction.action_type, trafficSource.source, device.deviceCategory.
  
## 3. Tools Used
- BigQuery: Data extraction and transformation with advanced SQL queries.
- Google Cloud Console: Query execution and data exploration.
## 4. Key Features
- Cohort Funnel Calculation: Tracked user behavior from product view ➔ add to cart ➔ completed purchase.

- Behavior Rate Calculation:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Add-to-Cart Rate = (Number of products added to cart) ÷ (Number of products viewed).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Purchase Rate = (Number of products purchased) ÷ (Number of products viewed).

- Session Behavior Analysis:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mapped how customers move through different e-commerce actions within a session.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identified stages with the highest drop-off rates.

## 5. Analysis
**:one: Calculate total visit, pageview, transaction for Jan, Feb and March 2017**
<br>**:rocket: Query:**
```sql
SELECT 
  FORMAT_DATE('%Y%m',PARSE_DATE('%Y%m%d',date)) as month,-- convert "date" field from string to date and format the date in "YYYY-MM"
  SUM(totals.visits) as visits,
  SUM(totals.pageviews) as pageviews,
  SUM(totals.transactions) as transactions
FROM `bigquery-public-data.google_analytics_sample.ga_sessions_2017*`
WHERE _table_suffix between '0101'and '0331' -- extract data for Jan, Feb and March 2017
GROUP BY month
ORDER BY month;
```
**:round_pushpin: Result:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-05-16%20161357.png?raw=true)

**:two: Calculate bounce rate per traffic source in July 2017 (Bounce_rate = num_bounce/total_visit)**
<br>**:rocket: Query:**
```sql
SELECT  
  source,
  total_visits,
  total_no_of_bounces,
  round(cast(total_no_of_bounces as decimal)/total_visits*100,3) as bounce_rate
FROM(
  SELECT
    trafficSource.source as source,
    sum(totals.visits) as total_visits,
    sum(totals.bounces) as total_no_of_bounces
  FROM `bigquery-public-data.google_analytics_sample.ga_sessions_201707*` -- extract data  for July 2017
  GROUP BY source
  ORDER BY total_visits DESC);
```
**:round_pushpin: Result:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-05-16%20161442.png?raw=true)

**:three: Revenue by traffic source by week, by month in June 2017**
<br>**:rocket: Query:**
```sql
with 
month_data as(
  SELECT
    "Month" as time_type,
    format_date("%Y%m", parse_date("%Y%m%d", date)) as time,
    trafficSource.source AS source,
    SUM(p.productRevenue)/1000000 AS revenue
  FROM `bigquery-public-data.google_analytics_sample.ga_sessions_201706*`,
    unnest(hits) hits,
    unnest(product) p
  WHERE p.productRevenue is not null
  GROUP BY 1,2,3
  order by revenue DESC
),

week_data as(
  SELECT
    "Week" as time_type,
    format_date("%Y%W", parse_date("%Y%m%d", date)) as time,
    trafficSource.source AS source,
    SUM(p.productRevenue)/1000000 AS revenue
  FROM `bigquery-public-data.google_analytics_sample.ga_sessions_201706*`,
    unnest(hits) hits,
    unnest(product) p
  WHERE p.productRevenue is not null
  GROUP BY 1,2,3
  order by revenue DESC
)

select * from month_data
union all
select * from week_data
order by source,time_type,time;
```
**:round_pushpin: Result:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-05-16%20162255.png?raw=true)

**:four: Average number of pageviews by purchaser type (purchasers vs non-purchasers) in June, July 2017e**
<br>**:rocket: Query:**
```sql
SELECT
  month,
  total_pageviews_purchaser/purchaser as avg_pageviews_purchase,
  total_pageviews_non_purchaser/non_purchaser as avg_pageviews_non_purchase
FROM (
  SELECT 
    FORMAT_DATE('%Y%m',PARSE_DATE('%Y%m%d',date)) AS month,
    COUNT(DISTINCT CASE WHEN totals.transactions >=1 AND product.productRevenue IS NOT NULL THEN fullVisitorId END) AS purchaser,
    COUNT(DISTINCT CASE WHEN totals.transactions IS NULL and product.productRevenue IS NULL THEN fullVisitorId END) AS non_purchaser,
    SUM(CASE WHEN totals.transactions >=1 AND product.productRevenue IS NOT NULL THEN totals.pageviews END) AS total_pageviews_purchaser,
    SUM(CASE WHEN totals.transactions IS NULL AND product.productRevenue IS NULL THEN totals.pageviews END) AS total_pageviews_non_purchaser
  FROM `bigquery-public-data.google_analytics_sample.ga_sessions_2017*`,
  UNNEST (hits) hits,
  UNNEST (hits.product) product
  WHERE _table_suffix between '0601'and '0731' -- extract data for June, July 2017
  GROUP BY month
  ORDER BY month
)
```
**:round_pushpin: Result:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-05-16%20162419.png?raw=true)

**:five: Average number of transactions per user that made a purchase in July 2017**
<br>**:rocket: Query:**
```sql
select
    format_date("%Y%m",parse_date("%Y%m%d",date)) as month,
    sum(totals.transactions)/count(distinct fullvisitorid) as Avg_total_transactions_per_user
from `bigquery-public-data.google_analytics_sample.ga_sessions_201707*`
    ,unnest (hits) hits,
    unnest(product) product
where  totals.transactions>=1
and product.productRevenue is not null
group by month;
```
**:round_pushpin: Result:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-05-16%20162534.png?raw=true)

**:six: Average amount of money spent per session. Only include purchaser data in July 2017**
<br>**:rocket: Query:**
```sql
select
    format_date("%Y%m",parse_date("%Y%m%d",date)) as month,
    ((sum(product.productRevenue)/sum(totals.visits))/power(10,6)) as avg_revenue_by_user_per_visit
from `bigquery-public-data.google_analytics_sample.ga_sessions_201707*`
  ,unnest(hits) hits
  ,unnest(product) product
where product.productRevenue is not null
  and totals.transactions>=1
group by month;
```
**:round_pushpin: Result:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-05-16%20162619.png?raw=true)

**:seven: Other products purchased by customers who purchased product "YouTube Men's Vintage Henley" in July 2017.**
<br>**:rocket: Query:**
```sql
select
    product.v2productname as other_purchased_product,
    sum(product.productQuantity) as quantity
from `bigquery-public-data.google_analytics_sample.ga_sessions_201707*`,
    unnest(hits) as hits,
    unnest(hits.product) as product
where fullvisitorid in (select distinct fullvisitorid
                        from `bigquery-public-data.google_analytics_sample.ga_sessions_201707*`,
                        unnest(hits) as hits,
                        unnest(hits.product) as product
                        where product.v2productname = "YouTube Men's Vintage Henley"
                        and product.productRevenue is not null)
  and product.v2productname != "YouTube Men's Vintage Henley"
  and product.productRevenue is not null
group by other_purchased_product
order by quantity desc;
```
**:round_pushpin: Result:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-05-16%20162707.png?raw=true)

**:eight: Calculate cohort map from product view to addtocart to purchase in Jan, Feb and March 2017. Add_to_cart_rate = number product  add to cart/number product view. Purchase_rate = number product purchase/number product view.**
<br>**:rocket: Query:**
```sql
with product_data as(
select
    format_date('%Y%m', parse_date('%Y%m%d',date)) as month,
    count(CASE WHEN eCommerceAction.action_type = '2' THEN product.v2ProductName END) as num_product_view,
    count(CASE WHEN eCommerceAction.action_type = '3' THEN product.v2ProductName END) as num_add_to_cart,
    count(CASE WHEN eCommerceAction.action_type = '6' and product.productRevenue is not null THEN product.v2ProductName END) as num_purchase
FROM `bigquery-public-data.google_analytics_sample.ga_sessions_*`
,UNNEST(hits) as hits
,UNNEST (hits.product) as product
where _table_suffix between '20170101' and '20170331'
and eCommerceAction.action_type in ('2','3','6')
group by month
order by month
)

select
    *,
    round(num_add_to_cart/num_product_view * 100, 2) as add_to_cart_rate,
    round(num_purchase/num_product_view * 100, 2) as purchase_rate
from product_data;
```
**:round_pushpin: Result:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-05-16%20163340.png?raw=true)

## 6. Insights
**- Overall Conversion Funnel:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20155627.png?raw=true)

    + Only about 30%-40% of viewed products were added to cart.
    + About 8%-13% of viewed products were successfully purchased.
    + Major drop-off happens between viewing a product and adding it to the cart.

**- Device Differences:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20163922.png?raw=true)


    + Desktop users showed higher add-to-cart and purchase rates compared to mobile users.

**- Traffic Source Effect:**
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20163153.png?raw=true)


    + Organic Search and Direct traffic sources converted better than Paid Advertising.

## Conclusion:
**1. Enhance Product Page Experience**

- Make the Add to Cart button highly visible and accessible.

- Improve product images, add short videos, and strengthen product descriptions to build trust and interest.

- Highlight urgency using "Low Stock" or "Limited Time Offer" tags.

**2. Optimize Mobile Shopping Experience**

- Simplify mobile navigation with larger buttons and fewer checkout steps.

- Implement fast checkout options like one-click purchasing or wallet integrations (e.g., Apple Pay, Google Pay).

- Improve mobile site loading speed to reduce bounce rates.

**3. Focus on High-Converting Channels**

- Invest more in SEO and Direct marketing campaigns (e.g., loyalty programs, email marketing) where users show stronger purchase intent.

- Refine Paid Advertising targeting by focusing on high-quality audiences (e.g., retargeting past visitors, lookalike audiences).

**4. Recover Abandoned Carts**

- Set up abandoned cart email sequences offering incentives like discounts or free shipping.

- Use exit-intent popups reminding users of their cart when they try to leave the page.

**5. Personalized and Device-Specific Promotions**

- Create personalized offers based on user behavior (e.g., recently viewed items).

- Offer special promotions tailored for mobile users to improve mobile conversion rates (e.g., mobile-only discounts).










