## Results (3 choreography phrases, 18 keypoints each)

We treat the recorded choreography order (Excel row order) as the *original* time sequence, and measure route cost as total Euclidean displacement in the stage (X, Z) plane.

Across three phrases, the original traversal is **53–60% longer** than a spatially optimized tour.  
Christofides’ algorithm produces tours close to the **exact optimum** (Held–Karp), with gaps between **~3% and ~11%** in our samples.

| file | n | original | christofides | optimal | improvement | christofides gap |
|---|---:|---:|---:|---:|---:|---:|
| keypoints.xlsx | 18 | 4990.63 | 2312.79 | 2081.82 | 53.66% | 11.09% |
| keypoints_2.xlsx | 18 | 6501.69 | 2676.73 | 2594.98 | 58.83% | 3.15% |
| keypoints_3.xlsx | 18 | 5364.02 | 2118.89 | 2015.67 | 60.50% | ~5.1% |

![Results summary](figures/results_summary.png)
