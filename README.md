# Low-rank Tensor Completion Approach for Incomplete and Corrupted Traffic Data Recovery

![Python 3.9](https://img.shields.io/badge/Python-3.9-blue.svg)

![MIT License](https://img.shields.io/badge/license-MIT-green.svg)

> This is the repository for our paper 'A Flexible and Robust Tensor Completion Approach for Trafﬁc Data Recovery with Low-rankness', which is submitted to IEEE Transactions on Intelligent Transportation Systems.
>
> The authors are organizing the experimental files, which will be publicly available upon acceptance.

## Overview
Data missingness and random anomalies are ubiquitous in intelligent transportation systems (ITS), resulting in poor data quality and usability, which is a major impediment to real-world ITS applications.

This repository provides the codes of a novel low-rank tensor completion approach termed SCPN and its robust form termed RSCPN, which can effectively and efficiently recover ground-truth values from incomplete and corrupted observations. Besides, some toy examples will also be provded to show how to use SCPN as well as RSCPN.

## Problem Statement
In the real world, the acquisition of trafﬁc state data is often incomplete due to uncertainties such as signal interruptions or temporary power outages. In addition, collected data are vulnerable to corruption by ubiquitous anomalies. We here differentiate the following two data quality improvement tasks:
- Trafﬁc data imputation task: to impute missing values in the partial observations by leveraging the intrinsic lowrankness of trafﬁc spatiotemporal data.
- Trafﬁc data recovery task: to simultaneously impute missing values and replace potential anomalies with reasonable ones. Note that the anomalies considered in this work are those unstructured outliers caused by data measurement errors.

![framework](https://github.com/LiyangHu97/RSCPN/blob/main/Figures/framework.png)

## Model Description

### Low-rank tensor completion (LRTC) approach 

The high-dimensional traffic spatiotemporal data detected by $n_1$ sensors at $ n_3 $ time intervals within $ n_2 $ days can be structured as a third-order tensor with the size of $ \mathcal{X} \in \mathbb{R}^{n_1 \times n_2 \times n_3} $, which is assumed to have a low-rank property. Thus, the general mathematical form of LRTC is expressed as:

```math
\min _{\mathcal{X}}  \operatorname{rank}(\mathcal{X}), \text { s.t. } \mathcal{P}_{\Omega}(\mathcal{X})=\mathcal{P}_{\Omega}(\mathcal{Y}),
```

where $ \operatorname{rank} \left( \cdot \right)  $ indicates the algebraic rank of the tensor $ \mathcal{X} $, $ \Omega $ denotes the set of observed entries, and the operator $ \mathcal{P}_{\Omega} $ represents the orthogonal projection supported on $ \Omega $, i.e.,

```math
\left[\mathcal{P}_{\Omega}(\mathcal{X})\right]_{i,j,e}= \begin{cases}x_{i,j,e}, & \text { if }(i,j,e) \in \Omega. \\ 0, & \text {otherwise}.\end{cases}
```

### Schatten p norm

Due to the non-convexity and discreteness, to solve the rank minimization problem is generally NP-hard. There are various alternatives (including convex surrogate and non-convex surrogate) for the algebraic rank, of which the Schatten p norm is a flexible one that can well-balance the rank function and the traditional nuclear norm.

![Schatten p norm](https://github.com/LiyangHu97/RSCPN/blob/main/Figures/scp_norm.png){:height="50%" width="50%"}

### Tensor Schatten capped p norm (SCPN)

In this work, we propose a tensor Schatten capped p norm, a non-convex rank substitution, which is determined  as:

```math
\|\mathcal{X}\|_{S_{p}, \tau}=\sum_{k=1}^{3} \alpha_{k} \left(\sum_{i=1}^{\min \left\{n_{1}, n_{2}\right\}} \min \left(\sigma_{i}\left(\mathcal{X}_{(k)}\right), \tau\right)^{p}\right)^{\frac{1}{p}},
```

By proposing the tensor Schatten capped p norm, the corresponding relaxed LRTC approach can be expressed as:

```math
\min _{\mathcal{X}}  \sum_{k=1}^{3} \alpha_{k}\left\|\mathcal{X}_{(k)}\right\|_{S_{p}, \tau}^{p}, \text { s.t. } \mathcal{P}_{\Omega}(\mathcal{X})=\mathcal{P}_{\Omega}(\mathcal{Y}).
```

```math
			\begin{split}
				\min _{\{ \mathcal{X}_{k} \}_{k=1}^{3}, \mathcal{M}}  \sum_{k=1}^{3} \alpha_{k}\left\|\mathcal{X}_{k(k)}\right\|_{S_{p}, \tau}^{p}, \\
				\text { s.t. } \mathcal{X}_{k} = \mathcal{M},		\mathcal{P}_{\Omega}(\mathcal{M})=\mathcal{P}_{\Omega}(\mathcal{Y}).
			\end{split}
```


### Robust form (RSCPN)

Taking random anomalies into account, we further extend the proposed SCPN into a robust form termed RSCPN, which is formulated as:

```math
			\begin{split}
				\min _{\{ \mathcal{X}_{k}, \mathcal{E}_{k} \}_{k=1}^{3}, \mathcal{M}}  \sum_{k=1}^{3} \alpha_{k}\left\|\mathcal{X}_{k(k)}\right\|_{S_{p}, \tau}^{p} + \lambda_{k} \| \mathcal{E}_{k} \|_{1}, \\
				\text { s.t. } \mathcal{X}_{k} + \mathcal{E}_{k} = \mathcal{M},		\mathcal{P}_{\Omega}(\mathcal{M})=\mathcal{P}_{\Omega}(\mathcal{Y}),
			\end{split}
```
where $ \lambda_{k} $ balances the importance of the two terms.


## Datasets

We provide two datasets in this repository:

- PEMS speed: The PEMS speed dataset contains 44 days’ (weekdays of May and June, 2012) trafﬁc speed information detected by 228 loop detectors in District 7 of California with a 5-minute time resolution. The corresponding tensor size is `228 ×44×288`.
- PEMS volume: The PEMS volume dataset includes 62 days’ (Jul.1-Aug.31, 2016) trafﬁc volume information detected by 170 loop detectors in San Bernardino with a 5minute time resolution. The corresponding tensor size is `170×62×288`.

## Toy examples

We give two toy examples tailored for missing data imputation and corrupted data recovery tasks in the Jupyter Notebook `toy_example_1.ipynb` and `toy_example_2.ipynb`, respectively.

## Reference

If you find this repository useful for your research, please cite our paper.

## License

This work is released under the MIT license.

