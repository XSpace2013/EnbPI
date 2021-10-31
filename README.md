# Sequential Distribution-free Ensemble Batch Prediction Intervals (EnbPI)

>**Important Update:** We have been improving the ICML 2021 work for a journal submission. An [arxiv version](https://arxiv.org/abs/2010.09107) has been posted and linked to this repository for method implementation of both works. The current repository will soon be under one branch and the journal method under another (to be posted).

> Talk, Code, Extension Ideas for Our ICML 2021 Oral Work: [Conformal Prediction Interval for Dynamic Time-series](https://arxiv.org/abs/2010.09107) (Xu et al. 2021a). <!-- Please refer to codes in this repository for usage, as those downloaded from [PMLR]() had not been clearly explained. --> <!-- Put a link here once PMLR shows my work -->

> Please cite our work through [PMLR V139](http://proceedings.mlr.press/v139/xu21h.html) if you find it interesting and inspiring to your work. Please use codes in this repository, as those downloaded from PMLR are not the most updated ones.

> Please direct any inquiries either to [Chen Xu](https://sites.gatech.edu/chenxu97/) (cxu310@gatech.edu) or [Yao Xie](https://www2.isye.gatech.edu/~yxie77/index.html) (yao.xie@isye.gatech.edu). The work is constantly updated to incorporate new feedback and ideas. 

## Table of Contents
* [How to use](#how-to-use)
* [Poster Talk and Slides](#poster-talk-and-slides)
* [Extension Works and Ideas](#extension-works-and-ideas)
* [FAQ](#faq)
* [References](#references)
<!-- * [License](#license) -->

## How to use
- **Required Dependency:** 
  - Basic modules: `numpy, pandas, sklearn, scipy, matplotlib, seaborn`.
  - Additional modules: `statsmodels` for implementing ARIMA, `keras` for building neural network and recurrent neural networks, and `pyod` for competing anomaly detection methods.
- **General Info and Tests:** This work reproduces all experiments in [Conformal Prediction Interval for Dynamic Time-series](https://arxiv.org/abs/2010.09107) (Xu et al. 2021a). In particular, 
  - [tests_paper.ipynb](https://github.com/hamrel-cxu/EnbPI/blob/main/tests_paper.ipynb) provides an illustration of how to generate the main figures (Figure 1-4) in the paper. The code contents are nearly identical to those in [tests_paper.py](https://github.com/hamrel-cxu/EnbPI/blob/main/tests_paper.py). 
  - [tests_paper+supp.py](https://github.com/hamrel-cxu/EnbPI/blob/main/tests_paper%2Bsupp.py) reproduces all figures, including additional ones found in the Appendix.
- **EnbPI implementation:** 
  - [PI_class_EnbPI.py](https://github.com/hamrel-cxu/EnbPI/blob/main/PI_class_EnbPI.py) implements the [class](https://github.com/hamrel-cxu/EnbPI/blob/85245eb51adb5276b17b320be6cf1f83629b712b/PI_class_EnbPI.py#L20) that contains **EnbPI** ([line](https://github.com/hamrel-cxu/EnbPI/blob/85245eb51adb5276b17b320be6cf1f83629b712b/PI_class_EnbPI.py#L119)), Jackknife+-after-bootstrap ([line](https://github.com/hamrel-cxu/EnbPI/blob/85245eb51adb5276b17b320be6cf1f83629b712b/PI_class_EnbPI.py#L192), [paper](https://proceedings.neurips.cc/paper/2020/hash/2b346a0aa375a07f5a90a344a61416c4-Abstract.html)), Split/Inductive Conformal ([line](https://github.com/hamrel-cxu/EnbPI/blob/85245eb51adb5276b17b320be6cf1f83629b712b/PI_class_EnbPI.py#L222), [paper](https://www.intechopen.com/books/tools_in_artificial_intelligence/inductive_conformal_prediction__theory_and_application_to_neural_networks)), and Weighted Inductive Conformal ([line](https://github.com/hamrel-cxu/EnbPI/blob/85245eb51adb5276b17b320be6cf1f83629b712b/PI_class_EnbPI.py#L266), [paper](https://www.stat.cmu.edu/~ryantibs/papers/weightedcp.pdf)). We used [ARIMA](https://github.com/hamrel-cxu/EnbPI/blob/85245eb51adb5276b17b320be6cf1f83629b712b/PI_class_EnbPI.py#L318) as another competing method. 
  - Because conditional coverage (Figure 3) and anomaly detection (Figure 4) require problem-specific modifications, the code changes are not contained in "PI_class_EnbPI.py" but in their respective sections within [tests_paper.py](https://github.com/hamrel-cxu/EnbPI/blob/main/tests_paper.py)/[tests_paper+supp.py](https://github.com/hamrel-cxu/EnbPI/blob/main/tests_paper%2Bsupp.py).
- **Other Function Files:** 
  - [utils_EnbPI.py](https://github.com/hamrel-cxu/EnbPI/blob/main/utils_EnbPI.py) primarily contain plotting functions for all figures except Figure 4.
  - [PI_class_ECAD.py](https://github.com/hamrel-cxu/EnbPI/blob/main/PI_class_ECAD.py) implements **ECAD** based on **EnbPI** (see [Xu et al. 2021a, Section 8.5, Algorithm 2]) and [utils_ECAD.py](https://github.com/hamrel-cxu/EnbPI/blob/main/utils_ECAD.py) contains helpers for anomaly detection.
- **Additional Files** 
  - The [Data](https://github.com/hamrel-cxu/EnbPI/tree/main/Data) repository contains all dataset in our paperexcept the money laundry one for Figure 4 (due to size limit). 
  - The [Results](https://github.com/hamrel-cxu/EnbPI/tree/main/Results) repository is provided for your convenience to reproduce plots, since some experiments by neural network/recurrent neural networks can take some time to execute. It contains all .csv results files on all dataset.
- **Broad Usage:** To wrap **EnbPI** around other regression models and/or use on other data, one should:
  - **If other regression models:** Make sure the model has methods `.fit(X_train, Y_train)` to train a predictor and `.predict(X_predict)` to make predictions on new data. Most models in [sklearn](https://scikit-learn.org/stable/supervised_learning.html) or deep learning models built by keras/pytorch are capable of doing so.
  - **If other data:** We have assumed that all our datasets are save as `pandas.DataFrame` and convertible to `numpy.array`. However, such assumptions are purely computational. Please feel free to adjust the data formate as long as it can be processed by regression models of choice.

## Poster Talk and Slides

- The poster for our work is [available via this link](https://github.com/hamrel-cxu/EnbPI/blob/main/ICML%20Poster.png).
- We are fortunate to pre-record a long presentation and give an oral presentation at the Proceedings of the 38th International Conference on Machine Learning (ICML 2021). The long presentation is [available on Slideslive](https://recorder-v3.slideslive.com/?share=37762&s=ee12530c-5218-4c9e-8bb3-5107ceb79f41) and the oral presentation will be given at the conference once the date is finalized.
- The slide for the talk is [available here](https://github.com/hamrel-cxu/EnbPI/blob/main/ICML2021_Slide.pdf).

## Extension Works and Ideas
- [Conformal Anomaly Detection on Spatio-Temporal Observations with Missing Data](https://arxiv.org/abs/2105.11886) (Xu et al. 2021b) is our recent applicable work on adopting **EnbPI** for detecting anomalous traffic flows. Our method significantly outperforms competing methods (Table 1). It has been accepted by the Distribution-free Uncertainty Quantification Workshop in ICML 2021 ([DFUQ 2021](https://sites.google.com/berkeley.edu/dfuq21/)), with the [Poster here](https://github.com/hamrel-cxu/EnbPI/blob/main/DFUQ%202021%20Anomaly%20Detection%20Poster.png).
- We are also actively exploring ways further improve **EnbPI** in classification, so that the resulting prediction sets work well for correlated categorical observations.

## FAQ
1. Encountering "NotImplementedError: Cannot convert a symbolic Tensor (lstm_2/strided_slice:0) to a numpy array" when using RNN as the regression model:
- See [this github answer](https://stackoverflow.com/questions/66207609/notimplementederror-cannot-convert-a-symbolic-tensor-lstm-2-strided-slice0-t) to resolve the problem, primarily due to numpy & python version issues.

## References
- Xu, Chen and Yao Xie (2021a). Conformal prediction interval for dynamic time-series. The Proceedings of the 38th International Conference on Machine Learning, PMLR 139, 2021.
- Xu, Chen and Yao Xie (2021b). Conformal Anomaly Detection on Spatio-Temporal Observations with Missing Data. arXiv: 2105.11886 [stat.AP].

