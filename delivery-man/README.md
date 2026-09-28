# Delivery Man — A* Route Planning

A group project implementing an autonomous delivery agent in R.

## Overview

The Delivery Man problem requires an agent to collect and deliver packages while navigating a grid whose road costs change over time.

The system combines two levels of decision-making:

1. **Target selection** chooses which package or delivery location the agent should pursue.
2. **A* route planning** determines a minimum-cost route to the selected target using the current road costs.

Because traffic conditions change over time, route planning is repeated using the current road costs rather than relying on a permanently fixed route.

## A* Search

Each search state represents a position on the grid. The evaluation function is:

`f(n) = g(n) + h(n)`

where:

- `g(n)` is the accumulated traversal cost from the starting position;
- `h(n)` is the Manhattan distance from the current position to the target;
- `f(n)` estimates the total cost of a route through the state.

The search maintains a frontier of discovered states and an explored set. When multiple paths reach the same position, the lower-cost path is retained.

The first movement along the selected path is propagated through the search, allowing the controller to execute one action before replanning as road conditions change.

## Evaluation

The final controller was evaluated over 500 simulations:

- **Mean:** 171.79 turns
- **Standard deviation:** 37.55
- **Runtime:** 202.24 seconds

The mean score met the project target of **≤180 turns**.

## Topics

R · A* search · heuristic search · graph traversal · shortest paths · dynamic edge costs · decision strategies
