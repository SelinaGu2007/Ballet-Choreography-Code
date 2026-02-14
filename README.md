# Route Planning and Optimization of Ballet Choreography

## Overview
This project studies ballet choreography through the lens of **combinatorial optimization** and **computational movement analysis**.  
We model a dancer’s spatial trajectory as a sequence of stage coordinates and investigate how closely real choreography aligns with the **minimum‑displacement traversal** predicted by routing algorithms.

Using pose‑tracking data extracted from video, we construct spatial keypoints and formulate the choreography ordering problem as a **metric Traveling Salesperson Problem (TSP)**. We compare:

- The original choreography traversal (time order)
- A polynomial‑time approximation (Christofides algorithm)
- The exact optimal traversal (Held–Karp dynamic programming)

This framework provides a quantitative method to evaluate the relationship between **artistic choreography design** and **geometric movement efficiency**.

---

## Mathematical Formulation

Let

$$
P = \{p_1, p_2, \dots, p_n\}
$$

be sampled stage positions in the $XZ$‑plane derived from pose tracking.  
Define a complete weighted graph

$$
G=(V,E), \quad w(i,j)=\|p_i-p_j\|_2
$$

The choreography traversal corresponds to an ordered cycle through all nodes.  
The optimization objective is

$$
\min_{\pi} \sum_{k=1}^{n} w(\pi_k, \pi_{k+1}),
$$

which is the classical **metric TSP**.

---

## Algorithms Implemented

### Held–Karp (Exact)
Dynamic programming solution producing the **optimal tour** for small datasets  
($O(n^2 2^n)$), used as the evaluation baseline.

### Christofides Algorithm
Polynomial‑time approximation with theoretical guarantee:

$$
L_{\text{Christofides}} \le 1.5\,L_{\text{optimal}}.
$$

In experiments, the approximation gap is typically much smaller.

---

## Data Pipeline

The repository contains a fully reproducible pipeline:

```
video
  → pose tracking (MediaPipe PoseLandmarker)
  → coordinate extraction
  → outlier removal (IQR filter)
  → trajectory subsampling (keypoints)
  → optimization analysis (TSP)
  → comparison results and plots
```

Key scripts:

```
scripts/extract_head_coords.py
scripts/clean_coords.py
scripts/make_keypoints.py
scripts/run_experiments.py
scripts/plot_results.py
```

---

## Experiments

Three choreography phrases were processed from video recordings.  
For each phrase:

- head trajectory was tracked using MediaPipe PoseLandmarker
- spatial keypoints were sampled from the cleaned trajectory
- the original traversal, Christofides tour, and exact optimal tour were computed

---

## Results

Across all phrases:

- Original choreography traversals are **substantially longer** than the spatial optimum, indicating that choreography is not primarily designed for displacement efficiency.
- Christofides tours consistently produce **near‑optimal** paths, typically within a small percentage of the exact optimum.

(See `results_with_optimal.csv` and the generated figures in `figures/`.)

---

## Reproducing the Pipeline

Example commands:

```bash
python scripts/extract_head_coords.py --video <video.mp4> --model <pose_landmarker_full.task> --out head.xlsx
python scripts/clean_coords.py --in head.xlsx --out cleaned.xlsx
python scripts/make_keypoints.py --in cleaned.xlsx --out keypoints.xlsx
python scripts/run_experiments.py --data-dir data --pattern "keypoints*.xlsx" --plot
python scripts/plot_results.py --csv results_with_optimal.csv
```

---

## Future Work

Potential extensions include:

- multi‑dancer coordination optimization
- time‑dependent routing with tempo constraints
- biomechanical energy models incorporating velocity and acceleration
- comparative analysis across choreographers and dance styles

---

## Author

Sulin Gu  
Rice University — Mathematics and Computer Science
