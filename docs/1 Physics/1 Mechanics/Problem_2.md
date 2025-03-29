# Problem 2

# Investigating the Dynamics of a Forced Damped Pendulum

## 1. Theoretical Foundation

The equation of motion for a forced damped pendulum is:

$$ \frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \sin\theta = A \cos(\omega t )$$

Where:

- $theta$: angular displacement
- $gamma$: damping coefficient
- $omega_0$: natural frequency of the pendulum
- $A$: amplitude of the driving force
- $omega$: frequency of the driving force

### Small-Angle Approximation

For small angles, $\sin(\theta)$ $\approx$ $\theta$. The equation becomes:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \theta = A \cos(\omega t)
$$

This is a linear second-order differential equation with periodic forcing.

### Resonance

Resonance occurs when the driving frequency $omega$ is close to the natural frequency $omega_0$. The system absorbs energy efficiently, and oscillations can grow significantly if damping is low.

## 2. Analysis of Dynamics

- **Damping Coefficient $gamma$**: Increases energy loss. High $gamma$ suppresses oscillations.
- **Driving Amplitude $A$**: Larger values can lead to chaotic motion.
- **Driving Frequency $omega$**: Controls resonance and synchronization effects.

Chaotic behavior emerges when nonlinearities dominate, especially at high amplitudes and low damping.

## 3. Practical Applications

- **Energy Harvesting**: Capturing vibrational energy using resonant systems.
- **Suspension Bridges**: Avoiding resonant frequencies during design.
- **Oscillating Circuits**: Analogous to RLC circuits with periodic input.

## 4. Implementation

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

def pendulum(t, y, gamma, omega0, A, omega):
    theta, v = y
    dydt = [v, -gamma*v - omega0**2*np.sin(theta) + A*np.cos(omega*t)]
    return dydt

def simulate(gamma, omega0, A, omega, y0, t_span, t_eval):
    sol = solve_ivp(pendulum, t_span, y0, args=(gamma, omega0, A, omega), t_eval=t_eval)
    return sol

# Parameters
gamma = 0.2
omega0 = 1.0
A = 1.2
omega = 0.8
y0 = [0.1, 0.0]
t_span = (0, 100)
t_eval = np.linspace(*t_span, 2000)

sol = simulate(gamma, omega0, A, omega, y0, t_span, t_eval)

plt.plot(sol.t, sol.y[0])
plt.xlabel('Time')
plt.ylabel('Theta (rad)')
plt.title('Forced Damped Pendulum')
plt.grid()
plt.show()
```

![Output](velocities.png)
