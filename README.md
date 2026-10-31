# Marketing-campaign-cleaning-and-structure-
A response model can provide a significant boost to the efficiency of a marketing campaign by increasing responses or reducing expenses. The objective is to predict who will respond to an offer for a product or service
Objective

Turn the raw marketing dataset into a reliable, analysis-ready table: no duplicates, correct data types, no impossible values and consistent text categories.

### Input and output
Input :	data/marketing_campaign.csv	Raw dataset, ~ 2240 customers
Output :	data/marketing_campaign_clean.csv	Cleaned dataset used by notebooks 02 to 04 and the dashboard
Dataset variables

### Group	Variables
Campaigns	AcceptedCmp1-AcceptedCmp5, Response (target: last campaign)
Customer	DtCustomer, Education, Marital, Kidhome, Teenhome, Income, Complain
Spending (2 years)	MntWines, MntFruits, MntMeatProducts, MntFishProducts, MntSweetProducts, MntGoldProds
Purchases	NumDealsPurchases, NumWebPurchases, NumCatalogPurchases, NumStorePurchases, NumWebVisitsMonth
Activity	Recency (days since last purchase)

### Cleaning steps and decisions

Step	What was done	Why	Rows / values affected
Exact duplicates	df.duplicated() then drop_duplicates()	Duplicates inflate counts and totals
Data types	DtCustomer converted to datetime, Income and spending to numeric, binary columns to integers	Enables date and numeric operations dates not converted
Negative values	Set to missing (NaN) instead of dropping the row	No returns logic in this dataset, a negative spend or count is invalid	
Invalid binaries	Values outside {0, 1} set to NaN	Binary flags must be 0 or 1	
Income	Values <= 0 set to NaN; extreme incomes flagged in Income_outlier, not removed	Keep information, let the analyst decide flagged
Future dates	Enrolment dates after today set to missing	Impossible values	
Target	Rows without Response dropped	Unusable for campaign analysis	
Text columns	Trimmed, title-cased, then grouped: 2n Cycle -> Master; Alone -> Single; Absurd, YOLO -> Other	One label per real category	see before/after below
### Before / after
Before  	After
Rows 2240   2240
Missing Income	24
Education categories	2240   2240
Marital categories	2240 2240
