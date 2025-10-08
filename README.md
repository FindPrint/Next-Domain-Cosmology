---

# **Cosmological Robustness Analysis with the *Cosmics Tension* Pipeline**

## Introduction
The precise determination of cosmological parameters, in particular the Hubble constant $$H_0$$, remains one of the major challenges of modern cosmology. The tensions observed between different measurement methods (Type Ia supernovae, cosmic microwave background anisotropies, local Cepheids) raise the question of the robustness of results with respect to methodological choices.  
In this work, we develop a complete pipeline, called *Cosmics Tension*, which aims to quantify the stability of cosmological parameters by comparing different covariance matrices from the **Pantheon+SH0ES** dataset.

---

## Methods

### Data
- **Catalog**: 1701 Type Ia supernovae (Pantheon+SH0ES).  
- **Observables**: redshift $$z$$ and observed distance modulus $$\mu_{\text{obs}}$$.  
- **Covariances**: statistical‑only matrices (STATONLY) and full matrices (STAT+SYS).

### Preprocessing
- Covariance files are provided in flattened form (2,893,402 lines).  
- Reshaped into square matrices $$1701 \times 1701$$.  
- SPD correction (symmetrization + eigenvalue regularization).  
- Construction of a blended covariance:  

$$
C_{\text{blend}}(\alpha) = \alpha \, C_{\text{STAT+SYS}} + (1-\alpha) \, C_{\text{STATONLY}}
$$

### Cosmological Model
- Luminosity distance:  

$$
d_L(z) = \frac{c}{H_0}(1+z) \int_0^z \frac{dz'}{\sqrt{\Omega_m(1+z')^3 + (1-\Omega_m)}}
$$

- Theoretical distance modulus:  

$$
\mu(z) = 5 \, \log_{10}(d_L(z)) + 25 + M
$$

- Free parameters: $$H_0, \; \Omega_m, \; M$$.

### Likelihoods
- Two log‑likelihoods defined:  
  - $$\mathcal{L}_{\text{truncated}}$$ (full corrected covariance).  
  - $$\mathcal{L}_{\text{blend}}$$ (blended covariance).

### Bayesian Inference
- Metropolis–Hastings MCMC algorithm.  
- Chains of 6000–8000 steps, with appropriate burn‑in.  
- Statistical summaries: mean, median, credible intervals.

### *Cosmics Tension* Metrics
Four indicators to compare truncated vs blended posteriors:
1. **Stability (S)**: median shift in units of σ.  
2. **Persistence (P)**: fraction of overlap between credible intervals.  
3. **Degeneracy (D)**: correlation between parameters.  
4. **Robustness (R)**: weighted combination of S, P, D.

---

## Results

- **Ωₘ**: robust and stable (R ≈ 0.86–0.90), insensitive to covariance choice.  
- **H₀ and M**: fragile (R ≈ 0.1–0.4), strongly degenerate (D ≈ 0.99), with marked sensitivity to α.  
- α‑scan (0.6–0.9):  
  - Ωₘ remains stable.  
  - H₀ and M show a robustness minimum at α=0.7 and a rebound at α=0.8.  

Visualizations:
- **R(α) curves**: Ωₘ remains high, H₀/M oscillate.  
- **Radar chart (α=0.8)**: Ωₘ forms a balanced polygon, H₀/M collapse.  
- **Radar grid (α=0.6–0.9)**: clear multidimensional evolution of robustness.

---

## Discussion
These results confirm that:
- The constraint on Ωₘ is robust, independent of covariance treatment.  
- The H₀ tension is not a numerical artifact: it reflects a structural instability, amplified by degeneracy with the nuisance parameter M.  
- The parameter α acts as a robustness probe: certain values (≈0.8) partially mitigate instability, but do not eliminate it.

---

## Conclusion
The *Cosmics Tension* pipeline provides a systematic method to evaluate the robustness of cosmological parameters.  
- It highlights the stability of Ωₘ and the fragility of H₀/M.  
- It demonstrates that the H₀ tension is intrinsically linked to covariance choice and degeneracy with M.  
- The visualizations (curves and radars) offer a powerful pedagogical tool to communicate these results.  

👉 This framework can be generalized to other cosmological datasets and serve as a basis for comparative evaluation of current tensions in cosmology.

---


Would you like me to also prepare a **shortened “executive summary” version** (5–6 sentences, no equations) that you can put at the very top of your README as a quick overview?
