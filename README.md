---

# **Analysis of Cosmological Robustness with the *Cosmics Tension* Pipeline

## Introduction
The precise determination of cosmological parameters, particularly the Hubble constant (H_0), remains one of the major challenges of modern cosmology. The tensions observed between different measurement methods (Type Ia supernovae, anisotropies of the cosmic microwave background, local Cepheids) raise the question of the robustness of results in the face of methodological choices.
In this work, we develop a comprehensive pipeline, called *Cosmics Tension*, which aims to quantify the stability of cosmological parameters by comparing different covariance matrices from the **Pantheon+SH0ES** dataset.

--

## Methods

### Data
- **Catalog**: 1701 Type Ia supernovae (Pantheon+SH0ES).
- **Observables**: redshift \(z\) and observed distance modulus \(\mu_{\text{obs}}\).
- **Covariances**: statistical matrices only (STATONLY) and complete (STAT+SYS).

### Preprocessing
- Covariance files are provided in flattened form (2893402 rows).
- Reshape into square matrices \(1701 \times 1701\).
- SPD correction (symmetrization + eigenvalue regularization).
- Construction of a blended covariance:
\[
C_{\text{blend}}(\alpha) = \alpha C_{\text{STAT+SYS}} + (1-\alpha) C_{\text{STATONLY}}
\]

### Cosmological model
- Luminosity distance:
\[
d_L(z) = \frac{c}{H_0}(1+z)\int_0^z \frac{dz'}{\sqrt{\Omega_m(1+z')^3 + (1-\Omega_m)}}
\]
- Theoretical distance modulus:
\[
\mu(z) = 5 \log_{10}(d_L(z)) + 25 + M
\]
- Free parameters: \(H_0, \Omega_m, M\).

### Likelihoods
- Two defined log-likelihoods:
- \(\mathcal{L}_{\text{truncated}}\) (corrected full covariance).
- \(\mathcal{L}_{\text{blend}}\) (blended covariance).

### Bayesian Inference
- Metropolis–Hastings (MCMC) algorithm.
- Chains of 6000–8000 steps, with adapted burn-in.
- Statistical summaries: mean, median, credibility intervals.

### Metrics *Cosmics Tension*
Four indicators to compare truncated vs. blended posteriors:
1. **Stability (S)**: deviation of medians in σ units.
2. **Persistence (P)**: overlap fraction of credibility intervals.
3. **Degeneracy (D)**: correlation between parameters.
4. **Robustness (R)**: Weighted combination of S, P, D.

---

## Results

- **Ωₘ**: Robust and stable (R ≈ 0.86–0.90), insensitive to the choice of covariance.
- **H₀ and M**: Fragile (R ≈ 0.1–0.4), highly degenerate (D ≈ 0.99), with marked sensitivity to α.
- Sweep in α (0.6–0.9):
- Ωₘ remains stable.
- H₀ and M show minimal robustness at α=0.7 and a rebound at α=0.8.

Visualizations:
- **R(α) curves**: Ωₘ remains high, H₀/M oscillate.
- Radar chart (α=0.8) : Ωₘ occupies a balanced polygon, H₀/M are squashed.
- Radar grid (α=0.6–0.9) : Clear multidimensional evolution of robustness.

---

## Discussion
These results confirm that:
- The constraint on Ωₘ is robust, independent of the treatment of covariances.
- The tension on H₀ is not a simple numerical artifact: it reflects a structural instability, amplified by degeneracy with the nuisance parameter M.
- The parameter α acts as a robustness indicator: certain values ​​(≈0.8) partially attenuate the instability, but do not eliminate it.

---

## Conclusion
The *Cosmics Tension* pipeline provides a systematic method for evaluating the robustness of cosmological parameters.
- It highlights the stability of Ωₘ and the fragility of H₀/M.
- It demonstrates that the tension on H₀ is intrinsically linked to the choice of covariance and to degeneracy with M.
- The visualizations (curves and radars) provide a powerful educational tool for communicating these results.

👉 This framework can be generalized to other cosmological datasets and serve as a basis for a comparative assessment of current tensions in cosmology.

---
