# Problem 1

# Simulating the Effects of the Lorentz Force

## Motivation

The **Lorentz force** governs the motion of charged particles in the presence of electric and magnetic fields. It is central to understanding systems such as:

- **Particle accelerators** (e.g., cyclotrons, synchrotrons)
- **Mass spectrometers**
- **Plasma confinement devices** (e.g., tokamaks, magnetic bottles)
- **Charged particle beams** in space and astrophysics

By simulating the Lorentz force, we gain insight into how particles move under various field conditions, observe behaviors like circular or helical motion, and understand applications like velocity selectors or drift tubes.

---

## Objective

- Simulate the trajectory of a charged particle under different field configurations.
- Visualize motion in 2D/3D to observe patterns such as **circular**, **helical**, or **drift** trajectories.
- Explore how **field strength**, **initial velocity**, **mass**, and **charge** influence the motion.

---

## Methodology

We use the Lorentz force law:

$$
\vec{F} = q(\vec{E} + \vec{v} \times \vec{B})
$$

The resulting equations of motion are:

$$m \frac{d\vec{v}}{dt} = q(\vec{E} + \vec{v} \times \vec{B})$$

$$\frac{d\vec{r}}{dt} = \vec{v}$$

To numerically solve these coupled equations, we use the **Runge-Kutta 4th-order method (RK4)** for better stability and accuracy.

---

## Python Code: Particle Trajectory in E and B Fields

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants and initial parameters
q = 1.0    # Charge
m = 1.0    # Mass
v0 = np.array([1.0, 0.0, 0.0])  # Initial velocity
r0 = np.array([0.0, 0.0, 0.0])  # Initial position
E = np.array([0.0, 0.0, 0.0])   # Electric field
B = np.array([0.0, 0.0, 1.0])   # Magnetic field

dt = 0.01
steps = 3000

# Storage arrays
positions = [r0]
velocities = [v0]

# RK4 integration
def lorentz_force(v, E, B):
    return (q / m) * (E + np.cross(v, B))

for _ in range(steps):
    r = positions[-1]
    v = velocities[-1]

    k1v = lorentz_force(v, E, B) * dt
    k1r = v * dt

    k2v = lorentz_force(v + 0.5 * k1v, E, B) * dt
    k2r = (v + 0.5 * k1v) * dt

    k3v = lorentz_force(v + 0.5 * k2v, E, B) * dt
    k3r = (v + 0.5 * k2v) * dt

    k4v = lorentz_force(v + k3v, E, B) * dt
    k4r = (v + k3v) * dt

    v_new = v + (1/6)*(k1v + 2*k2v + 2*k3v + k4v)
    r_new = r + (1/6)*(k1r + 2*k2r + 2*k3r + k4r)

    velocities.append(v_new)
    positions.append(r_new)

positions = np.array(positions)

# 3D Trajectory Plot
fig = plt.figure(figsize=(10, 6))
ax = fig.add_subplot(111, projection='3d')
ax.plot(positions[:, 0], positions[:, 1], positions[:, 2])
ax.set_title("Particle Trajectory Under Uniform Magnetic Field")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_zlabel("z")
plt.tight_layout()
plt.show()

```

![Output](Lorentz%20Force.png)

## Simulation Result

In a uniform magnetic field, the charged particle follows a helical path.

The radius of the circular component (Larmor radius) depends on velocity and magnetic field strength:

$$𝑟𝐿=𝑓𝑟𝑎𝑐𝑚𝑣⊥∣𝑞𝐵∣ rL=fracmv ⊥ ∣qB∣$$

The pitch of the helix depends on the component of velocity along the field.

## Applications and Extensions

Adding a constant electric field creates E × B drift, where the particle drifts perpendicular to both fields.

- The simulation can be extended to:

- Non-uniform fields (e.g., magnetic mirrors)

- Multiple particles (plasma dynamics)

- Collisions or interactions (Monte Carlo models)

This simulation provides an intuitive understanding of the Lorentz force, complementing theory with visualization and encouraging deeper exploration.
