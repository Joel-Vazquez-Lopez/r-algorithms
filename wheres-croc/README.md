# Where's Croc — Hidden Markov Model and BFS Search

A group project implementing an autonomous crocodile-tracking agent in R. The agent estimates the crocodile's location from uncertain observations and navigates a network of 40 waterholes to search for it.

## Overview

The agent combines **probabilistic state estimation** with **graph search**:

1. **Transition model:** Construct a 40-state transition matrix from the waterhole connections. The crocodile may remain in the same waterhole or move to an adjacent one; the implementation assigns equal probability to each allowed transition.
2. **Prediction:** Propagate the location probability distribution through the transition matrix to estimate the crocodile's next position.
3. **Observation updates:** Reweight the distribution using sensor readings, tourist information, and waterholes where earlier searches were unsuccessful.
4. **Navigation:** Use breadth-first search (BFS) to precompute shortest-path steps between waterholes, then travel toward the most probable crocodile location.

The controller maintains its transition matrix, belief distribution, routing tables, and search history in `moveInfo$mem` across turns.

## Probabilistic reasoning

The implementation uses a Hidden Markov Model (HMM)-style filtering loop.

- **Initial belief:** A uniform distribution across 40 waterholes.
- **Motion prediction:** Multiply the current belief by the transition probabilities.
- **Sensor likelihood:** Evaluate each sensor reading under the Gaussian distributions provided for each waterhole (`dnorm`), multiply the likelihoods, and normalize.
- **Tourist evidence:** Rule out waterholes occupied by living tourists; a reported attack localizes the crocodile to the corresponding waterhole.
- **Unsuccessful searches:** Exclude searched waterholes from the prior belief before predicting the next movement.

The code includes fallbacks for some zero-probability updates.

## BFS navigation and action selection

The agent performs BFS from each possible destination and stores a `nextStep` table. On each turn, it selects the waterhole with the highest current posterior probability (`which.max`) and follows the precomputed shortest path toward it.

It requests a search when its movement reaches the selected target, then remembers the searched waterhole for the next probability update.

## Run the notebook

Open [`WheresCroc_Group_67.ipynb`](WheresCroc_Group_67.ipynb) in Google Colab with an **R runtime**.

The notebook depends on the **`WheresCroc` R package, version 1.2.2**, supplied as `WheresCroc_1.2.2.tar.gz`. This package archive is **not included** in the repository.

1. Obtain the game package from the original course/project distribution and upload it to the Colab session at `/content/WheresCroc_1.2.2.tar.gz`.
2. Run the notebook cells in order to install and load the package, define the agent functions, and execute the simulation.
3. The example uses `set.seed(67)`, `runWheresCroc(myFunction, doPlot = TRUE, pause = 1)`, and `testWC(myFunction)`.

The saved notebook shows the crocodile found in **2 moves in the seeded example**. This is one demonstration, not a general performance estimate. Rerunning the notebook requires the external package.

## Topics

R · Hidden Markov Models · Bayesian filtering · Gaussian likelihoods · state transitions · breadth-first search · shortest paths · probabilistic planning
