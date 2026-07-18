# Supermarket Sales SQL Analysis

## Overview 

I built this project to practice SQL using a supermarket sales dataset. The idea was simple: pretend I'm an analyst working for a retail chain, and use SQL to figure out things the business would actually want to know like which products sell the most, which branch brings in the most money, and when customers shop the most.

I picked this topic because retail sales data is something almost everyone can relate to (we've all been the customer in one of these transactions), and it has enough variety  branches, product lines, payment methods, timestamps  to practice a good range of SQL concepts, not just basic SELECT statements.

This isn't meant to be a polished business report. It's a learning project where I focused on writing clean queries, thinking about what questions actually matter, and getting comfortable with things like grouping, subqueries, and date functions.

## Inside the Dataset 

The dataset contains simulated sales transactions from a supermarket chain operating across three branches  Pune, Mumbai, and Delhi. Each row represents a single invoice and includes details such as:

* Branch and city
* Customer type (Member or Normal) and gender
* Product line purchased (e.g., Electronics, Fashion, Sports)
* Unit price, quantity, tax (VAT), and total amount
* Date and time of purchase
* Payment method
* Cost of goods sold (COGS) and gross income
* Customer rating for the transaction

## Why This Dataset ?

Honestly, I wanted something that felt real, not just a toy dataset with random numbers. Sales data made sense because businesses actually use this kind of analysis all the time  knowing which products are worth stocking more of, which branch might need attention, or when customers are most active isn't just theoretical, it's stuff real companies pay analysts to figure out.

So instead of just writing SELECT statements for the sake of it, I tried to approach each query like I was actually trying to answer a question someone would ask me, like "which branch is doing the best?" or "what do our customers like buying?"

## What I Did

1. Created the table schema, deciding what data types and constraints made sense for each column.
2. Inserted sample transaction data so I'd have something to actually query, similar to what a real store's database might look like.
3. Added a few extra columns that weren't in the original data but made the analysis easier:
   * time_of_day  turns the timestamp into Morning, Afternoon, Evening, or Night
   * day_name  pulls out the day of the week from the date
   * month_name pulls out the month from the date
4. Wrote queries grouped into a few categories, just to keep things organized:
   * Product Analysis  best-selling products, top revenue, best ratings
   * Sales Analysis  revenue and VAT trends across branches and time
   * Customer Analysis  how customer type and gender relate to spending and ratings
   * General Questions  basic stuff like how many branches/cities are in the data

## Skills Practiced

* Writing DDL statements (CREATE TABLE, ALTER TABLE)
* Inserting and updating data (INSERT, UPDATE)
* Using CASE statements for feature engineering
* Aggregate functions (SUM, AVG, COUNT) combined with GROUP BY and HAVING
* Subqueries for comparative analysis (e.g., branches performing above average)
* Date and time functions (DAYNAME, MONTHNAME, HOUR)
* Sorting and filtering results to answer specific business question
