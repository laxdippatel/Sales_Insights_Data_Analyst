# Sales_Insights_Data_Analyst
This is Project about Sales Product in Various Cities sells of Products with Year and Months with Data and more.

# Instructions for to setup mysql on your local computer.
SQL database dump is in db_dump.sql file above. Download db_dump.sql file to your local computer and import into your MySQL workbench.
Download MYSQL WorkBench : https://dev.mysql.com/downloads/workbench/

# Data Analysis Using SQL
**1.** Show all customer records

  `SELECT * FROM customers;`

**2.** Show total number of customers

`SELECT count(*) FROM customers;`

**3.**  Show transactions for Chennai market market code for chennai is Mark001

   `SELECT * FROM transactions where market_code='Mark001';`

**4.** Show distrinct product codes that were sold in chennai

 `SELECT distinct product_code FROM transactions where market_code='Mark001;`

**5.** Show transactions where currency is US dollars

`SELECT * from transactions where currency="USD"`

**6.** Show transactions in 2020 join by date table

`SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

**7.** Show total revenue in year 2020,

`SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`

**8.** Show total revenue in year 2020, January Month.

`SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

**9.** Show total revenue in year 2020 in Chennai

`SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.market_code="Mark001";`

**10.** You have to find of Inner join with date year = 2020;

`SELECT sales.transactions.*, sales.date.* from sales.transactions INNER JOIN sales.date ON sales.transactions.order_date = sales.date.date where sales.date.year=2020;`

**11.** Find the Revenue of 2020.

`SELECT SUM(sales.transactions.sales_amount) from sales.transactions INNER JOIN sales.date ON sales.transactions.order_date = sales.date.date where sales.date.year=2020;`

**12.** Show the with date of Sales revenue in chennai.

`SELECT SUM(sales.transactions.sales_amount) from sales.transactions INNER JOIN sales.date ON sales.transactions.order_date = sales.date.date
 where sales.date.year=2020 and sales.transactions.market_code="Mark001"`

 **13.** Distinct query for sell Product in Chennai.

`SELECT distinct product_code from sales.transactions where market_code="Mark001";`


**Star Schema :**
 - A star schema is a data model that organizes data in a database in a way that makes it easier to analyze and understand. It's a popular architecture for data warehousing and is characterized by a central fact table surrounded by dimension tables. 

![image](https://github.com/user-attachments/assets/2831e439-1f9c-4935-8a79-99951837e4c6)

**Data Analysis Using Power BI Formula to create norm_amount column**
-----------------------------------------------------------------------

`= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)`


**Sales market Table :**
Make a filter for blank zones removed .

`= Table.SelectRows(sales_markets, each ([zone] <> ""))`

![image](https://github.com/user-attachments/assets/bc6a0025-26de-40c8-b55a-54f7079b27ba)

**Sales _transactions table :**
Where -1 value find out .

`SELECT * FROM sales.transactions where sales_amount = -1;`

![image](https://github.com/user-attachments/assets/a8312dd8-4e7d-447c-b2df-d7b6e482c436)


`SELECT * FROM sales.transactions where sales_amount <= 0;`

**Or using <=0 then find values less than 0 so it’s garbage value.**

![image](https://github.com/user-attachments/assets/a99a831f-6d34-4dee-8c1e-661b778a7635)


**In PowerBi :**


![image](https://github.com/user-attachments/assets/04bc11f6-e468-4055-abcf-e2a03f4ef909)

Using filter deselect 0 and -1 values you can get the filtered data from sales transactions.

→ Using conditional column , select currency and add value USD and Output value 1 so it will change the where USD  = 1 and else Null.
But you can change the formula and make it 0 instead of Null.


![image](https://github.com/user-attachments/assets/ad203447-1bb7-40bb-a0cd-cab959d1a4cd)


→ Using formula :

` = Table.AddColumn(#"Filtered Rows", "norm_sales_amount", each if [currency] = "USD" then [sales_amount]*84  else [sales_amount])`

Norms_sales_amount convert USD to INR and also sales_amount will as similar show.

![image](https://github.com/user-attachments/assets/8b11e3b5-a501-4890-a161-0db380970df5)

**→ In between found the duplicates records like INR\r and USD\r :**

`select count(*) from transactions where transactions.currency='INR\r';`

`select count(*) from transactions where transactions.currency='INR';`

`select * from transactions where transactions.currency='USD\r' or transactions.currency='USD';`

Their is 4 records found and fix it.

![image](https://github.com/user-attachments/assets/15805ff4-608d-440d-928e-82ab2f67bf39)


**Make a dashboard of Sales Insights :**
 - Revenue generated in Market
 - Sales by Market
 - Top 5 Customers in Market
 - Top 5 Products in Market

Revenue and Date between generates market show on Dashboard.


![image](https://github.com/user-attachments/assets/d53cd46a-72bc-4756-876a-b95e3a8a02ea)


**Mobile View of PowerBI Dashboard:** 


![image](https://github.com/user-attachments/assets/6fb61435-1203-443a-988a-07bd5c5677c8)




----------------------------------------------------------------------
`In that Sales Insights Project I have generate the Piecharts , Stakedbar Chart , LineChart , Slicer Using make a Report of Revenue Generate , Sales of Product ,Top 5 Customers and Top 5 Product Sell in Market show in Report by Date,Month and Year.`
-----------------------------------------------------------------------












