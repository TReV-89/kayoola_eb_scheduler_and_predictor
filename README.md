# EB Scheduler and Predictor

This project provides a comprehensive solution for managing Kayoola Electric Bus (EB) operations. It combines machine learning for energy estimation with mathematical optimization for fleet scheduling, specifically designed to minimize battery degradation and optimize resource usage for routes (e.g., Jinja-Iganga).

## Project Overview

The system consists of two main components located in the `notebooks/` directory:

1.  **EV Energy Predictor (`EVEnergyPredictor.ipynb`)**:
    *   **Goal**: Predicts energy consumption (kWh) for specific trips based on variable conditions.
    *   **Method**: Uses Machine Learning models (Gradient Boosting, Random Forest, SVR) trained on historical trip data.
    *   **Features Used**: Distance, Passenger Count, Temperature, Average Speed, Terrain Type (Hilly/Non-hilly), and Traffic Conditions.

2.  **EB Scheduler (`EBscheduling.ipynb`)**:
    *   **Goal**: Generates optimal daily schedules for electric buses to service a set of fixed trips.
    *   **Method**: Uses Mathematical Programming (Mixed-Integer Linear Programming) and Multi-Objective Evolutionary Algorithms (NSGA-II).
    *   **Objectives**:
        *   Minimize Battery Degradation (health-conscious charging).
        *   Optimize the number of buses required.
    *   **Constraints**: Manages State of Charge (SOC), charging intervals, trip start/end times, and grid limitations.

## Prerequisites

-   **Python 3.8+**
-   **Optimization Solvers**: This project utilizes **Gurobi** and **AMPL** for solving complex optimization problems. You will need valid licenses for these solvers.

## Installation

1.  **Clone the repository**:
    ```bash
    git clone <repository_url>
    cd eb_scheduler_and_predictor
    ```

2.  **Install dependencies**:
    Install the required Python packages listed in `requirements.txt`:
    ```bash
    pip install -r requirements.txt
    ```

3.  **Environment Configuration**:
    Create a `.env` file in the root directory to store your solver license keys. The project expects the following variables (see `.env` for template):
    ```ini
    # Gurobi WLS Credentials
    GUROBI_WLSACCESSID="your_access_id"
    GUROBI_WLSSECRET="your_secret"
    GUROBI_LICENSEID="your_license_id"

    # AMPL License
    AMPL_LICENSE_UUID="your_ampl_uuid"
    ```

## Usage

### 1. Energy Prediction
Open `notebooks/EVEnergyPredictor.ipynb`. This notebook loads historical EV data, processes features (handling outliers and categorical data), trains the regression models, and saves the best model for use by the scheduler.

### 2. Scheduling Optimization
Open `notebooks/EBscheduling.ipynb`. This notebook:
1.  Loads trip parameters (Start times, End times).
2.  Uses the trained predictor to estimate energy demand for each trip.
3.  Constructs a **Pyomo** concrete model.
4.  Solves the scheduling problem using **Gurobi** (via `amplpy` or `gurobipy`).

## Technologies

*   **Optimization**: Pyomo, Gurobi, AMPL
*   **Machine Learning**: Scikit-Learn (GradientBoosting, RandomForest), Pandas, NumPy
*   **Visualization**: Matplotlib// filepath: /Users/trevorsaaka/Desktop/KMC/eb_scheduler_and_predictor/README.md

