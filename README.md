# Route Optimizer 📍

A Python implementation of the Traveling Salesperson Problem (TSP) designed to create optimized itineraries using real-world geographic data.

## Overview
This tool computes the most efficient route between multiple locations by solving the TSP via the **Held-Karp algorithm** (Dynamic Programming). It integrates the **Google Maps Distance Matrix API** for accurate distance and duration metrics and uses **Gemini 2.0 Flash** to dynamically generate points of interest.

## Key Features
- **Flexible Optimization**: Supports both Hamiltonian Cycles (returning to start) and Hamiltonian Paths (point-to-point).
- **Multi-Modal**: Configurable travel modes (walking, driving, bicycling, transit) and cost metrics (distance or duration).
- **AI Integration**: Optional automated attraction discovery via Google Gemini.
- **Visual Output**: Generates a ready-to-use Google Maps directions link for the optimized sequence.

## Tech Stack
- **Language**: Python
- **APIs**: Google Maps Platform, Google Generative AI
- **Algorithm**: Held-Karp (Dynamic Programming)

## Usage
1. Insert your `MAPS_API_KEY` and `GEMINI_API_KEY`.
2. Define your `PROBLEM_TYPE` (1 for Cycle, 2 for Path).
3. Set the `search_area` and number of attractions.
4. Run the notebook to get the optimized stop sequence and the Maps URL.

## Technical Note
The solver ensures global optimality for the selected set of locations, providing a logically coherent sequence based on the chosen cost metric. Due to the $O(n^2 2^n)$ time complexity of the Held-Karp algorithm, performance scales exponentially; it is highly efficient for small-to-medium itineraries but becomes computationally expensive with more than 15-20 locations.
