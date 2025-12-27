\# About the data   
   
This project uses the Beverage Sales dataset from Kaggle.   
The dataset is a simulated wholesale beverage sales dataset designed to resemble realistic patterns in a beverage distribution business. The original file contains information about customers, products, dates, orders, quantities, prices, and discounts.

Original data source (Kaggle):    
[https://www.kaggle.com/datasets/sebastianwillmann/beverage-sales](https://www.kaggle.com/datasets/sebastianwillmann/beverage-sales)  
Thanks to author Sebastian Willmann, who provided the dataset via Kaggle.

For this course project, we transformed the original file, which contained data from January 2021- December 2023 into a small analytical dataset focusing on the year 2023\.

Number of records (2021-2023): 8,999,911 (includes header row)  
Number of records (2023): 2,994,658 (includes header row)

Additional files include the original data in csv format and an illustration of the star schema.  
from IPython.display import Image  
Image(url="https://github.com/96195hsu-create/data\_final\_project/blob/main/Star%20Schema.jpg?raw=true”)

The central fact table records each sales line, and three dimension tables, customer, product, and date.

Tools used:  
csvkit/xsv: used for data wrangling and data validation  
Duckdb: used for sql queries and dimensional modeling  
Pandas and matplotlib: used for visualizations

Enclosed please find an .ipynb file containing data acquisition and wrangling, queries to interrogate business questions, and analysis of results. 

\# The Main Data Tables

\#\# star\_beverage (facts)

Each row in star\_beverage represents one order line: a quantity of a given product sold to a specific customer on a specific date.

Notes:  
\* quantity – number of units sold on this order line.  
\* unit\_price – price per unit at the time of the order.  
\* discount – discount applied to this line.  
\* total\_price – final extended price for the line after discount.  
\* order\_id – business identifier for the order; kept in the fact table as a degenerate dimension so we can group or filter by order.  
\* customer\_key – integer surrogate key referencing customer.customer\_key.  
\* product\_key – integer surrogate key referencing product.product\_key.  
\* date\_key – integer surrogate key referencing date.date\_key.

\#\# customer

The customer dimension stores attributes that describe each customer in the dataset.

Notes:  
\* customer\_id – business identifier.  
\* type – customer type (for example, B2B, B2C).  
\* region – geographic region associated with the customer.  
\* customer\_key – integer surrogate primary key used in joins from star\_beverage.

\#\# product

The product dimension stores attributes of the beverage products.

Notes:  
\* product – product name.  
\* category – beverage category (for example, soft drinks, water, juices, and alcoholic beverages).  
\* product\_key – integer surrogate primary key used in joins from star\_beverage.

\#\# date

The date dimension is a standard calendar table built from the order dates in the source data.

Notes:  
\* order\_date – full calendar date of the order.  
\* day  – day of month as an integer (1–31).  
\* month – month number (1–12).  
\* year – four-digit year.  
\* weekday – name or number of the weekday.  
\* weekend – flag indicating whether the date falls on a weekend.  
\* date\_key – integer surrogate primary key used in joins from star\_beverage.

\#\# conventions

For consistency, we decided to normalize some of the output across queries.  
Any output results related to quantity were cast as integers.  
Any output results related to prices were rounded to the hundredths place, or two digits following the decimal. All monetary values are assumed to be in Euros for the analysis.  
Any output in a visual table included “.df()” to store it as a DataFrame and to make the visualizations.

## \#\#\# Business Questions:

* ## Q1) How does the popularity of each category change by month? Are there clear seasonal peaks?

* ## Q2) Which of the categories are most popular, and are any of those being discounted?

* ## Q3) Which product is the top seller by quantity in each region?

* ## Q4) Among B2B sales, are larger orders from repeat customers? What about BTC sales?

Each question is accompanied by the result, a visualization and the finding.

