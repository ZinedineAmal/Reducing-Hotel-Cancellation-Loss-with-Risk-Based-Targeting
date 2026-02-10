Reducing Hotel Cancellation Loss with Risk-Based Targeting

This project analyzes hotel booking data to understand cancellation behavior and proposes a model-based targeting strategy to reduce cancellation-related revenue loss. Using a tuned XGBoost model, we generate booking-level cancellation probabilities and simulate business impact by targeting only the highest-risk bookings.

Dataset
Source: Kaggle (Hotel Booking Dataset)
Size: 83,293 rows × 33 columns
Period: 2017–2019
Contents: booking status, lead time, stay duration, ADR, customer info, distribution channel, market segment, country, and hotel identifiers

Business Problem
Hotel cancellations create high uncertainty and significant revenue loss. Cancellation rates remain consistently high (≈36–39% annually) with seasonal peaks around April–June (~40–41%). The goal is to reduce cancellation loss by identifying high-risk bookings early and applying targeted mitigation policies.

Approach
1) Data Cleaning & Quality Checks
- Missing values handled:
children → 0
country → "Unknown"
agent, company → missing indicators (has_agent, has_company) + treated as categorical IDs
- Data type fixes:
reservation_status_date → datetime
agent, company → category
Removed anomaly rows:
dropped records where total_guests == 0
- Defined loss proxy:
booking_value_proxy = adr × total_nights
loss_proxy = booking_value_proxy if canceled else 0

2) Exploratory Data Analysis (EDA)
Key findings:
- Seasonality: highest cancellation pressure occurs around April–June
- Segment & channel concentration:
Online TA drives the largest loss due to high volume
Groups has the highest cancellation rate, but lower total loss due to smaller volume
- Country concentration:
Portugal (PRT) dominates both cancellation rate (56.56%) and revenue loss (~$5.99M)
- Lead time:
cancellation rate increases with lead time (up to ~68% for >365 days)
loss concentrates in 31–365 days, not the extreme >365 window

3) Modeling & Explainability

Compared multiple classifiers; selected tuned XGBoost
Performance (test set):
- PR-AUC: 0.91
- ROC-AUC: 0.94

Explainability:
used SHAP to identify top drivers (lead time and seasonality-related features)

4) Risk-Based Targeting + Impact Simulation
Ranked bookings by predicted P(cancel) from tuned XGBoost
- Selected Top 20% highest-risk bookings
- captures ~52.77% of cancellations
- captures ~47.23% of total cancellation loss

Simulated policy effectiveness (loss reduction within the target group):
- 10% → 4.72% total loss saved (~$0.55M)
- 20% → 9.45% saved (~$1.10M)
- 30% → 14.17% saved (~$1.65M)
(Currency follows ADR unit; values are proxy.)

Results Snapshot
- Tuned XGBoost reliably separates cancellations and enables actionable prioritization
- Concentrating interventions on Top 20% risk bookings provides high impact with limited operational scopeReducing Hotel Cancellation Loss with Risk-Based Targeting
- This project analyzes hotel booking data to understand cancellation behavior and proposes a model-based targeting strategy to reduce cancellation-related revenue loss. Using a tuned XGBoost model, we generate booking-level cancellation probabilities and simulate business impact by targeting only the highest-risk bookings.

