Monte Carlo Simulation for Stock Price Prediction
This project simulates future stock prices using the Monte Carlo method and Geometric Brownian Motion (GBM). It models 1,000 possible price paths for the S&P 500 (^GSPC) over the next 100 trading days using historical data from Yahoo Finance.

Overview
- Fetches historical stock prices from Yahoo Finance (yfinance)
- Computes daily return and volatility
- Simulates future price paths using the GBM model
- Visualizes simulation results with a reference to the current price

<pre> ```Project Structure

├── Monte_Carlo_Simulation.ipynb     # Jupyter notebook version of the simulation
├── montecarlo.py                    # Standalone script for simulation and plotting
├── Simulated chart.png              # Output plot of Monte Carlo simulation
├── requirements.txt                 # Required dependencies
└── README.md                        # Project documentation``` </pre>

Sample Output
![Simulated chart](https://github.com/user-attachments/assets/344727fd-2dff-47d9-a456-0cd236cbf6c7)


Installation
- Install required packages:
<pre> ```bash
pip install numpy pandas matplotlib yfinance``` </pre>

Usage
- Run the simulation script:
<pre> ```bash
python montecarlo.py``` </pre>

How It Works
1. Fetch Historical Stock Data
- Downloads S&P 500 closing prices (2023–2024)
- Extracts the last closing price (S₀)
- Calculates mean return (μ) and volatility (σ)

2. Monte Carlo Simulation with GBM
The model uses the formula:

<pre> ```lua

S(t) = S₀ * exp[(μ - 0.5σ²)t + σW(t)]
``` </pre>

Where:

* S₀: Current stock price
* μ: Historical mean return
* σ: Historical volatility
* W(t): Brownian motion (normally distributed random walk)

It simulates 1,000 possible price paths over 100 future days.

3. Visualization
- Plots 100 simulated paths for clarity
- Highlights current price with a red dashed line

Interpretation
- Upward trend → Potential bullish behavior
- Downward trend → Potential bearish behavior
- Wider spread → High volatility and uncertainty
- Tighter spread → Low volatility and predictability

Applications
- Risk Management: Estimate future price ranges under uncertainty
- Options Pricing: Simulate underlying asset paths for derivative valuation
- Scenario Testing: Model outcomes under different market assumptions
