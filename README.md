# Customer Purchase Behaviors on Google Merchandise Store in 2017
**:pushpin: Link BigQuery: https://console.cloud.google.com/bigquery?sq=42610209294:a6a3284128924aa7a42d825d87cbe07c**
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

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20105728.png?raw=true)

**:two: Calculate bounce rate per traffic source in July 2017 (Bounce_rate = num_bounce/total_visit)**

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20105917.png?raw=true)

**:three: Revenue by traffic source by week, by month in June 2017**

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20112312.png?raw=true)
![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20112338.png?raw=true)

**:four: Average number of pageviews by purchaser type (purchasers vs non-purchasers) in June, July 2017e**

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20113512.png?raw=true)

**:five: Average number of transactions per user that made a purchase in July 2017**

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20114530.png?raw=true)

**:six: Average amount of money spent per session. Only include purchaser data in July 2017**

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20113648.png?raw=true)

**:seven: Other products purchased by customers who purchased product "YouTube Men's Vintage Henley" in July 2017.**

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20113742.png?raw=true)

**:eight: Calculate cohort map from product view to addtocart to purchase in Jan, Feb and March 2017. Add_to_cart_rate = number product  add to cart/number product view. Purchase_rate = number product purchase/number product view.**

![alt](https://github.com/NguyenPhuongNghi/Customer-Purchase-Behaviors-on-an-E-commerce-platform/blob/main/images/Screenshot%202025-04-28%20114623.png?raw=true)

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










