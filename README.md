# Meta-Cognition Approaches
### Mathematical Representations of Human Self-Awareness

A research project developing a **novel mathematical formalization of human self-awareness**  
as a preprint publication, grounded in psychology research from UW–Madison.

---

## Core Idea

Self-awareness is modeled as a **contractive Bayesian operator T_SA** on the space of  
self-belief distributions. The unique fixed point of T_SA is the *self-model* — the  
agent's true internal type. The rate of contraction is the **SA measure**, directly  
interpretable in terms of Davidson's empirical six-dimension emotional style framework.

---

## Repository Structure

```
meta-cognition-approaches/
│
├── framework.md                      ← 7-approach theoretical overview
│                                       (IIT, Free Energy, Dynamical Systems,
│                                        HOT, Category Theory, LLMs, Game Theory)
│
├── formulations/
│   └── fixed_point_theory.md         ← Precise definitions and theorems
│                                       for the T_SA operator approach
│
├── experiments/
│   ├── sa_operator.py                ← Core T_SA implementation (NumPy)
│   ├── exp01_convergence.py          ← Experiment 1: fixed-point convergence
│   ├── exp02_sa_measure.py           ← Experiment 2: SA measure vs noise
│   └── exp03_davidson_mapping.py     ← Experiment 3: Davidson dimensions
│
├── results/                          ← Generated plots (after running experiments)
│
└── requirements.txt
```

---

## UW–Madison Research Anchors

| Researcher | Lab | Relevance |
|---|---|---|
| **Giulio Tononi** | Center for Sleep and Consciousness (Psychiatry) | Integrated Information Theory (IIT) — Φ as consciousness measure |
| **Richard Davidson** | Center for Healthy Minds (Psychology) | Six dimensions of emotional style — empirical SA ground truth |

Davidson's **self-awareness dimension** (measured via insula fMRI activation and self-report accuracy)  
is the primary empirical target. The T_SA operator's KL-based SA measure is designed to  
correlate with and explain this dimension mathematically.

---

## The T_SA Operator (Key Formulation)

Given:
- **Θ** = finite set of self-types (emotional/behavioral profiles)
- **L ∈ ℝ^{m×n}** = likelihood model: `L[k,j] = P(obs=k | type=θ_j)`, strictly positive
- **q ∈ Δ^n** = current self-belief distribution

The operator for observation `k` is:

```
T_SA^k(q)_j = L[k,j] · q_j / Σ_i L[k,i] · q_i    (Bayesian posterior update)
```

**Main result (Theorem 4.2):** Under i.i.d. observations from the true type θ*,  
iterating T_SA converges to δ_{θ*} (point mass on the true self-model) almost surely.  
The rate is controlled by the **SA measure**:

```
SA(system) = min_{j ≠ θ*} D_KL( P(obs | θ*) || P(obs | θ_j) )
```

High SA → observations sharply discriminate the true type → fast convergence.

---

## Quick Start

```bash
pip install -r requirements.txt

# Run experiments (each saves a plot to results/)
python experiments/exp01_convergence.py
python experiments/exp02_sa_measure.py
python experiments/exp03_davidson_mapping.py
```

### What each experiment shows

| Script | Question | Key finding |
|---|---|---|
| `exp01_convergence.py` | Does T_SA converge? How fast? | Exponential convergence; rate scales with SA level |
| `exp02_sa_measure.py` | How does SA measure vary with likelihood sharpness? | Monotone increase; KL and Birkhoff measures agree; bifurcation at noise = 1/n_types |
| `exp03_davidson_mapping.py` | How do Davidson's six dimensions map onto T_SA? | D1→SA_KL, D2→resilience, D3→effective rank; synthetic subjects show predicted correlations |

---

## Seven Theoretical Approaches (framework.md)

The `framework.md` file surveys seven distinct mathematical approaches to self-awareness,  
from physical substrate to abstract structure:

```
LEVEL 5 (Abstract)      Category Theory        ← structural constraints
LEVEL 4 (Logical)       HOT / Modal Logic      ← what representations exist
LEVEL 3 (Computational) Free Energy / IIT      ← how representations are computed
LEVEL 2 (Strategic)     Game Theory            ← why the self is stable
LEVEL 1 (Physical)      Dynamical Systems      ← substrate realization
LEVEL 0.5 (Synthetic)   LLM Framework          ← empirically testable bridge
LEVEL 0 (Empirical)     Davidson / Tononi data ← ground truth
```

The T_SA fixed-point theory (this repo's core contribution) lives at Level 3  
and formally connects Level 4 (fixed points = HOT meta-depth) and Level 2  
(Nash equilibrium = fixed point of best-response).

---

## Roadmap

- [x] Seven-approach theoretical framework (`framework.md`)
- [x] Precise mathematical formulations (`formulations/fixed_point_theory.md`)
- [x] Core operator implementation (`experiments/sa_operator.py`)
- [x] Experiment 1: convergence
- [x] Experiment 2: SA measure
- [x] Experiment 3: Davidson mapping
- [ ] Experiment 4: Higher-order T_SA^{(k)} and meta-depth
- [ ] Experiment 5: Continuous type space (Wasserstein metric)
- [ ] Experiment 6: Coupled self-game (Game Theory × T_SA)
- [ ] Preprint draft

---

## References

- Tononi, G. — [IIT 3.0, PLOS Computational Biology (2014)](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003588)
- [Center for Sleep and Consciousness, UW–Madison](https://centerforsleepandconsciousness.psychiatry.wisc.edu/integrated-information-theory/)
- Davidson, R.J. — [Center for Healthy Minds, UW–Madison](https://centerhealthyminds.org/about/founder-richard-davidson)
- Birkhoff, G. — *Lattice Theory* (1967) — contraction theorem for positive maps
- Rosenthal, D. — [Higher-Order Theories of Consciousness](https://davidrosenthal.org/DR-HO-Theories-Handbook.pdf)
- Friston, K. — Free Energy Principle (Nature Reviews Neuroscience, 2010)
- [Epistemic Foundations of Game Theory, Stanford Encyclopedia](https://plato.stanford.edu/entries/epistemic-game/)
