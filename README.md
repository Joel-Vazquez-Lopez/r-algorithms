# R Algorithms

Algorithms, search, and computational methods implemented in R.

This repository collects algorithmic projects developed while studying artificial intelligence, algorithms and data structures, and related computational methods.

The focus is on implementing algorithms from first principles, understanding their mathematical foundations, and evaluating their behaviour experimentally.

## Projects

### Delivery Man — A* Search

A group project implementing an autonomous delivery agent in R. The agent uses A* search for route planning on a dynamically weighted road network and a target-selection strategy for package collection and delivery.

The final controller achieved a mean score of **171.79 turns over 500 simulations**, meeting the project target of **≤180 turns**.

**Topics:** A* search · heuristic search · graph traversal · shortest paths · dynamic edge costs · decision strategies

**Language:** R

[View project](delivery-man/)

### Where's Croc — Hidden Markov Model and BFS Search

A group project building an autonomous crocodile-tracking agent in R. The agent combines a Hidden Markov Model-style belief update with sensor and tourist observations to estimate the crocodile's location, then uses breadth-first search to navigate a network of waterholes.

The notebook includes an example simulation and a test call. Running it requires the external `WheresCroc` R package (version 1.2.2), which is not bundled in this repository.

**Topics:** Hidden Markov Models · Bayesian filtering · Gaussian likelihoods · graph traversal · BFS · shortest paths · probabilistic decision-making

**Language:** R

[View project](wheres-croc/)
