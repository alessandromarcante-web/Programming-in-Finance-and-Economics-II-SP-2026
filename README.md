Code

import numpy as np

# Parameters
S0 = 100.0 # initial price
mu = 0.08 # drift
sigma = 0.2 # volatility
T = 1.0 # years
n_steps = 20
n_paths = 100

dt = T / n_steps

# Simulate GBM paths
Z = np.random.normal(size=(n_steps, n_paths))
increments = (mu - 0.5 * sigma**2) * dt + sigma * np.sqrt(dt) * Z

paths = np.empty((n_steps + 1, n_paths))
paths[0] = S0
paths[1:] = S0 * np.exp(np.cumsum(increments, axis=0))

paths

import matplotlib.pyplot as plt

time_grid = np.linspace(0, T, n_steps + 1)

plt.figure(figsize=(10, 6))
plt.plot(time_grid, paths, linewidth=1, alpha=0.7)

plt.show()  # Forza la visualizzazione
plt.title("Simulated GBM Stock Price Paths")
plt.xlabel("Time (years)")
plt.ylabel("Stock Price")
plt.grid(True, alpha=0.3)
plt.show()
