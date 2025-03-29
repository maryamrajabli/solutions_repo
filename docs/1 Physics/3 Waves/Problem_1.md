# Problem 1

# Interference Patterns from Multiple Wave Sources

## Motivation

When multiple wave sources interact, the resulting pattern reveals the rich behavior of **wave interference**. This phenomenon is central to understanding light, sound, and even quantum behavior. By studying how waves from different sources superimpose on a water surface, we explore **constructive** and **destructive interference**, which form beautiful and physically meaningful patterns.

This simulation offers a hands-on way to **visualize** and **understand** the effects of phase relationships and spatial arrangement on interference, laying a foundation for real-world applications like **antenna design**, **acoustics**, and **optics**.

---

## Objective

- Analyze interference from **coherent wave sources** placed at the vertices of a **regular polygon** (e.g., square).
- Apply the **principle of superposition** to calculate total displacement at any point.
- Use simulation to **visualize regions** of constructive and destructive interference.
- Understand the influence of **geometric symmetry** on wave interaction.

---

## Theoretical Foundation

### Circular Wave Equation

A circular wave from a single point source is modeled as:

$$
y(x, y, t) = A \sin(kr - \omega t + \phi)
$$

Where:

- $A$: amplitude
- $r=\sqrt{(x - x_0)^2 + (y - y_0)^2}$: distance from the source
- $k =\frac{2\pi}{\lambda}$: wave number
- $\omega = 2\pi f$: angular frequency
- $\phi$: initial phase

---

### Superposition of Multiple Sources

For $N$ coherent sources:

$$
y_{\text{total}}(x, y, t) = \sum_{i=1}^{N} A \sin(k r_i - \omega t)
$$

This produces **interference patterns** where wave crests align (constructive) or cancel (destructive).

---

### Constructive & Destructive Interference

- **Constructive**: $\Delta r = m \lambda$ (waves in phase)
- **Destructive**: $\Delta r = (m + 0.5)\lambda$ (waves out of phase)
- These lead to alternating regions of high and low displacement.

---

### Polygonal Source Arrangement

Using a **square configuration** ensures symmetry, helping us observe consistent interference patterns. The geometry influences **how and where** constructive and destructive interference occurs.

---

## Python Simulation: Square Configuration

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
A = 1.0
λ = 1.0
f = 1.0
k = 2 * np.pi / λ
ω = 2 * np.pi * f
φ = 0
t = 0

x = np.linspace(-5, 5, 500)
y = np.linspace(-5, 5, 500)
X, Y = np.meshgrid(x, y)

# Square vertices
R = 2
num_sources = 4
angles = np.linspace(0, 2 * np.pi, num_sources, endpoint=False)
sources = [(R * np.cos(a), R * np.sin(a)) for a in angles]

Z = np.zeros_like(X)
for (sx, sy) in sources:
    r = np.sqrt((X - sx)**2 + (Y - sy)**2)
    Z += A * np.sin(k * r - ω * t + φ)

plt.figure(figsize=(8, 6))
plt.contourf(X, Y, Z, levels=100, cmap='viridis')
plt.colorbar(label='Displacement')
plt.title('Wave Interference Pattern (Square Sources)')
plt.xlabel('x')
plt.ylabel('y')
plt.axis('equal')
plt.tight_layout()
plt.show()

```

![Output](Wave%20interference.png)
