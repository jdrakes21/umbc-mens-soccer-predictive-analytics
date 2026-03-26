# UMBC Men’s Soccer Predictive Analytics 

A structured predictive analytics project modeling how UMBC men’s soccer matches are played and how outcomes unfold using interpretable statistical methods.

This project goes beyond predicting final scores. It builds a full pipeline that analyzes match performance, models expected goals, incorporates opponent strength, and simulates future outcomes probabilistically.

---

## Project Context

This project is being developed as part of my work with the **Division of Information Technology (DoIT) at the University of Maryland, Baltimore County (UMBC)**. It represents an applied sports analytics initiative that combines statistical modeling, simulation, and data-driven performance evaluation to better understand team behavior and match outcomes.

The work reflects a professional analytics workflow, moving from exploratory performance analysis (xG/xGA) to opponent-aware predictive modeling and Monte Carlo simulation, with future plans for player-level modeling, spatial xG enhancement, and interactive dashboard development.

---

# Project Overview

This project consists of multiple analytical notebooks that build toward a complete match simulation framework.

The work progresses from:

- Performance analysis  
- Contextual modeling  
- Opponent strength estimation  
- Match simulation  

Rather than predicting a single scoreline, the goal is to simulate how matches are likely to unfold and estimate probabilistic outcomes such as wins, draws, losses, expected points, and expected goal difference.

---

# Notebooks in This Project

## 1. xG Analysis (Attacking Model)

This notebook focuses on modeling **expected goals scored (xG)**.

The attack model uses:

- Shots on goal
- Shot accuracy
- Home vs away
- Conference status
- Opponent strength
- Interaction effects

Instead of relying only on goals scored, the model estimates how many goals UMBC *should* score based on chance creation and shot quality.

**Purpose:**
- Evaluate attacking efficiency
- Identify matches where finishing over- or under-performed
- Create a performance-based attacking metric

---

## 2. xGA Analysis (Defensive Model)

This notebook models **expected goals against (xGA)**.

The defensive model uses:

- Opponent shots on goal
- Home vs away
- Conference status
- Opponent strength
- Interaction effects

**Purpose:**
- Measure defensive pressure allowed
- Identify structurally strong vs fragile performances
- Separate defensive process from final results

---

## 3. Conference vs Non-Conference Analysis

This notebook analyzes structural differences between:

- America East conference matches
- Non-conference matches

Findings explore:

- Differences in shot creation
- Changes in defensive pressure
- Variations in goal expectation
- Whether conference opponents suppress performance differently

**Purpose:**
- Understand contextual performance shifts
- Inform how conference effects should enter the models

---

## 4. Opponent Strength Modeling

This notebook builds a **leak-free opponent strength metric** using prior UMBC results only.

Opponent strength is calculated using:

- Prior goal differential vs each opponent (expanding mean)
- Shifted to prevent data leakage

**Purpose:**
- Quantify matchup difficulty
- Make models opponent-aware
- Avoid using future information

This metric becomes a key input in both attack and defense models.

---

## 5. Match Simulation Framework

The final stage integrates all previous analysis into a predictive simulation system.

Three approaches were built:

---

### A) Simple Approach (Baseline)

- Uses historical context averages (home vs away, conference vs non-conference)
- Estimates match inputs using typical values
- Simulates goals using Poisson distributions
- Runs Monte Carlo simulations to estimate win/draw/loss probabilities

**Purpose:**
- Validate the modeling pipeline
- Establish a baseline for comparison
- Confirm realistic behavior

**Limitation:**
- Treats future matches as “typical” scenarios
- Not strongly opponent-specific

---

### B) Better Approach (Opponent-Aware)

- Uses regression models to predict:
  - Shots on goal
  - Shot accuracy
  - Opponent pressure
- Inputs depend on:
  - Opponent strength
  - Conference context
  - Home advantage

Goals are then simulated using these predicted inputs.

**Improvement:**
- Adjusts match conditions based on opponent
- Produces more matchup-sensitive projections

**Limitation:**
- Predicted inputs are fixed per match
- Only goal scoring is random

---

### C) Better++ Two-Stage Stochastic Model (Most Realistic)

“Stochastic” means randomness is built into the model.

This version:

1. Simulates how the match is played  
   - Shot volume (Negative Binomial)
   - Shot accuracy variation
   - Defensive pressure variation  

2. Simulates goals based on those simulated conditions  

**Benefits:**
- Captures uncertainty in match flow
- Reduces overconfidence
- Produces more realistic outcome distributions
- Maintains interpretability

This is the strongest version of the framework.

---

# Key Modeling Techniques

- Poisson Regression (Goals)
- Negative Binomial Regression (Shot Volume)
- Binomial Logistic Regression (Shot Accuracy)
- Monte Carlo Simulation
- Two-Stage Stochastic Modeling
- Leak-Free Opponent Strength Estimation

---

# Results Summary

Across models:

- The **Simple model** tends to be slightly optimistic.
- The **Better model** reduces overconfidence by adjusting for opponent strength.
- The **Better++ model** produces the most realistic projections by simulating both match processes and goal outcomes.

The progression from **Simple → Better → Better++** demonstrates increasing realism while maintaining interpretability.

Overall, the **Better++ two-stage stochastic model** is the strongest framework in this project because it best captures both matchup-specific dynamics and the natural unpredictability of soccer.

---

# Why This Project Matters

This project shows how to:

- Move from descriptive analysis (xG/xGA) to predictive simulation
- Incorporate opponent strength without data leakage
- Introduce uncertainty properly in sports modeling
- Build interpretable, matchup-aware predictive systems

Rather than predicting a single score, this framework produces probabilistic match outcomes aligned with real-world sports uncertainty.

---

# Future Extensions

The next phase of this project will expand the analysis beyond the current team-level simulation framework and move toward more detailed and interactive analytics.

### Expanding the Dataset

The current analysis focuses on UMBC men’s soccer match data from **2023–2025**. A key next step is extending the dataset to include seasons **prior to 2023**. Incorporating additional historical seasons will increase the amount of training data available for the models, which should improve the stability and reliability of the statistical estimates. More historical data will also allow for better evaluation of long-term performance trends and model robustness.

### Player-Level Modeling

Future work will introduce **player-level models** to better understand individual contributions to team performance. Instead of modeling the team as a single unit, this extension will analyze how specific players influence shot creation, finishing quality, and defensive pressure. Player-level analysis can provide deeper insight into tactical strengths, key contributors, and how lineup changes affect overall performance.

### Improved xG Using Shot Location and Imagery

Another extension will incorporate **spatial data and imagery** to improve the expected goals (xG) calculation. The current model uses shot volume and accuracy, but future versions will consider where shots are taken from and the context of the attempt. By incorporating shot location and visual information from match imagery or tracking data, the model will be able to estimate goal probability more precisely and create a richer representation of attacking opportunities.

### Interactive Analytics Dashboard

The project will also be extended into an **interactive analytics dashboard** where users can explore the data and simulation outputs dynamically. The dashboard will allow users to:

- Explore team performance metrics such as **xG, xGA, and xGD**
- Compare simulated outcomes against different opponents
- Visualize attacking and defensive trends across matches
- Interactively view model predictions and probabilities

This will make the project more accessible to analysts, coaches, and researchers by allowing them to explore insights without needing to run the underlying code.

Together, these extensions will transform the project from a team-level predictive simulation framework into a more comprehensive sports analytics platform that integrates player analysis, spatial modeling, and interactive visualization.

---

# Author

**Jervon Drakes**  
Sports Analytics & Predictive Modeling  
Division of Information Technology (DoIT), UMBC
