# Quantum Tunneling Simulation

A comprehensive computational physics simulation of quantum tunneling phenomena using Python and CuPy.

## Video Demonstration

![Demo](quantum_tunneling (3).gif)

## Overview

This project simulates quantum particles tunneling through a potential barrier using the time-dependent Schrödinger equation. It visualizes the quantum tunneling effect, demonstrating how particles can penetrate barriers that would be impossible according to classical physics.

## Components and Mathematical Formulation

### 1. Time-Dependent Schrödinger Equation

The simulation solves the time-dependent Schrödinger equation:

$$i\hbar\frac{\partial\psi(x,t)}{\partial t} = -\frac{\hbar^2}{2m}\frac{\partial^2\psi(x,t)}{\partial x^2} + V(x)\psi(x,t)$$

Where:
- $\psi(x,t)$ is the wave function
- $\hbar$ is the reduced Planck constant
- $m$ is the mass of the particle (electron in this case)
- $V(x)$ is the potential energy function

### 2. Potential Barrier Function

The model uses a rectangular potential barrier defined as:

$$V(x) = 
\begin{cases}
V_0, & \text{if } |x| \leq L/2 \\
0, & \text{otherwise}
\end{cases}$$

Where:
- $V_0$ is the height of the barrier (in eV)
- $L$ is the width of the barrier (in nm)

### 3. Transmission and Reflection Coefficients

For a particle with energy $E$, the transmission ($T$) and reflection ($R$) coefficients are calculated using the quantum mechanical formulas:

#### For $E > V_0$ (above barrier):
$$k_1 = \frac{\sqrt{2mE}}{\hbar}, \quad k_2 = \frac{\sqrt{2m(E-V_0)}}{\hbar}$$

$$r = \frac{i(k_1^2 + k_2^2)\sin(k_2L)}{(k_1^2 + k_2^2)\sin(k_2L) + 2ik_1k_2\cos(k_2L)}$$

$$t = \frac{2ik_1k_2}{(k_1^2 + k_2^2)\sin(k_2L) + 2ik_1k_2\cos(k_2L)}$$

#### For $E < V_0$ (tunneling regime):
$$k_1 = \frac{\sqrt{2mE}}{\hbar}, \quad k_2 = \frac{\sqrt{2m(V_0-E)}}{\hbar}$$

$$r = \frac{i(k_1^2 + k_2^2)\sinh(k_2L)}{(k_1^2 - k_2^2)\sinh(k_2L) + 2ik_1k_2\cosh(k_2L)}$$

$$t = \frac{2ik_1k_2}{(k_1^2 - k_2^2)\sinh(k_2L) + 2ik_1k_2\cosh(k_2L)}$$

The transmission and reflection probabilities are calculated as:
$$T = |t|^2, \quad R = |r|^2$$

With the property that $T + R = 1$ (conservation of probability).

### 4. Wave Packet Initialization

The simulation initializes a Gaussian wave packet:

$$\psi(x,0) = \frac{1}{\sqrt[4]{2\pi\sigma^2}}\exp\left(-\frac{(x-x_0)^2}{4\sigma^2} + ik_0(x-x_0)\right)$$

Where:
- $x_0$ is the initial position
- $\sigma$ is the width of the wave packet
- $k_0 = \sqrt{2mE}/\hbar$ is the wave number

### 5. Time Evolution

The wave function evolves in time according to:

$$\psi(x, t + \Delta t) = e^{-i\hat{H}\Delta t/\hbar}\psi(x,t)$$

This is implemented numerically using the split-operator method with fast Fourier transforms.

### 6. Hardware Acceleration

The simulation uses CuPy for GPU acceleration, offering significant performance improvements over standard NumPy for this computationally intensive task.

## Core Implementation Classes

### 1. `QuantumTunnelingSimulator`

The main class that handles:
- Wave packet initialization
- Hamiltonian construction
- Time evolution of the wave function
- Calculation of transmission and reflection coefficients

### 2. Visualization

The visualization includes:
- Real-time plotting of the wave function
- Color-coded phase information
- Potential barrier representation
- Transmission and reflection probability indicators

## Parameters

The simulation allows customization of:
- Particle energy (E) in eV
- Barrier height (V₀) in eV
- Barrier width (L) in nm
- Wave packet width (σ)
- Initial position of the wave packet
- Simulation resolution and duration

## Physics Insights

This simulation demonstrates key quantum phenomena:
- Tunneling through classically forbidden regions
- Wave-particle duality
- Probability interpretation of quantum mechanics
- Phase information in quantum systems

## Running the Simulation

To run the simulation, execute the Jupyter notebook. The key parameters are:
- `E` = 0.3 eV (Energy of the particle)
- `V0` = 0.3434 eV (Barrier height)
- `L` = 1.0 nm (Barrier width)
- `initial_position` = -5 nm
- `wave_width` = 1e-9 m (wave packet width)

The output is a video visualization of the quantum tunneling process. 
