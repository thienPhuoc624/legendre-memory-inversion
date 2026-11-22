# legendre-memory-inversion




This repository implements a numerical framework for recovering unknown initial conditions of convection–diffusion equations with memory from noisy final-time observations.

The method is based on our research paper:

**[Inverse Initial Data Reconstruction for a Memory Convection–Diffusion Equation via Legendre Spatial Reduction and Tikhonov Regularization](https://arxiv.org/abs/2606.20875)**

*Cong B. Van, Thien P. B. Nguyen, Minh-Binh Tran, and Loc H. Nguyen (2026).*

📄 **Paper:** [arXiv:2606.20875](https://arxiv.org/abs/2606.20875)

## Key Idea

Backward parabolic problems are severely ill-posed: small perturbations in final-time observations can cause significant reconstruction errors.

Our approach combines **Legendre spatial dimensional reduction** and **Tikhonov regularization** to address this instability.

### 1. Legendre Spatial Reduction

We approximate the solution using a truncated tensor-product Legendre expansion:

$$
u(x,t)\approx\sum_{\mathbf n\preceq\mathbf N}
u_{\mathbf n}(t)\Phi_{\mathbf n}(x).
$$

This transforms the original PDE into a **finite-dimensional system of integro-differential equations**, providing:

- **Dimensional reduction:** A computationally manageable system of time-dependent coefficients.
- **Spectral filtering:** Suppression of high-frequency components responsible for severe noise amplification.

### 2. Tikhonov Regularization

We solve the reduced inverse problem through regularized least squares:

$$
\min_{U(T)=U_T^\delta}
\left\{
\|\mathcal L_N U\|_{L^2(0,T)}^2
+\varepsilon\|U\|_{H^2(0,T)}^2
\right\}.
$$

The $H^2$ penalty stabilizes reconstruction while preserving the prescribed terminal coefficients. For a fixed Legendre truncation order, the paper establishes convergence to the finite-dimensional minimum-norm solution under suitable regularization conditions.

## Numerical Results

Our two-dimensional experiments demonstrate:

- **Noise robustness:** Successful reconstruction with up to **20% measurement noise**.
- **Geometric accuracy:** Recovery of circular, elliptical, C-shaped, and square-annulus initial profiles.
- **Flexibility:** Applicability to spatially varying coefficients, including vanishing instantaneous diffusion coefficients.

The combined filtering effect of Legendre truncation and Tikhonov regularization enables stable recovery of the principal geometric features even from substantially corrupted observations.

## Alternative Approach: Physics-Informed Neural Networks (PINNs)

Interested in a neural-network-based solution? Explore my separate **Physics-Informed Neural Network (PINN) implementation** of this inverse problem to compare reconstruction results with the Legendre–Tikhonov approach.

[Explore the PINN implementation](YOUR_PINN_REPOSITORY_URL)
