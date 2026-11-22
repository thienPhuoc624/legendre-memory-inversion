# legendre-memory-inversion


This repository implements a numerical method for reconstructing unknown initial conditions of **convection–diffusion equations with memory** from noisy final-time observations.

Backward parabolic problems are notoriously ill-posed: even small measurement errors can be dramatically amplified during reconstruction. The presence of a memory term further complicates the problem, as the current state depends on its entire past evolution.

## Key Idea

Our approach combines **Legendre spatial dimensional reduction** with **Tikhonov regularization** to obtain a computationally manageable and noise-resistant reconstruction framework.

**1. Legendre Spatial Dimensional Reduction**

We approximate the unknown solution using a truncated tensor-product Legendre expansion:

$$
u(x,t)\approx \sum_{\mathbf n\preceq\mathbf N}u_{\mathbf n}(t)\Phi_{\mathbf n}(x).
$$

Projecting the governing PDE onto this orthonormal basis transforms the original spatially continuous problem into a **finite-dimensional system of integro-differential equations** for the time-dependent Legendre coefficients.

This reduction offers two major advantages:
- **Computational efficiency:** Replaces the spatial PDE with a finite system of coefficient equations.
- **Implicit noise filtering:** Truncation suppresses high-frequency spatial components, which are particularly susceptible to instability in backward reconstruction.

**2. Tikhonov Regularization**

To stabilize the reduced inverse problem, we solve a regularized least-squares problem:

$$
\min_{U(T)=U_T^\delta}
\left\{
\|\mathcal L_N U\|_{L^2(0,T)}^2
+\varepsilon\|U\|_{H^2(0,T)}^2
\right\}.
$$

Here, $\mathcal L_N$ represents the residual of the reduced integro-differential system, while the $H^2$ penalty controls the temporal regularity of the solution.

The terminal observations are enforced exactly in the reduced coefficient space, while Tikhonov regularization stabilizes the reconstruction and limits noise amplification.

## Numerical Results

The proposed method successfully reconstructs several discontinuous two-dimensional initial profiles, including circular, elliptical, C-shaped, and square-annulus geometries.

**Key findings:**
- Preserves the main geometric features of unknown initial conditions.
- Demonstrates robustness to measurement noise levels of **up to 20%** in the numerical experiments.
- Handles spatially varying coefficients, including cases where the instantaneous diffusion coefficient vanishes.
- Provides a theoretical convergence guarantee for the finite-dimensional Tikhonov reconstruction under suitable regularization conditions.

The combination of **spectral truncation and Tikhonov regularization** is central to achieving stable reconstructions even when the final-time data are substantially corrupted by noise.

## Alternative Approach: Physics-Informed Neural Networks (PINNs)

For readers interested in a neural-network-based approach to the same inverse reconstruction problem, please explore my separate **Physics-Informed Neural Network (PINN) implementation** to compare the reconstruction results with the Legendre–Tikhonov method.

[Explore the PINN implementation](YOUR_PINN_REPOSITORY_URL)
