# \# PLSQL Assignment One - Sunrise Supermarket

# 

# \## Student Information

# 

# \*\*Name:\*\* NIYIMBONERA Mahoro Anselme  

# \*\*Student ID:\*\* 29558  

# \*\*DBMS Used:\*\* Oracle Database 21c Express Edition (XE)

# 

# \---

# 

# \# Business Scenario

# 

# Sunrise Supermarket sells a variety of products to customers. Customers place orders containing one or more items from different product categories. Management wants to better understand customer purchasing behavior, product demand, and sales trends over time.

# 

# This project uses SQL queries to analyze supermarket data through JOIN operations, Common Table Expressions (CTEs), and Window Functions.

# 

# \---

# 

# \# Database Structure

# 

# The database consists of the following four tables:

# 

# \## Customers

# 

# Stores customer information.

# 

# | Column | Description |

# |----------|-------------|

# | customer\_id | Unique customer ID |

# | customer\_name | Customer full name |

# | email | Customer email |

# | city | Customer city |

# 

# \## Products

# 

# Stores product information.

# 

# | Column | Description |

# |----------|-------------|

# | product\_id | Unique product ID |

# | product\_name | Product name |

# | category | Product category |

# | price | Product price |

# 

# \## Orders

# 

# Stores customer orders.

# 

# | Column | Description |

# |----------|-------------|

# | order\_id | Unique order ID |

# | customer\_id | Customer who placed the order |

# | order\_date | Date of order |

# 

# \## Order Items

# 

# Stores products purchased within each order.

# 

# | Column | Description |

# |----------|-------------|

# | order\_item\_id | Unique order item ID |

# | order\_id | Associated order |

# | product\_id | Purchased product |

# | quantity | Quantity purchased |

# 

# \---

# 

# \# Data Population

# 

# The database was populated with:

# 

# \- 6 Customers

# \- 10 Products

# \- 4 Product Categories

# \- 15 Orders

# \- 30 Order Items

# \- Multiple Order Dates

# 

# This satisfies the assignment requirements.

# 

# \---

# 

# \# How to Run the Project

# 

# 1\. Open Oracle SQL Developer.

# 2\. Connect to Oracle Database 21c XE.

# 3\. Open the SQL script file (`assignment\_1.sql`).

# 4\. Execute the table creation statements.

# 5\. Execute the INSERT statements.

# 6\. Run each query section individually.

# 7\. Review the results and screenshots.

# 

# \---

# 

# \# JOIN Queries

# 

# \## JOIN Query 1: Orders and Customers

# 

# \### Objective

# 

# List every order together with the customer's name, city, and order date.

# 

# \### Explanation

# 

# An INNER JOIN is used between the `orders` and `customers` tables through the `customer\_id` field. Only records that exist in both tables are returned.

# 

# \### Screenshot

# 

# !\[JOIN Query 1](screenshots/join\_query\_1\_orders\_customers.png)

# 

# \### Business Interpretation

# 

# This query helps management identify who placed each order and where customers are located.

# 

# \---

# 

# \## JOIN Query 2: Order Items and Products

# 

# \### Objective

# 

# Display every order item together with product details.

# 

# \### Explanation

# 

# An INNER JOIN is performed between `order\_items` and `products` using `product\_id`.

# 

# The query displays:

# 

# \- Product Name

# \- Category

# \- Price

# \- Quantity Purchased

# 

# \### Screenshot

# 

# !\[JOIN Query 2](screenshots/join\_query\_2\_orderitems\_products.png)

# 

# \### Business Interpretation

# 

# Management can see which products are being purchased and in what quantities.

# 

# \---

# 

# \## JOIN Query 3: Customers and Orders

# 

# \### Objective

# 

# List all customers and their orders, including customers without orders.

# 

# \### Explanation

# 

# A LEFT JOIN is used between `customers` and `orders`.

# 

# All customers are displayed even if they have never placed an order.

# 

# \### Screenshot

# 

# !\[JOIN Query 3](screenshots/join\_query\_3\_customers\_orders.png)

# 

# \### Business Interpretation

# 

# This helps identify active customers and customers who have not yet made purchases.

# 

# \---

# 

# \# Common Table Expression (CTE)

# 

# \## Customer Spending Above Average

# 

# \### Objective

# 

# Calculate total customer spending and identify customers whose spending exceeds the average spending.

# 

# \### Explanation

# 

# A CTE named `customer\_totals` calculates total spending per customer using:

# 

# ```sql

# SUM(quantity \* price)

# ```

# 

# The main query then compares each customer's spending against the overall average spending.

# 

# \### Screenshot

# 

# !\[CTE Query](screenshots/cte\_customer\_above\_average\_spend.png)

# 

# \### Business Interpretation

# 

# Management can identify high-value customers and target them with loyalty programs and promotions.

# 

# \---

# 

# \# Window Function Queries

# 

# \## Window Function 1: Customer Spending Rank

# 

# \### Objective

# 

# Rank customers according to total spending.

# 

# \### Explanation

# 

# The `RANK()` window function is used to rank customers from highest spender to lowest spender.

# 

# \### Screenshot

# 

# !\[Window Function 1](screenshots/window\_1\_customer\_rank.png)

# 

# \### Business Interpretation

# 

# This query helps identify the supermarket's most valuable customers.

# 

# \---

# 

# \## Window Function 2: Customer Order Numbering

# 

# \### Objective

# 

# Number each customer's orders according to the order in which they were placed.

# 

# \### Explanation

# 

# The `ROW\_NUMBER()` function assigns a sequential number to each order within each customer group.

# 

# \### Screenshot

# 

# !\[Window Function 2](screenshots/window\_2\_order\_numbering.png)

# 

# \### Business Interpretation

# 

# This allows management to track customer purchasing history and ordering frequency.

# 

# \---

# 

# \## Window Function 3: Running Revenue Total

# 

# \### Objective

# 

# Display cumulative revenue over time.

# 

# \### Explanation

# 

# The query first calculates revenue for each order and then uses:

# 

# ```sql

# SUM() OVER()

# ```

# 

# to generate a running total.

# 

# \### Screenshot

# 

# !\[Window Function 3](screenshots/window\_3\_running\_revenue.png)

# 

# \### Business Interpretation

# 

# This query shows how total supermarket revenue grows over time and helps monitor sales performance.

# 

# \---

# 

# \## Window Function 4: Days Between Orders

# 

# \### Objective

# 

# Calculate the number of days between consecutive orders for each customer.

# 

# \### Explanation

# 

# The `LAG()` function retrieves the previous order date for each customer.

# 

# The difference between the current order date and previous order date is then calculated.

# 

# \### Screenshot

# 

# !\[Window Function 4](screenshots/window\_4\_days\_between\_orders.png)

# 

# \### Business Interpretation

# 

# This helps management understand customer purchase frequency and identify customers who shop regularly.

# 

# \---

# 

# \# Overall Business Insights

# 

# The SQL analysis provides valuable information about:

# 

# \- Customer purchasing behavior

# \- Customer spending patterns

# \- Product demand

# \- Order frequency

# \- Revenue growth trends

# \- Customer loyalty

# \- Time intervals between purchases

# 

# These insights can support better marketing strategies, inventory planning, and customer relationship management.

# 

# \---

# 

# \# Challenges Encountered and Solutions

# 

# \## Challenge 1: Oracle Listener Connection Error

# 

# \### Problem

# 

# While connecting Oracle SQL Developer to Oracle Database 21c XE, the following error occurred:

# 

# ```text

# ORA-12505: TNS Listener does not currently know of SID given in connect descriptor

# ```

# 

# \### Solution

# 

# The Oracle Listener status was checked using:

# 

# ```cmd

# lsnrctl status

# ```

# 

# It was discovered that the listener was configured on port \*\*1522\*\* rather than the default port \*\*1521\*\*.

# 

# The SQL Developer connection was updated as follows:

# 

# ```text

# Hostname: localhost

# Port: 1522

# Service Name: XEPDB1

# ```

# 

# The connection was then established successfully.

# 

# \---

# 

# \## Challenge 2: Understanding Window Functions

# 

# \### Problem

# 

# Initially, it was difficult to understand how functions such as `RANK()`, `ROW\_NUMBER()`, and `LAG()` operate across rows.

# 

# \### Solution

# 

# Additional testing was performed using sample queries and result comparisons. This improved understanding of how window functions process ordered data while preserving individual rows.

# 

# \---

# 

# \# Conclusion

# 

# This assignment demonstrates practical SQL skills using Oracle Database 21c XE. Through JOIN operations, Common Table Expressions (CTEs), and Window Functions, meaningful business insights were generated from Sunrise Supermarket sales data.

# 

# The project successfully meets all assignment requirements and provides a solid foundation for advanced database analysis and reporting.

