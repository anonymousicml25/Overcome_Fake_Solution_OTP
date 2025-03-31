>**Q.** Relationship between the LPIPS metric and the transport cost.

**A.** Thank you for the insightful comment. We interpret the **LPIPS metric as a proxy for the transport cost in the feature space**, while FID serves as a proxy for the marginal constraint violation (i.e., how well $T_{\\#}\mu = \nu$ is satisfied). Specifically, the LPIPS metric is defined as:

$$LPIPS(x, T(x)) = \sum_{l} \frac{1}{H_{l}W_{l}} \sum_{h,w} \| (f^{l}(x) - f^{l}(T(x)))_{h, w} \|^2.$$

where $l$ denotes the feature layer index of the VGG netwotk and $f^{l}$ is the feature extracter for the $l$-th layer. $h, w$ indicates indices for feature height and width. In this formulation, LPIPS measures the transport cost between features of the source image $x$ and the translated image $T(x)$.

In this respect, in the Neural OT models for image datasets, **LPIPS metic has been widely adopted as the (proxy) measure of transport cost [1, 2]**, while FID is used to assess how well the marginal constraint $T_{\\#}\mu = \nu$ is satisfied. Following this convention, we adopted LPIPS and FID to evaluate cost optimality and marginal constraint violation, respectively.

Reference
- [1] Shi, Yuyang, et al. "Diffusion schrödinger bridge matching." NeurIPS 2023.
- [2] Gushchin, Nikita, et al. "Adversarial Schr\" odinger Bridge Matching." NeurIPS 2024.

---
> **Q.** Additional experiments on the pathological cases (Table 1) with $d=256$ and on the benchmark introduced in [Korotin et al., 2022]

**A.** We appreciate the reviewer for providing an insightful comment. Following the reviewer's suggestion, we conducted two additional experiments: (1) benchmark experiments from [1] and (2) 256-dim version of the failure case experiments in Table 1.

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

---
**Other Comments Or Suggestions:**

>**Q.** Fake solutions may violate the marginal constraint or cost optimality.

**A.** Thank you for the great question. While our focus is on cases where the marginal constraint is not satisfied, one might wonder whether spurious solutions to the max-min formulation could still arise even when the marginal constraint is met, but the solution is not cost-optimal. However, we would like to emphasize that this situation does not occur. Specifically, **any max-min solution $T^{\dagger}$ satisfying the marginal constraint, i.e., $T^{\dagger}_\\# \mu=\nu$ is guaranteed to be the optimal transport map**. This result was established in [Thm 3, [1]]. To clarify this, we revised the beginning of Sec 3 as follows:

> In particular, even ${T^{\\dagger}} \mu = \nu$ does not hold in general (see Fig. 1), which means that $T^{\dagger}$ is not a valid transport map from $\mu$ to $\nu$ as in (Eq. 3). It is worth noting that any max-min solution that satisfies $T^{\dagger}_\\# \mu = \nu$ is guaranteed to be the OT map [Thm 3, [1]].

Reference 
- [1] Fan, Jiaojiao, et al. "Neural monge map estimation and its applications." TMLR 2023.
