# Route Optimizer

A Python implementation of the Traveling Salesperson Problem (TSP) designed to create globally optimized itineraries using real-world geographic data.

## Overview
This tool computes the most efficient route between multiple locations by solving the TSP via the **Held-Karp algorithm**. It integrates the **Google Maps Distance Matrix API** for precise distance and duration metrics and leverages **Gemini 2.0 Flash** to dynamically discover and format points of interest.

---

## Key Features

* **Dual Optimization Modes**: 
    * **Hamiltonian Cycle**: For round-trips where you must return to the starting location.
    * **Hamiltonian Path**: For open-ended journeys where you finish at a different location.
* **Granular Path Constraints**:
    * **Flexible Start**: Option to either lock the starting point to the first city or allow the algorithm to determine the mathematically optimal starting node.
    * **Flexible Arrival**: Toggle between forcing the trip to end at a specific destination (e.g., your hotel or a station) or letting the solver find the most efficient endpoint.
* **Multi-Modal Routing**: Supports multiple travel modes including `walking`, `driving`, `bicycling`, and `transit`.
* **AI-Powered Discovery**: Automated generation of iconic attractions within a specified area using natural language prompts.
* **Instant Visualization**: Automatically generates a formatted Google Maps URL containing the optimized sequence of waypoints for immediate navigation.

---

## Tech Stack

* **Language**: Python 3
* **APIs**: Google Maps Platform (Distance Matrix), Google Generative AI (Gemini)
* **Algorithm**: Held-Karp (Dynamic Programming)

---

## Usage

1.  **Dependencies**: Install the required libraries:
    ```bash
    pip install googlemaps google-generativeai
    ```
2.  **API Keys**: Insert your API key in the configuration section.
3.  **Configuration**:
    * Set `PROBLEM_TYPE`: `1` for Cycle, `2` for Path.
    * Set `FREE_START`: `True` to optimize the starting point, `False` to fix it.
    * Set `FREE_ARRIVAL`: `True` for an open finish, `False` to force arrival at the last city in your list.
    * Choose your `cost_metric` (`distance` or `duration`) and `travel_mode`.
4.  **Execution**: Run the notebook cells to generate the cost matrix, solve the route, and receive the Google Maps link.

---

## Technical Specifications

### Algorithm & Complexity
The solver utilizes the Held-Karp dynamic programming approach to ensure global optimality for the selected set of locations. Unlike heuristic methods, this guarantees the shortest possible path.
The time complexity is: 
$$O(n^2 2^n)$$
Where $n$ is the number of locations.

### Path Logic
For Hamiltonian Paths, the algorithm initializes the DP table by evaluating all possible starting nodes if `FREE_START` is enabled. The final cost is determined by scanning the complete set of visited nodes (full mask) to find the minimum value:
$$\min_{j \in \{0 \dots n-1\}} DP[\text{full\_mask}][j]$$

---

## Disclaimer
This tool requires a valid Google Maps API key with the Distance Matrix API enabled. Usage may incur costs depending on your Google Cloud Platform billing tier.
