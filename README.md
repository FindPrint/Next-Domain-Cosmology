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







Here’s the full **English version** of your structured summary, with all equations written in **GitHub‑friendly math syntax** (`$$ ... $$` blocks). You can paste this directly into your README or documentation without equations breaking.

---

# 🚀 Global Summary of Work Performed

## 1. 📥 Data Loading and Preparation
- **Download of Pantheon+SH0ES files** from the official repository (catalog `.dat` and covariance matrices `.cov`).  
- **Reading SNe Ia data**:  
  - 1701 supernovae, with redshift `zHD` and observed distance modulus `MU_SH0ES`.  
- **Initial issue**: covariance files are provided in flattened form (2,893,402 lines).  
  - **Solution**: skip the first header line, then reshape into square matrices 1701×1701.

---

## 2. 🧮 Covariance Matrix Preparation
- **SPD correction**: symmetrization + eigenvalue regularization to ensure positive definiteness.  
- **Construction of a blended covariance**:  

$$
C_{\text{blend}} = \alpha \, C_{\text{corrected full}} + (1-\alpha)\, C_{\text{stat}}
$$

with $$\alpha = 0.8$$ (and later scanning multiple values of α).  
- Verification: minimum eigenvalues > 0 → matrices are well‑conditioned.

---

## 3. 🌌 Cosmological Model
- Definition of the luminosity distance model:  
  - Friedmann–Lemaître integral:  

$$
d_L(z) = \frac{c}{H_0}(1+z)\int_0^z \frac{dz'}{\sqrt{\Omega_m(1+z')^3 + (1-\Omega_m)}}
$$

  - Theoretical distance modulus:  

$$
\mu(z) = 5 \log_{10}(d_L(z)) + 25 + M
$$

- Free parameters: **H₀, Ωₘ, M**.

---

## 4. 📊 Likelihoods
- Two log‑likelihoods defined:  
  - `lnlike_tronque` → full corrected covariance.  
  - `lnlike_blend` → blended covariance.  
- Pre‑computations: covariance inverses and determinants to speed up evaluations.

---

## 5. 🔁 MCMC (Metropolis)
- Implementation of a simple but optimized MCMC (vectorized proposals).  
- Two chains launched:  
  - Truncated: 6000 steps (burn‑in 1000).  
  - Blend: 8000 steps (burn‑in 2000).  
- Results: posterior distributions of H₀, Ωₘ, M.  
- Verification: correct acceptance rates, statistical summaries (mean, median, intervals).

---

## 6. 📐 *Cosmics Tension* Metrics
Definition of four indicators to compare truncated vs blended runs:
- **Stability (S)**: median shift in units of σ.  
- **Persistence (P)**: fraction of overlap between credible intervals.  
- **Degeneracy (D)**: correlation between parameters (e.g. H₀–M).  
- **Robustness (R)**: global score combining S, P, D.

Typical results:
- **Ωₘ** → robust (R ≈ 0.86–0.90).  
- **H₀ and M** → fragile (R ≈ 0.1–0.4), highly degenerate with each other.

---

## 7. 🔄 α‑Scanning
- Loop over α = 0.6, 0.7, 0.8, 0.9.  
- For each α: recompute `C_blend`, run a fast MCMC, compute metrics.  
- Build a comparative table of R scores.

Observation:  
- Ωₘ remains stable and robust.  
- H₀ and M vary strongly with α, with a robustness peak around α=0.8.

---

## 8. 📈 Visualizations
- **R(α) curves**: robustness evolution for H₀, Ωₘ, M.  
- **Radar chart (α=0.8)**: direct comparison of the four metrics (S, P, D, R) for each parameter.  
- **Radar grid (α=0.6, 0.7, 0.8, 0.9)**: multidimensional visualization of robustness evolution.

---

# ✨ Conclusion

A **complete and reproducible pipeline** has been built that:  
1. Loads and corrects Pantheon+SH0ES data.  
2. Defines a simple cosmological model (H₀, Ωₘ, M).  
3. Compares two covariance frameworks (truncated vs blend).  
4. Explores parameter stability via MCMC.  
5. Quantifies robustness with the *Cosmics Tension* metrics.  
6. Visualizes results with tables, curves, and radar plots.  

👉 In short: this demonstrates that **Ωₘ is robust**, while **H₀ and M are unstable and degenerate**, and that this fragility depends on the weight α assigned to the systematic covariance.

--- 




---

# 🌌 Understanding Cosmological Robustness with *Cosmics Tension*

## 1. The Starting Problem
In cosmology, we try to measure fundamental numbers that describe the Universe.  
Two of the most important are:
- **H₀**: the rate at which the Universe is expanding today (the famous “Hubble constant”).  
- **Ωₘ**: the proportion of matter in the Universe.  

The issue is that different methods give results that don’t agree, especially for H₀. This is known as the **Hubble tension**.  

---

## 2. The Data Used
We rely on a large catalog of Type Ia supernovae (Pantheon+SH0ES).  
- These exploding stars serve as **cosmic beacons**: by measuring their brightness and distance, we can reconstruct the history of the Universe’s expansion.  
- The data come with covariance matrices, which describe uncertainties and correlations between measurements.  

---

## 3. The Idea of the *Cosmics Tension* Pipeline
We want to test **how robust the results are** when we change how uncertainties are treated.  
- We compare two approaches:  
  - **Full covariance** (stricter, includes all sources of error).  
  - **Statistical‑only covariance** (simpler, excludes systematics).  
- We also mix the two with a parameter $$\alpha$$ (for example, 80% full covariance + 20% statistical).  

---

## 4. How It Works
1. Define a simple model of the Universe (based on H₀, Ωₘ, and a calibration parameter M).  
2. Fit this model to the data using a sampling method (MCMC) that explores all possible values.  
3. Compare the results obtained with the different covariances.  

---

## 5. The Four Indicators
To measure robustness, we designed four easy‑to‑understand metrics:  
- **Stability (S)**: does the value change a lot when covariance changes?  
- **Persistence (P)**: do the confidence intervals overlap well?  
- **Degeneracy (D)**: are two parameters too tightly linked (e.g. H₀ and M moving together)?  
- **Robustness (R)**: a global score combining the three above.  

---

## 6. What We Find
- **Ωₘ (matter)**: very robust. No matter the covariance, the result stays stable and reliable.  
- **H₀ (expansion)** and **M (calibration)**: fragile.  
  - They change significantly depending on covariance.  
  - They are almost perfectly correlated → hard to separate.  
  - Their robustness is low (R ≈ 0.1–0.4).  
- When varying $$\alpha$$:  
  - Ωₘ remains solid.  
  - H₀ and M show a dip in robustness at $$\alpha = 0.7$$ and a rebound at $$\alpha = 0.8$$.  

---

## 7. Visualizations
- **R(α) curves**: show Ωₘ stays high, while H₀ and M oscillate.  
- **Radar charts**: make it clear at a glance that Ωₘ is balanced, while H₀ and M are “flattened” by their instability.  

---

## 8. Conclusion
- The *Cosmics Tension* pipeline is a **toolbox** for testing the solidity of cosmological results.  
- It shows that:  
  - The matter fraction (Ωₘ) is well measured and robust.  
  - The Hubble constant (H₀) is fragile, dependent on error treatment, and strongly tied to M.  
- The H₀ tension is therefore not a simple bug: it is a real structural instability.  

---

✨ In summary: this work makes visible what many suspected — **some cosmological parameters are solid, others are fragile**, and it is important to state this clearly in order to move forward.  

--- 





---

# 🚀 Concrete Solution Pathways with *Cosmics Tension*

The *Cosmics Tension* pipeline does not stop at observing that some cosmological parameters (such as $$H_0$$) are fragile and unstable. Its goal is to provide **practical tools and concrete solutions** to improve the reliability of analyses and guide future research. Here are the main pathways this work proposes:

---

## 1. **Mapping Parameter Robustness**
Instead of publishing a single value of $$H_0$$ or $$\Omega_m$$, the pipeline provides a **robustness score (R)** for each parameter.  
- This acts as a **confidence label**: researchers can immediately see whether a result is solid (like $$\Omega_m$$) or fragile (like $$H_0$$).  
- This approach avoids presenting isolated numbers without context and allows parameters to be ranked according to their stability.

---

## 2. **Identifying Confidence Zones**
By scanning the parameter $$\alpha$$ (the weight assigned to systematic covariances), we can:  
- Determine the **robustness ranges** where results remain stable despite methodological choices.  
- Recommend **trustworthy intervals** rather than a single potentially misleading number.  
- For example: “$$\Omega_m$$ remains robust for all $$\alpha$$, but $$H_0$$ is only interpretable around $$\alpha \approx 0.8$$.”

---

## 3. **Reducing Degeneracies**
The pipeline highlights the strong correlation between $$H_0$$ and the calibration parameter $$M$$.  
- **Solution**: combine Pantheon+ with other independent probes (BAO, CMB, gravitational lensing) to break this degeneracy.  
- The pipeline can serve as a **testing bench**: add a new dataset and measure whether the robustness of $$H_0$$ improves.

---

## 4. **Guiding Research Efforts**
By showing which parameters are robust and which are fragile, *Cosmics Tension* helps to:  
- **Avoid wasting time** refining parameters that are already stable (like $$\Omega_m$$).  
- **Focus efforts** on problematic zones (H₀/M), where new methods or data are needed.  
- **Prioritize resources**: for example, invest in local probes to better constrain $$M$$, or in multi‑probe analyses to stabilize $$H_0$$.

---

## 5. **A Common Language for the Community**
The four metrics (S, P, D, R) provide a simple and universal vocabulary for discussing robustness:  
- **S** = stability of medians.  
- **P** = persistence of intervals.  
- **D** = degeneracy between parameters.  
- **R** = overall robustness.  

This language can be adopted by the community to compare results across teams, datasets, or methods. It facilitates **transparency** and **comparability**.

---

## 6. **Educational and Communication Tool**
Visualizations (R(α) curves, radar charts) make robustness **visible and intuitive**.  
- For researchers: a quick diagnostic of result solidity.  
- For the public: a clear way to understand why some numbers are reliable and others are not.  
- For scientific decision‑makers: a tool to guide where to invest effort.

---

# ✨ Conclusion
The *Cosmics Tension* pipeline does more than confirm that some parameters are fragile.  
It provides an **operational framework** to:  
- measure robustness,  
- identify confidence zones,  
- reduce degeneracies,  
- guide research priorities,  
- and supply a common language for the community.  

In this sense, it transforms an “open wound” (the H₀ tension) into a **constructive opportunity**: to better understand our uncertainties, better communicate our results, and better target the next steps of cosmological research.

--- 

