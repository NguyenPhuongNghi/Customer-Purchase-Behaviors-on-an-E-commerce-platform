# Customer Purchase Behaviors on Google Merchandise Store in 2017

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
## 4. Key Features and Insights
Cohort Funnel Calculation: Tracked user behavior from product view ➔ add to cart ➔ completed purchase.

Behavior Rate Calculation:

Add-to-Cart Rate = (Number of products added to cart) ÷ (Number of products viewed).

Purchase Rate = (Number of products purchased) ÷ (Number of products viewed).

Session Behavior Analysis:

Mapped how customers move through different e-commerce actions within a session.

Identified stages with the highest drop-off rates.

## 5. Key Insights and Conclusion
Overall Conversion Funnel:

100% of sessions started with product views.

Only about 35%-40% of viewed products were added to cart.

About 8%-10% of viewed products were successfully purchased.

Drop-off Analysis:

Major drop-off happens between viewing a product and adding it to the cart.

Device Differences:

Desktop users showed higher add-to-cart and purchase rates compared to mobile users.

Traffic Source Effect:

Organic Search and Direct traffic sources converted better than Paid Advertising.

## Conclusion:

Optimization efforts should focus on improving the product detail pages and cart experience, especially for mobile users.

Special attention should be given to traffic from paid ads to enhance ROI.
