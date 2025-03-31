> **Q.** Additional experiments on the pathological cases (Table 1) with $d=256$ and on the benchmark introduced in [Korotin et al., 2022]

We appreciate the reviewer for providing an insightful comment. Following the reviewer's suggestion, we conducted two additional experiments: (1) benchmark experiments from [1] and (2) 256-dim version of the failure case experiments in Table 1.

**(1) Benchmark experiment from [1]:** 
**We evaluated our model on the benchmark from [1]**, not in [Korotin et al., 2022], because the latter targets the Wasserstein-1 setting, which differs from our setting. Specifically, we implemented our OTP model, based on the [MMv2:R] baseline in [1], which solves the SNOT formulation (Eq. 18) using an ICNN architecture. 

Note that this benchmark employs a Gaussian mixture as the source distribution, which is already absolutely continuous. Therefore, by our Thm 3.1., existing SNOT models can also recover the correct OT map. In this respect, this benchmark is slightly unfavorable to our OTP model, because our additional input noise would be regarded as an error. Nevertheless, as shown in the table below, our model shows comparable performance to MMv2:R. **We included this discussion and the full results table, including 16-dim case and additional baselines, in the revised manuscript**.

||D=64||D=256||
|:---|:---|:---|:---|:---|
|| $\mathcal{L}^2$-UVP ($\downarrow$) | cos ($\uparrow$) | $\mathcal{L}^2$-UVP ($\downarrow$) | cos ($\uparrow$) |
|L| 63.9 | 0.75 | 67.4 | 0.77 |
|MMv2:R| 6.8  | 0.97 | 2.8 | 0.99  | 
|Ours| 6.5 | 0.97 | 3.7 | 0.99 |


**(2) 256-dim experiments of Table 1:** 
**We extended our failure case experiments to 256 dimensions**. The results are provided below and added to the revised version of Table 1. In the Perpendicular case, our model outperforms both OTM and OTM-s in terms of both $D_{cost}$ and $D_{target}$. In the One-to-Many case, our model shows comparable performance.

||Perpendicular||One-to-Many||
|:---|:---|:---|:---|:---|
|Method| $D_{cost}$ | $D_{target}$ | $D_{cost}$ | $D_{target}$ |
|OTM| 10.98 | 84.91 | **0.04** | 62.02 | 
|OTM-s| 16.45 | 81.68 | 0.25 | 61.87 |
|Ours| **5.05** | **63.36**  | 0.33 | **61.27**|


Reference
- [1] Korotin et al., "Do Neural Optimal Transport Solvers Work? A Continuous Wasserstein-2 Benchmark.", NeurIPS, 2021.
