# Customer & Sales Analysis - Online Retail

Exploratory analysis of a real transactional dataset from a UK-based online retailer. The project covers revenue calculation, identification of top-performing products and countries, outlier detection, and customer segmentation using RFM analysis (Recency, Frequency, Monetary).

## Project context

An e-commerce company wants to better understand its customers and its sales in order to identify its most valuable customers, its best-performing products, and areas where it could improve commercially.

This project tries to answer the following questions:

1. How much does the company sell overall?
2. How do sales evolve over time?
3. Which products generate the most revenue?
4. Which countries matter the most?
5. Which customers spend the most?
6. Are there any abnormal behaviors (outliers)?
7. Which customers are loyal?
8. Which customers seem inactive?
9. Can we segment customers into meaningful groups?

## Dataset

Online Retail, from the UCI Machine Learning Repository: https://archive.ics.uci.edu/dataset/352/online+retail
This is a real transactional dataset from a UK-based online retailer, with 541,909 transactions recorded between December 2010 and December 2011. It includes order numbers, product codes and descriptions, quantities, unit prices, invoice dates, customer IDs and countries. It's distributed under a CC BY 4.0 license, so it's free to use as long as it's properly credited.

The file itself (Online Retail.xlsx) isn't included in this repo since it's too large. You'll need to download it from the link above and drop it in a `data/` folder before running the notebook.

## What the notebook does

The analysis follows a fairly standard pipeline:
First, I explore the raw data to check its shape, types, missing values and duplicates. Then comes the cleaning step: dropping duplicate rows, removing entries without a CustomerID, and converting the invoice date to a proper datetime format.

After that I deal with the transactions themselves, filtering out cancelled orders (invoices starting with "C") and removing rows with negative or zero quantity/price, which don't represent real sales.

Once the data is clean, I compute the revenue for each transaction (Quantity times UnitPrice) and build a few date-based columns (year, month) to make time-based grouping easier.

From there the analysis moves into the actual business questions: total revenue, monthly revenue trend, top 10 products by revenue, top 10 countries by revenue, revenue and order count per customer, and average order value. I also look for outliers in transaction revenue using the IQR method, and plot the distribution of order amounts to get a feel for how spread out purchases are.

The last part is the RFM segmentation: for each customer I compute how recently they bought something, how often they buy, and how much they've spent in total, then score each of those three dimensions on a 1-5 scale to build an RFM profile per customer. I also plot the relationship between purchase frequency and spending, and the distribution of recency across customers

## Tools

Python 3, with pandas and numpy for data manipulation, matplotlib and seaborn for visualization, and openpyxl to read the Excel file.

## Running it

Clone the repo, install the dependencies with pip install pandas numpy matplotlib seaborn openpyxl, make sure the dataset is in data/Online Retail.xlsx, then open customer_analysis.ipynb with Jupyter and run it top to bottom.

## Key takeaways

The notebook ends up giving a full picture of the business: total revenue and how it trends month over month, which products and countries drive the most sales, who the top customers are, what the average basket size looks like, how many outlier transactions exist, and a segmentation that separates loyal high-value customers from occasional buyers and inactive ones.

## Possible next steps

There's room to go further with this, for example by turning the RFM scores into actual customer segments (champions, at-risk, lost, etc.) based on business rules, trying a K-Means clustering on top of the RFM scores instead of manual thresholds, digging into seasonality at a finer level like day of week or time of day, or building an interactive dashboard on top of this with something like Streamlit.

## License

This project is built on the Online Retail dataset, distributed under a CC BY 4.0 license by the UCI Machine Learning Repository.

## Auteur

Projet réalisé par ZIRMI Amira, de la préparation et du nettoyage des données jusqu'à l'analyse et la visualisation des résultats.
