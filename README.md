# Route Optimizer

A Python implementation of the Traveling Salesperson Problem (TSP) designed to create globally optimized itineraries using real-world geographic data.

## Overview
This tool computes the most efficient route between multiple locations by solving the TSP via the **Held-Karp algorithm**. It integrates the **Google Maps Distance Matrix API** for precise distance and duration metrics and leverages **Gemini 2.0 Flash** to dynamically discover and format points of interest.

---

## Key Features

* **Dual Optimization Modes**: 
    * **Hamiltonian Cycle**: For round-trips where you must return to the starting location.
    * **Hamiltonian Path**: For open-ended journeys where you finish at a different location.
* **Path Constraints**:
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

## Algorithm & Complexity
The solver utilizes the Held-Karp dynamic programming approach to ensure global optimality for the selected set of locations. Unlike heuristic methods, this guarantees the shortest possible path.
The time complexity is: 
$$O(n^2 2^n)$$
Where $n$ is the number of locations.

---

## Disclaimer & Limitations

### 1. Usage Limits and Scalability
To ensure optimal performance and avoid errors, do not input an excessive number of destinations. This tool is subject to three main constraints:
* **Algorithmic Complexity**: The Held-Karp algorithm has a time complexity of $O(n^2 2^n)$. While it guarantees a global optimum, performance will degrade exponentially beyond 15–20 locations.
* **API Constraints**: The Google Maps Distance Matrix API typically allows up to 25 origins and 25 destinations per request.
* **Navigation Limits**: The generated Google Maps URL is subject to Google's waypoint limits.

### 2. Data Accuracy & Route Robustness
* **API Discrepancies**: Minor differences in distance or duration may exist between the Distance Matrix API and the standard Google Maps consumer app/website.
* **Sensitivity to Proximity**: When destinations are very close to each other (e.g., within the same city block), these small discrepancies can occasionally result in a different "optimal" sequence. 
* **Large-Scale Robustness**: The optimization remains highly robust and reliable for journeys where distances between stops are significant, as minor API variations become negligible.

### 3. Costs
This tool requires a valid Google Maps API key with the Distance Matrix API enabled. Usage may incur costs depending on your Google Cloud Platform billing tier.
