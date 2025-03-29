# Problem 1

# Measuring Earth's Gravitational Acceleration with a Pendulum

## Motivation

The acceleration due to gravity $(g)$ is a fundamental constant that influences motion on Earth. One classic method to determine $(g)$ is through the oscillations of a simple pendulum, where the period of the pendulum depends on the gravitational field strength. This experiment offers hands-on practice in both measurement and uncertainty analysis — core components of experimental physics.

---

## Objective

- Measure the gravitational acceleration $(g)$ using a pendulum.
- Analyze the uncertainties in length and timing.
- Compare measured $(g)$ to the accepted value $(9.81 , text{m/s}^2)$ .

---

## Materials

- String of length: **1.00 m**
- Weight: keychain
- Ruler (±1 cm resolution)
- Stopwatch (±0.01 s resolution)
- Support for suspension

---

## Procedure

- Measured pendulum length:  
  $[
  L = 1.00 , \text{m}, \quad \Delta L = \pm 0.005, \text{m}]$
- Conducted 10 measurements of the time for 10 full oscillations:  
  $( T_{10} )$ in seconds:  
  `20.02, 19.88, 20.15, 20.00, 20.10, 19.95, 20.05, 20.00, 20.08, 19.90`

---

## Tabulated Data

| Trial | Time for 10 Oscillations (s) |
| ----- | ---------------------------- |
| 1     | 20.02                        |
| 2     | 19.88                        |
| 3     | 20.15                        |
| 4     | 20.00                        |
| 5     | 20.10                        |
| 6     | 19.95                        |
| 7     | 20.05                        |
| 8     | 20.00                        |
| 9     | 20.08                        |
| 10    | 19.90                        |

---

## Calculations

### 1. Calculate the period:

$[
T = \frac{\\overline{T}_{10}}{10} = \frac{20.013}{10} = 2.0013, \text{s}, \quad \Delta T = \frac{0.0863}{10} = 0.00863, \text{s}]$

### 2. Determine $(g)$:

$[g = \frac{4\pi^2 L}{T^2} = \frac{4\\pi^2 \cdot 1.00}{(2.0013)^2} \approx 9.857, \text{m/s}^2]$

### 3. Propagate uncertainties:

$[\Delta g = g \sqrt{ \left( \frac{\\Delta L}{L} \right)^2 + \left( 2 \cdot \\frac{\Delta T}{T} \right)^2 }]$

$[\Delta g = 9.857 \cdot \sqrt{ \left( \\frac{0.005}{1.00} \right)^2 + \left( 2 \\cdot \frac{0.0273}{2.0013} \right)^2 } \\approx 0.273, \text{m/s}^2]$

---

## Final Result

$[g = (9.857 \pm 0.273), \text{m/s}^2]$

---

## Python Simulation of Pendulum Motion

To better understand the relationship between the pendulum’s period and gravity, we simulate the motion using the formula:

$\theta(t) = \theta_0 \cos\left(\frac{2\\pi t}{T}\right)$

Where:

- $(\theta_0)$ is the initial angle (in radians)
- $(T = 2\pi \sqrt{L / g})$ is the period

---

### Python Code

```python
import numpy as np
import matplotlib.pyplot as plt

# Simulate simple pendulum period based on L and g
def pendulum_period(L, g=9.81):
    return 2 * np.pi * np.sqrt(L / g)

# Simulate oscillation and time trace
def simulate_pendulum_motion(L, g=9.81, theta0_deg=5, time_max=10, dt=0.01):
    theta0 = np.radians(theta0_deg)
    T = pendulum_period(L, g)
    t = np.arange(0, time_max, dt)
    theta = theta0 * np.cos(2 * np.pi * t / T)
    return t, theta, T

# Parameters
L_sim = 1.0  # length in meters
g_sim = 9.81  # gravitational acceleration
t_vals, theta_vals, T_theoretical = simulate_pendulum_motion(L_sim, g_sim)

# Plot the simulated angular displacement vs time
plt.figure(figsize=(10, 4))
plt.plot(t_vals, theta_vals)
plt.title(f"Simulated Pendulum Motion (L = {L_sim} m, g = {g_sim} m/s²)")
plt.xlabel("Time (s)")
plt.ylabel("Angular Displacement (rad)")
plt.grid(True)
plt.tight_layout()
plt.show()
```

![Output](Simulated%20pendulum.png)

## Analysis

### 1. Comparison:

- Measured $(g)$: **9.857 m/s²**
- Standard $(g)$: **9.81 m/s²**
- Absolute error: **0.047 m/s²**
- Relative error:  
  $frac{0.047}{9.81} \times 100\\% \approx 0.48\\%$

### 2. Discussion:

- **Effect of ΔL**: The uncertainty in length (±0.005 m) contributed minimally compared to timing uncertainty.
- **Effect of ΔT**: Variability in human reaction time causes larger uncertainty in timing. Measuring 10 oscillations helps reduce this.
- **Limitations**:
  - Small angle approximation must hold (<15°).
  - Air resistance and friction at the pivot are ignored.
  - Stopwatch precision and user reaction time affect reliability.

---

## Conclusion

Using a basic pendulum and careful timing, we measured the gravitational acceleration as:

$\boxed{g = (9.857 \\pm 0.273) \\, \text{m/s}^2}$

This result agrees well with the standard value, with less than 0.5% error. The experiment highlights how even simple tools — combined with multiple trials and uncertainty analysis — can yield precise and meaningful scientific results.
