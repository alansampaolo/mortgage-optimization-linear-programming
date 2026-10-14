# Mortgage Optimization with Linear Programming

Team project, Optimization Methods — University of Pavia (2025) · Python · Gurobi

## Objective

The objective was to **determine the optimal allocation across multiple mortgage options in order to minimise the total monthly payment while satisfying borrowing and repayment constraints**. The project also used **sensitivity analysis to understand how changes in constraints affect the optimal solution**.

## Setup

| | |
|---|---|
| **Problem** | Finance €500,000 over 240 months by combining four loans with different maturities (5–20 years), interest rates (about 2.6–3.2% per year), borrowing limits and minimum monthly payments |
| **Decision variables** | Amount borrowed from each loan, monthly payment on each loan, outstanding principal over time, constant total monthly payment `k` |
| **Model** | Minimise `k` subject to borrowing limits, principal dynamics `u_i,t = (1 + r_i)·u_i,t−1 − x_i,t`, full repayment at maturity, minimum payments and total financing |
| **Extensions** | Standard form, dual problem, complementary slackness, sensitivity scenarios, shadow prices, second dataset |

## Key results

- **Optimal constant monthly payment: €2,792.22** in the baseline case.
- **Strong duality verified:** the dual problem, solved independently, returns the same optimum, and complementary slackness holds numerically.
- **Interest rates matter far more than borrowing limits:** a 0.5 percentage-point rise in all annual rates raises the payment to €2,918.85 (+4.5%), while raising the limit of the cheapest loan by €50,000 lowers it by less than €1 (€2,791.53), and removing one loan while enlarging the others raises it to €2,799.72.
- **Shadow price of the financing constraint:** each additional €1,000 borrowed raises the optimal monthly payment by about €5.60.
- A second dataset (€300,000, three loans) gives an optimal payment of €1,935.87.

## Repository

- `mortgage_optimization.ipynb` — primal, standard form, dual, complementary slackness and sensitivity analysis
- `mortgage_optimization_report.pdf` — mathematical formulation, results and interpretation

**Tools:** Python · Gurobi (gurobipy) · pandas · Matplotlib
