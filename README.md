# Monte Carlo Simulation for Stock Price Prediction

## Overview
This project simulates **future stock price movements** using the **Monte Carlo method**. It retrieves historical stock data from **Yahoo Finance (`yfinance`)** and generates **1,000 potential price paths** over the next **100 trading days**.

## How It Works
### 1. **Download Historical Stock Data**
- Fetches closing prices for **S&P 500 (`^GSPC`)** from **Yahoo Finance**.
- Computes **daily returns & volatility** using historical data.

### 2. **Simulate Future Stock Prices**
- Uses the **Geometric Brownian Motion (GBM) model**:
  \[
  S_t = S_0 \times e^{(\mu - \frac{1}{2} \sigma^2)t + \sigma W_t}
  \]
- Generates **1,000 simulated stock price paths** for the next **100 days**.

### 3. **Visualize the Simulations**
- Plots **simulated price trajectories** over time.
- A **red dashed line** marks the **current stock price** as a reference.

## Project Files
- `montecarlo.py` → Python script for Monte Carlo simulation.
- `README.md` → Documentation (this file).
- `requirements.txt` → List of dependencies.

## Installation & Usage
### Step 1: Install Dependencies
Ensure you have Python 3 installed, then run:
```bash
pip install numpy pandas matplotlib yfinance
```

### Step 2: Run the Simulation
Execute the script:
```bash
python montecarlo.py
```

### Step 3: Interpret the Output
- The chart displays **1,000 potential future stock prices**.
- **Wide spread** → High **volatility** (higher uncertainty).
- **Most paths near the red line** → Stock is **stable** in the short term.

## Code Breakdown
### **Import Libraries**
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import yfinance as yf
```
- `numpy` → Handles random number generation & mathematical operations.
- `pandas` → Loads stock price data.
- `matplotlib.pyplot` → Visualizes stock price simulations.
- `yfinance` → Downloads **real historical stock prices**.

### **Fetching Stock Data**
```python
stock_symbol = "^GSPC"
data = yf.download(stock_symbol, start="2023-01-01", end="2024-01-01")
S0 = float(data["Close"].iloc[-1])  # Extracts last closing price
```
- Retrieves **S&P 500 data** for the past year.
- Extracts **last closing price** (`S0`), used as the **starting point**.

### **Monte Carlo Simulation**
```python
num_days = 100
num_simulations = 1000
dt = 1

stock_paths = np.zeros((num_simulations, num_days))

for i in range(num_simulations):
    Wt = np.random.normal(0, np.sqrt(dt), num_days)  # Random noise
    stock_paths[i, :] = S0 * np.exp(np.cumsum((mu - 0.5 * sigma**2) * dt + sigma * Wt))
```
- Simulates **1,000 price paths** using the **Geometric Brownian Motion model**.
- `Wt` introduces **random market fluctuations**.

### **Visualization**
```python
plt.figure(figsize=(10, 6))
for i in range(100):  # Display 100 paths for clarity
    plt.plot(stock_paths[i, :], linewidth=0.5, alpha=0.5)

plt.axhline(S0, color='r', linestyle='dashed', label="Current Price")
plt.xlabel("Days")
plt.ylabel("Stock Price")
plt.title(f"Monte Carlo Simulation for {stock_symbol}")
plt.legend()
plt.show()
```
- **Plots 100 simulated paths** (out of 1,000) for readability.
- **Red dashed line** → Represents **today's price** as a baseline.

## Interpretation & Applications
### How to Read the Chart
- **Upward trend** → Stock might be **bullish**.
- **Downward trend** → Stock might be **bearish**.
- **Wide spread** → Indicates **high volatility** and uncertainty.
- **Tight spread** → Indicates **low volatility** (predictable behavior).

### Trading Applications
- **Risk Management:** Helps estimate potential future price fluctuations.
- **Options Pricing:** Used to price derivatives by simulating different market scenarios.

## Author & Credits
- **Developed by:** Shubham Ravindra Nakhod  
- **Inspired by:** Quantitative Finance & Algorithmic Trading

