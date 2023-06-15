# Low-rank Tensor Completion Approach for Incomplete and Corrupted Traffic Data Recovery
> This is the repository for our paper 'A Flexible and Robust Tensor Completion Approach for Trafﬁc Data Recovery with Low-rankness', which is submitted to IEEE Transactions on Intelligent Transportation Systems.
> The authors are organizing the experimental files, which will be publicly available soon.

## Overview
Data missingness and random anomalies are ubiquitous in intelligent transportation systems (ITS), resulting in poor data quality and usability, which is a major impediment to real-world ITS applications.
This repository provides the codes of a novel low-rank tensor completion approach termed SCPN and its robust form termed RSCPN, which can effectively and efficiently recover ground-truth values from incomplete and corrupted observations.
Besides, some toy examples will also be provded to show how to use SCPN as well as RSCPN.

## Problem Statement
In the real world, the acquisition of trafﬁc state data is often incomplete due to uncertainties such as signal interruptions or temporary power outages. In addition, collected data are vulnerable to corruption by ubiquitous anomalies. We here differentiate the following two data quality improvement tasks:
- Trafﬁc data imputation task: to impute missing values in the partial observations by leveraging the intrinsic lowrankness of trafﬁc spatiotemporal data.
- Trafﬁc data recovery task: to simultaneously impute missing values and replace potential anomalies with reasonable ones. Note that the anomalies considered in this work are those unstructured outliers caused by data measurement errors.

## Model Description


## Dataset
