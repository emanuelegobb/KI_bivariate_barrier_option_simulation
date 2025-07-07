# KI_bivariate_barrier_option_simulation
# Monte Carlo Pricing of a Knock-In Call Option

This repository contains a Python implementation (via Jupyter Notebook) for pricing a **knock-in call option** using a **Monte Carlo simulation** approach. The option is based on two correlated assets with discrete monitoring, and the payoff depends on whether the barrier condition on the first asset is met.

## 📘 Overview

* **Product:** European-style knock-in call option on two assets
* **Barrier Type:** Up-and-in (on the first underlying asset)
* **Pricing Method:** Monte Carlo simulation
* **Correlation:** The two assets are simulated with positive correlation

## 📈 Features

* Simulates correlated geometric Brownian motions for the two assets
* Weekly monitoring of the barrier condition
* Calculation of discounted expected payoff at maturity
* Visualization of simulation paths
* 3D surface plots of option value across different volatility and correlation values
* Analysis of confidence intervals and convergence
* Comparison with a digital knock-in option
* Computation of option Greeks

## 🧲 Theoretical Background

This project simulates the pricing of a Knock-In European Call option, whose payoff depends on two securities:

* **S1** determines the activation of the barrier.
* **S2** is the underlying of the call once the barrier is touched.

Let the barrier level `b > S1(0)` be monitored at discrete dates. The barrier is activated if:

```
max{S1(t1), ..., S1(tM)} ≥ b
```

The final payoff is:

```
X(T) = max(S2(T) - K, 0) × 𝟙{barrier is breached}
```

This framework enables the simulation of price paths and determination of payoffs conditional on barrier activation.

### Monte Carlo Implementation

* Discrete-time SDEs for asset dynamics
* 10,000 simulations with weekly monitoring (52 steps)
* Barrier activation tracked via max price of S1 in each path
* European call payoff computed on S2 and filtered based on barrier
* Final price: discounted expected value over all valid paths

### Sensitivity Analysis

* Explored how the price responds to changes in volatility (`v1`, `v2`) and correlation (`rho`)
* Observed flattening of price sensitivity to `v1` as `rho` increases
* Found increasing sensitivity to `v2` with higher correlation

### Confidence Interval Study

* Investigated how price precision improves with:

  * More frequent monitoring (e.g., daily vs weekly)
  * Increasing number of simulations (diminishing returns above \~6000)

### Digital Option Comparison

* Compared knock-in call with a knock-in **digital** option
* Identified differences in price behavior relative to `v1` and `v2`

### Greeks Computation

* Computed **Delta**, **Gamma**, and **Vega** using central difference estimators
* Notable findings:

  * Greater Vega for `v2` than `v1`
  * Delta more sensitive to `S2` than `S1`
  * Gamma near zero, but becomes more relevant near the barrier

## 🧮 Parameters Used

* `r`: risk-free interest rate (5%)
* `q_1`, `q_2`: dividend yields (2%)
* `v_1`, `v_2`: volatilities (20%, 25%)
* `rho`: correlation between assets (0.5)
* `S0_1`, `S0_2`: initial prices of the assets (100)
* `b`: barrier level (120) on Asset 1
* `K`: strike price (120) for the call on Asset 2
* `T`: time to maturity (1 year)
* `m`: monitoring frequency (weekly → 52 steps)
* `n_sim`: number of simulations (10,000)

## 🗂 Files

* `MC_KI_call_final.ipynb`: Jupyter notebook with full simulation and analysis
* `README.md`: Project documentation

## 📦 Dependencies

This project requires:

```bash
numpy
pandas
matplotlib
seaborn
scipy
```

Install them with:

```bash
pip install numpy pandas matplotlib seaborn scipy
```

## 🚀 Running the Notebook

1. Clone this repository.
2. Open `MC_KI_call_final.ipynb` with Jupyter or VS Code.
3. Run all cells to reproduce the simulations and results.

## 📊 Sample Outputs

* Option price estimate
* Distribution of payoffs
* Path visualizations
* Sensitivity plots
* Greeks and confidence interval analysis
* Digital option comparison

## 📜 Intellectual Property

This project was developed as part of the group assignment for the course Applied Numerical Finance at Bocconi University. All intellectual property rights are held by the group members listed below: Arjola Cibaj, Rodolfo Cociani, Stefano Franciotti, Emanuele Gobbato, Elena Kutsak, Sara Maresca.
