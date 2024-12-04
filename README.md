# Milestone1Skill
1. Personal Expense Tracker API
Overview
Managing daily expenses is crucial for budgeting and financial planning. The Personal Expense
Tracker API helps users log, view, and analyze their expenses. It provides insights into spending
patterns and assists in better decision-making.
Features
1. Add a new expense with details such as category, amount, and date.
2. Retrieve a summary of expenses filtered by category or date range.
3. Analyze spending patterns, such as the highest spending category or monthly totals.
4. Generate a weekly or monthly summary report using automated tasks.
5. Requirements

● Endpoints:
○ Add Expense (POST /expenses): Log a new expense.
○ Get Expenses (GET /expenses): Retrieve expenses based on filters like category
or date range.
○ Analyze Spending (GET /expenses/analysis): Get insights like total by
category or time.
○ Generate Summary (CRON job): Automated reports for daily / weekly / monthly
expense summaries.

● Data Validation (Optional) :
○ Expense categories (e.g., "Food", "Travel") must be predefined.
○ Amount must be a positive number.

● Response Format: JSON structured as { status, data, error }.
Solution Design

● Use arrays for in-memory storage.

● Implement sorting and filtering logic to retrieve and group expenses.

● Leverage node-cron for generating summary reports



**Personal Expense Tracker API Report**
Objective
The purpose of this API is to manage and track personal expenses, analyze spending, and provide summary reports. The application is built using Node.js and uses Express.js for handling HTTP requests.

Features Implemented
Expense Tracking

Users can add expenses by providing a category, amount, and date.
Users can retrieve their expenses with optional filters for category, start date, and end date.
Spending Analysis

Generate summaries of spending by category over different periods (daily, weekly, monthly, or all time).
Identify the category with the highest spending and its total amount.
Automated Summaries

Scheduled daily, weekly, and monthly expense summaries using the node-cron library, which logs summaries to the console at specified intervals.
Validation and Error Handling

Validates input for required fields, positive amounts, valid dates, and predefined categories.
Returns clear error messages for invalid input.
Debugging

A dedicated route to view all stored expenses for debugging purposes.
Endpoints
Home

GET /
Returns a welcome message.
Add Expense

POST /expenses
Adds a new expense.
Required Fields: category, amount, date
Validations:
category must belong to a predefined list: ["Food", "Travel", "Entertainment", "Utilities", "Other"].
amount must be a positive number.
date must be a valid date string.
Get Expenses

GET /expenses
Retrieves expenses, optionally filtered by:
category
startDate (inclusive)
endDate (inclusive)
Spending Analysis

GET /expenses/analysis
Provides:
A summary of spending by category (all time).
The category with the highest spending and its total.
Debugging

GET /debug/expenses
Returns all stored expenses for debugging.
Scheduled Jobs
Using the node-cron library, the following automated reports are generated:

Daily Expense Summary

Scheduled to run every day at midnight (0 0 * * *).
Logs a summary of the day's expenses.
Weekly Expense Summary

Scheduled to run every Sunday at midnight (0 0 * * 0).
Logs a summary of the past 7 days' expenses.
Monthly Expense Summary

Scheduled to run on the 1st day of every month at midnight (0 0 1 * *).
Logs a summary of the past month's expenses.
In-Memory Storage
The expenses array stores all expense records.
Structure of an expense:
json
Copy code
{
  "category": "Food",
  "amount": 150.5,
  "date": "2024-12-04T00:00:00.000Z"
}
Helper Functions
generateSummary(period)

Filters and aggregates expenses based on the specified time period (daily, weekly, monthly, or all).
Returns a category-wise summary of spending.
getHighestSpendingCategory()

Determines the category with the highest total spending and its amount.
Technologies Used
Node.js: Server-side runtime environment.
Express.js: Web framework for building RESTful APIs.
body-parser: Middleware for parsing JSON payloads.
node-cron: Library for scheduling tasks.
Strengths
Modular Design: Helper functions and predefined categories make it easy to extend functionality.
Validation: Prevents invalid input and ensures data consistency.
Automation: Automatically provides timely summaries of expenses.
Real-Time Analysis: Easily retrieve filtered expenses and summaries through API calls.
Potential Enhancements
Data Persistence: Replace in-memory storage with a database (e.g., MongoDB, PostgreSQL) for durability.
User Authentication: Implement authentication to support multiple users and secure access.
Advanced Analysis:
Compare spending trends over different periods.
Provide suggestions for cost-saving.
UI Integration: Create a frontend for users to interact with the API.
Export Reports: Allow users to export summaries in formats like PDF or CSV.
Execution
Run the application:

bash
Copy code
node app.js
Access the API at:
http://localhost:6000
