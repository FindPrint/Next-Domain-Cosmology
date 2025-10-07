# 🌌 Next-Domain-Cosmology
**FR :** Application de l’équation expérimentale **Cosmic Tension** aux données cosmologiques (Pantheon+ Supernovae Ia) pour explorer la *Hubble tension*.  
**EN :** Applying the experimental **Cosmic Tension** equation to cosmological data (Pantheon+ Type Ia Supernovae) to explore the *Hubble tension*.

---

## 📑 Contexte / Background
**FR :**  
La *Hubble tension* est l’un des problèmes majeurs de la cosmologie moderne : les mesures locales de la constante de Hubble (H₀) diffèrent de celles issues du fond diffus cosmologique (Planck).  
Ce projet explore si l’équation **Cosmic Tension**, déjà testée sur les domaines épidémiques, financiers et climatiques, peut apporter un éclairage nouveau sur les données de supernovae Ia (Pantheon+).

**EN :**  
The *Hubble tension* is one of the major problems in modern cosmology: local measurements of the Hubble constant (H₀) differ from those inferred from the cosmic microwave background (Planck).  
This project explores whether the **Cosmic Tension** equation, already tested on epidemic, financial, and climate domains, can provide new insights on Type Ia supernovae data (Pantheon+).

---

## 🧪 Hypothèse de base / Initial Hypothesis
**FR :**  
L’équation Cosmic Tension, en intégrant une dynamique logarithmique et linéaire, pourrait mieux capturer les régularités non-linéaires de la relation distance–redshift que les modèles statistiques classiques (ARIMA).  

**EN :**  
The Cosmic Tension equation, by combining logarithmic and linear dynamics, may better capture the non-linear regularities of the distance–redshift relation than classical statistical models (ARIMA).

---

## 🔬 Processus entrepris / Process Undertaken
1. **Chargement des données** : Pantheon+ (1048 supernovae Ia, z ≈ 0–1.2).  
2. **Nettoyage et normalisation** : redshift (`zCMB`) et distance modulus (`μ`) mis à l’échelle [0,1].  
3. **Découpage en blocs** : redshift divisé en intervalles (0–0.3, 0.3–0.6, 0.6–0.9, etc.).  
4. **Comparaison ARIMA vs Cosmic Tension** :  
   - ARIMA appliqué sur la série `μ`.  
   - Cosmic Tension calibré automatiquement par `curve_fit` :  
     

\[
     \mu(z) = \alpha \cdot \log(1+z) + \beta \cdot z + \gamma
     \]

  
5. **Évaluation** : RMSE calculé bloc par bloc, vainqueur identifié.  
6. **Visualisation** : tracés `z vs μ` avec observations, ARIMA et Cosmic Tension superposés.  

---

## 📊 Résultats / Results

### Résultats par bloc
| Block             | N   | RMSE_ARIMA | RMSE_Cosmic | Winner          |
|-------------------|-----|------------|-------------|-----------------|
| z ∈ [0.00, 0.30]  | 914 | 0.0123     | 0.0382      | ARIMA           |
| z ∈ [0.30, 0.59]  | 125 | 0.0699     | 0.0117      | Cosmic Tension  |

### Résumé global
| Global RMSE_ARIMA | Global RMSE_Cosmic | Global Winner   |
|-------------------|--------------------|-----------------|
| 0.0411            | 0.0250             | Cosmic Tension  |

---

## 📈 Visualisations / Visualizations
Exemple de figure (bloc 0) :  

![Cosmo Block 0](figures_cosmology/Cosmo_Block0.png)

Exemple de figure (bloc 1) :  

![Cosmo Block 1](figures_cosmology/Cosmo_Block1.png)

*(Toutes les figures sont disponibles dans le dossier `figures_cosmology/`.)*

---

## 🧾 Conclusion / Conclusion

**FR :**  
Les résultats montrent que Cosmic Tension n’est pas universellement supérieur à ARIMA : aux bas redshifts, ARIMA reste compétitif.  
Cependant, dès que l’on monte en redshift, Cosmic Tension surpasse ARIMA et devient globalement meilleur sur l’ensemble du dataset Pantheon+.  
Ce résultat suggère que Cosmic Tension capte des régularités non-linéaires pertinentes pour la compréhension de la *Hubble tension*.  

**EN :**  
The results show that Cosmic Tension is not universally superior to ARIMA: at low redshifts, ARIMA remains competitive.  
However, as redshift increases, Cosmic Tension outperforms ARIMA and is globally better across the Pantheon+ dataset.  
This result suggests that Cosmic Tension captures non-linear regularities relevant to understanding the *Hubble tension*.  

---

## 🔮 Perspectives / Next Steps
- Étendre l’analyse à d’autres datasets cosmologiques :  
  - **BAO (Baryon Acoustic Oscillations)**  
  - **CMB (Planck)**  
- Comparer Cosmic Tension non seulement à ARIMA, mais aussi aux modèles cosmologiques standards (ΛCDM, wCDM).  
- Publier une note de synthèse et inviter la communauté scientifique à tester et critiquer l’approche.  

---

## 📚 Sources
- Pantheon+ dataset : [Scolnic et al. (2018)](https://github.com/dscolnic/Pantheon)  
- Discussions sur la Hubble tension : [Frontiers in Astronomy and Space Sciences (2022)](https://www.frontiersin.org/journals/astronomy-and-space-sciences/articles/10.3389/fspas.2022.1014433/full)  

---
