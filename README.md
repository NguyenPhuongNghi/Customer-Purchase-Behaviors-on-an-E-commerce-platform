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
## 4. Key Features
- Cohort Funnel Calculation: Tracked user behavior from product view ➔ add to cart ➔ completed purchase.

- Behavior Rate Calculation:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Add-to-Cart Rate = (Number of products added to cart) ÷ (Number of products viewed).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Purchase Rate = (Number of products purchased) ÷ (Number of products viewed).

- Session Behavior Analysis:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mapped how customers move through different e-commerce actions within a session.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identified stages with the highest drop-off rates.

## 5. Analysis
- Calculate total visit, pageview, transaction for Jan, Feb and March 2017

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20105728.png?raw=true)
- Calculate bounce rate per traffic source in July 2017 (Bounce_rate = num_bounce/total_visit)

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20105917.png?raw=true)
- Revenue by traffic source by week, by month in June 2017

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20112312.png?raw=true)
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20112338.png?raw=true)
- Average number of pageviews by purchaser type (purchasers vs non-purchasers) in June, July 2017e

![alt](
- Average number of transactions per user that made a purchase in July 2017
- Average amount of money spent per session. Only include purchaser data in July 2017
- Other products purchased by customers who purchased product "YouTube Men's Vintage Henley" in July 2017.
- Calculate cohort map from product view to addtocart to purchase in Jan, Feb and March 2017. Add_to_cart_rate = number product  add to cart/number product view. Purchase_rate = number product purchase/number product view.

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
