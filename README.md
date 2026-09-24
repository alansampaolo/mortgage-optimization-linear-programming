# Mortgage Optimization with Linear Programming

Linear programming project for optimizing the allocation of multiple mortgage loans using Python and Gurobi.

## Project Overview

This project formulates a mortgage financing problem as a Linear Programming problem.

A home buyer needs to finance a fixed amount and can combine multiple mortgage loans with different:

- interest rates;
- maturities;
- maximum borrowing limits;
- minimum monthly payments.

The objective is to determine how much to borrow from each available loan and how to allocate repayments over time in order to minimize the constant total monthly payment.

The broader objective is to show how mathematical optimization can support a practical financing decision by identifying the least costly feasible allocation under multiple contractual constraints.

The optimization problem is solved using Gurobi in Python.

## Problem Setup

The baseline case assumes:

- total financing requirement: `€500,000`;
- planning horizon: `240 months`;
- four available mortgage loans: A, B, C and D.

Each loan is characterized by its own monthly interest rate, maturity, maximum available amount and minimum monthly payment. 

## Decision Variables

The main decision variables are:

- `x_i,t`: payment made on loan `i` in month `t`;
- `u_i,t`: outstanding principal of loan `i` in month `t`;
- `u_i,0`: initial amount borrowed from loan `i`;
- `k`: constant total monthly payment.

## Objective Function

The optimization problem minimizes the constant monthly payment:

`min k`

## Constraints

The model includes the following constraints:

1. the total payment across all active loans must be constant each month;
2. the initial amount borrowed from each loan cannot exceed its maximum available amount;
3. outstanding principal evolves according to interest accumulation and monthly repayments;
4. every loan must be fully repaid by its maturity;
5. total initial borrowing must equal the required financing amount;
6. each loan must satisfy its minimum monthly payment requirement.

The outstanding principal evolves according to:

`u_i,t = (1 + r_i) * u_i,t-1 - x_i,t`

The complete primal formulation is reported in the project report.

## Primal Solution

The primal Linear Programming problem is implemented and solved using Gurobi.

For the baseline scenario, the optimal constant monthly payment is approximately:

`€2,792.22`

The optimizer simultaneously determines:

- how much to borrow from each loan;
- the payment allocated to each loan in each month;
- the outstanding principal over time.

The notebook also provides a graphical representation of the monthly payment allocation across the different loans. 
## Standard Form

The primal problem is also rewritten in standard form.

Slack variables are introduced to transform inequality constraints into equality constraints, providing the basis for the derivation of the dual problem.

The standard-form model is then solved again using Gurobi.

## Dual Problem

The dual Linear Programming problem is derived from the standard-form primal problem.

Dual variables are associated with each primal constraint, while the dual constraints are constructed using the matrix relationship:

`A^T y <= c`

The dual objective is formulated using the corresponding right-hand-side vector and dual variables.

The dual problem is then implemented and solved independently in Gurobi.

## Strong Duality

The primal and dual optimization problems return the same optimal objective value:

`Primal optimum = €2,792.22`

`Dual optimum = €2,792.22`

This result verifies the Strong Duality Theorem for the optimization problem.

Strong duality states that, at optimality, the optimal objective value of the primal problem equals the optimal objective value of the corresponding dual problem. 

## Complementary Slackness

Complementary slackness conditions are also verified numerically.

These conditions link the primal and dual optimal solutions.

For each corresponding primal-dual pair, the product between a slack and its associated dual quantity must be equal, or numerically very close, to zero.

The implementation checks these conditions using numerical tolerances to account for floating-point precision. 

## Sensitivity Analysis

The project investigates how the optimal monthly payment changes when the parameters of the problem are modified.

Three main scenarios are considered:

- an increase in all interest rates;
- an increase in the maximum available amount of the cheapest loan;
- the removal of one loan together with changes in the borrowing limits of other loans.

The results show that the optimal payment is considerably more sensitive to changes in interest rates than to changes in borrowing limits.

For example:

- baseline monthly payment: `€2,792.22`;
- higher interest rates: `€2,918.85`;
- increased borrowing limit for loan D: `€2,791.53`;
- modified loan availability: `€2,799.72`.

A second dataset with different financing requirements and loan characteristics is also tested. 

## Sensitivity Report

The project also examines:

- reduced costs;
- shadow prices.

Reduced costs provide information on how the objective coefficient of a variable would need to change before the variable becomes attractive in the optimal solution.

Shadow prices measure how the optimal objective value changes following a marginal change in the right-hand side of a constraint. 

## Repository Structure

```text
mortgage-optimization-linear-programming/
│
├── README.md
├── mortgage_optimization.ipynb
└── mortgage_optimization_report.pdf
```

## Main Files

- `mortgage_optimization.ipynb` — complete Python implementation of the primal, standard-form primal, dual problem, complementary slackness checks and sensitivity analysis
- `mortgage_optimization_report.pdf` — mathematical formulation, results and interpretation of the optimization problem

## Technologies

- Python
- Gurobi / gurobipy
- pandas
- matplotlib
- Linear Programming

## Main Findings

- Linear Programming can be used to determine an optimal combination of mortgage loans subject to financial and contractual constraints.
- The baseline problem produces an optimal constant monthly payment of approximately `€2,792.22`.
- The primal and dual problems produce the same optimal objective value, confirming strong duality.
- Complementary slackness conditions are verified numerically.
- The solution is more sensitive to changes in interest rates than to changes in individual loan borrowing limits.
- Shadow prices and reduced costs provide additional information on the sensitivity of the optimal solution.
- The framework illustrates how Linear Programming can be used as a decision support tool for choosing among competing financing alternatives under real world constraints.

## Limitations

The loan characteristics used in the analysis are assumed rather than obtained from observed mortgage market data.

The project is therefore intended as an optimization and methodological exercise rather than as a real-world mortgage recommendation.
