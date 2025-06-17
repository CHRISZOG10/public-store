# Project Public Store
✌🏻💯

This project simulates a real-word sales analysis for **Public**, a major Greek retail chain, using real-word data from the [Online Retail II dataset](https://www.kaggle.com/datasets). The goal is to demonstrate end-to-end data analytics skills using **Python (via PyCharm)** for data preperation and **Power BI** for business-oriented visual insights.  

---

## 📑 Table of Contents

- [Project Overview](#project-overview)
- [Tech Stack](#tech-stack)
- [Data Preparation](#data-preparation)
  - [Data Source](#data-source)
- [SQL Data Cleaning Process](#data-cleaning)
- [Sales Dashboard](#sales-dashboard)
- [Customer Dashboard](#customer-dashboard)
- [Interactivity & Filters](#interactivity--filters)
- [Screenshots](#screenshots)
- [Recommendations](#Recommendations)
- [How to Use](#how-to-use)
- [Project Outcome](#project-outcome)
- [Author](#author)

---

## 🔍 Project Overview

**Objective:**  
Simulate a real-world retail analytics scenario using historical sales data that reflects actual transactions from Public, and deliver a business-ready dashboard focused on deriving actionable insights that support product performance monitoring and customer segmentation. This includes:

- 📊 Understand and clean the sales data
- 💰 Identify key trends in product performance and customer behavior
- 🛒 Segment the customer base using RFM analysis  
- 🧑‍🤝‍🧑 Design a compelling Power BI dashboard to communicate business insights
- 📍 Customer ID & Country Filters  

---

## 🛠 Tech Stack
 
- **Python (via PyCharm)** – Data cleaning & analyze the trends  
- **Power BI** – Interactive visual dashboards  
- **GitHub** – Version control & collaboration  

---

## 🧹 Data Preparation

### 📁 Data Source
[View the data UCI Online Retail II Data Set](https://www.kaggle.com/datasets/jillwang87/online-retail-ii)

---

## SQL Data Cleaning Process

> **Cleaned and structured using Python in PyCharm.**  
> ✅ Data import and explore the data with pandas library

```python
# DATA IMPORT FROM CSV 
df = pd.read_csv(r"C:\Users\chris\OneDrive\Desktop\ΧΡΗΣΤΟΣ\PUBLIC PROJECT\data.csv\.vscode\DataCleaningPython\data.csv",encoding='windows-1252')
print(df)
#FIRST 5 ROWS
print(f'{df.head()}\n')
#SHAPE
print(f'{df.shape}\n')
#COLUMN TYPES
print(f'{df.info()}\n')
#COLUMN NAMES
print(f'{df.columns}\n') 
#STATISTICAL INFO
print(f'{df.describe()}\n')
```

> ✅ Drop na's and modify the incoicedate column type

```python
#DATA CLEANING
##HOW MANY NULLS IN COLUMNS AND DROP THEM
df.isna().sum()
df[['Description', 'CustomerID']]
df.dropna(subset=['Description'], inplace=True)
df.dropna(subset=['CustomerID'], inplace=True)

##MODIFY COLUMN INVOICEDATE DATA TYPE
df['InvoiceDate'].info()
df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'])
```

> ✅ Create two tables for earnings and returns and create a column TotalPrice for all the tables

```python
##CREATE 2 TABLES ONE FOR EARNINGS AND ONE FOR RETURNS
df_earnings = df[df['Quantity'] > 0]
df_returns = df[df['Quantity'] < 0]
df_earnings.head()
df_returns.head()

##CREATE NEW COLUMN TOTAL PRICE FOR BOTH TABLES
df_earnings['TotalPrice'] = df_earnings['Quantity'] * df_earnings['UnitPrice']
df_returns['TotalPrice'] = df_returns['Quantity'] * df_returns['UnitPrice']
df['TotalPrice'] = df['Quantity'] * df['UnitPrice']
df_earnings.head()
df_returns.head()
df.head()
```

> ✅ Normalize the data

```python
##NORMALIZE THE DATA IN COLUMNS 
df['Description'].apply(lambda x: re.sub(r'[!@#$%^&.,]', '', str(x)))
df['Description']
df_earnings['Description'].apply(lambda x: re.sub(r'[!@#$%^&.,]', '', str(x)))
df_earnings['Description']
df_returns['Description'].apply(lambda x: re.sub(r'[!@#$%^&.,]', '', str(x)))
df_returns['Description']
```

> ✅ Drop duplicates

```python
df.duplicated().value_counts()

##Remove Duplicates
df.drop_duplicates(subset=['InvoiceNo', 'StockCode', 'Description', 'Quantity', 'InvoiceDate','UnitPrice', 'CustomerID', 'Country'], inplace=True, ignore_index=True)
df_earnings.drop_duplicates(subset=['InvoiceNo', 'StockCode', 'Description', 'Quantity', 'InvoiceDate','UnitPrice', 'CustomerID', 'Country'], inplace=True, ignore_index=True)
df_returns.drop_duplicates(subset=['InvoiceNo', 'StockCode', 'Description', 'Quantity', 'InvoiceDate','UnitPrice', 'CustomerID', 'Country'], inplace=True, ignore_index=True)
df.info()
df_earnings.info()
df_returns.info()
```

> ✅ Export the data

```python
#EXPORT THE DATA 
df.to_csv('PublicProjectCleaned.csv')
df_earnings.to_csv('PublicProjectSales.csv')
df_returns.to_csv('PublicProjectReturns.csv')
```

---

## 📈 Sales Dashboard

The **Sales Dashboard** offers a deep dive into business performance across time, products, and regions.

### Key Features

- 📅 **KPI Overview:** Total Sales, Profit, Quantity (Current & Previous Year)  
- 📉 **Sales Trends:** Monthly comparison with highlights of best/worst months  
- 🧾 **Category Comparison:** Sales vs. Profit per Category  
- 📆 **Weekly Trends:** Weekly analysis with average line & variance indicators  

[View the USA SALES DASHBOARD](https://public.tableau.com/app/profile/chris.zogas/viz/USSTORESDASHBOARD/USASALESDASHBOARD)

---

## 👥 Customer Dashboard

Designed for marketing and strategy teams, this dashboard uncovers customer behavior patterns.

### Key Features

- 🔢 **KPI Overview:** Customers, Orders, Sales per Customer  
- 📆 **Customer Trends:** Monthly KPI breakdown  
- 📊 **Order Distribution:** Loyalty & engagement insights  
- 🥇 **Top 10 Customers by Profit:** Ranked by profit, with details  

[View the USA CUSTOMERS DASHBOARD](https://public.tableau.com/app/profile/chris.zogas/viz/USSTORESCUSTOMERSDASHBOARD/USACUSTOMERSDASHBOARD?publish=yes)

---

## 🧭 Interactivity & Filters

- 📌 **Dynamic Year Selector**
- 🔝 **Top Customers Selector** 
- 📍 **Filters by Region, State**  
- 🛍️ **Filters by Category, Payment Method**  
- 📈 **Clickable Visuals** – Drill into segments directly from charts  

---

## 🖼️ Screenshots

| Mockup Dashboard | Sales Dashboard | Customer Dashboard |
|------------------|-----------------|--------------------|
| ![Mockup](assets/images/USA-STORES-MOCKUP.png)| ![Sales](assets/images/USA-STORES-SALES.png) | ![Customer](assets/images/USA-STORES-CUSTOMERS.png) |

---

## 💭 Recommendations

Based on the insights derived from the dashboards, the following recommendations are suggested to enhance business performance:

1. Peak sales Month
   According to the tableau sales dashboard the month with the highest sales is January for the most years.
   So this indicates a strong trend and the companies should increase the inventory and launching promotions.

2. Investigate under performing Time periods
   The lowest sales performance occured in August in most years and February.
   Maybe this months is the months that the discounts is over and the people don't buy many products.
   It's reccomending that the companies may have a new marketing proposal for these months.

3. High/Low Profit Category
   The categories with thw highest profits over the years are the food and computer and electrics.
   This means that the USA companies should look to increase the items of those categories and start to sell more and more.
   The categories with the lowest profits over the years are the butchers and the patisseries.
   The USA companies have two options, the first is to discard this categories from the supermarkets and the other is to create a stratigic campaign for that category items to increase the customers

4. Improve Weekly Sales Consistency
   Weekly trend analysis shows major fluctuations, with 23 weeks being below average in 2024.
   Investigating these dips can help stabilize cash flow and avoid missed sales opportunities.

5. Reward and Retain Top Customers
   The top 5 customers contributed to almost 3M of total profits. Retaining these VIP clients through exclusive perks or dedicated account management could further boost lifetime value.
   ![Top 5 Customers](assets/images/Top-5-Customers.png)
  
---

## 🚀 How to Use

1. Clone the repo  
   ```bash
   git clone https://github.com/CHRISZOG10/public-store.git
   ```
2. Open the Tableau Workbook: `assets/USA Stores Dashboards/US STORES DASHBOARD.twbx`  
3. Explore both dashboards and try the interactivity features

---

## ✅ Project Outcome

This project demonstrates real-world skills in:

- End-to-end data pipeline creation  
- Cleaning and preparing large retail datasets  
- Advanced dashboard design in Tableau  
- Delivering business insights through KPIs & trends  
- Building interactive, user-driven visual experiences  

---



## 👨‍💻 Author

**Your Name**  
📧 [christoszogas97@gmail.com](mailto:christoszogas97@gmail.com)  
🔗 [LinkedIn](https://linkedin.com/in/christos-zogas-804323320)  
