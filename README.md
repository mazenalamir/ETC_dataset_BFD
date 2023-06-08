# ETC_dataset_BFD
A Synthetic benchmark for blind anomaly detectors for industrial time series

[![DOI](https://zenodo.org/badge/650488034.svg)](https://zenodo.org/badge/latestdoi/650488034)

## Description of the dataset 
This is a synthetic dataset that might be used to challenge **Blind anomaly detector for time series**

a very common situation is investigated where a controlled system is involved which is based on the set of nominal parameters of the system. In this case, the very closed-loop nature implies that the feedback control could hide some of the consequences of the parametric changes representing anomalies. On the other hand, the variability of contexts materializes in the values of the set-point changes that can be applied and fed to the control feedback algorithm. A schematic view of the system used to build the dataset bencmark is shown hereafter: 

<p align="center">
  <img src="https://github.com/mazenalamir/ETC_dataset_BFD/blob/main/images/etc.png" width="50%">
  <p align="center"> Fig. 1: schematic view of the ETC system used to build the dataset</p>
</p>

The equations of the electronic throttle controlled system are

$$
\begin{align}
\dot x_1&=x_2 \\
\dot x_2&=\dfrac{1}{J}\bigl[-K_{sp}(x_1-\theta_0)-K_fx_2+NK_tx_3+ -\pi R_p^2R_{af}\Delta_p\cos^2(x_1)\bigr]\\
\dot x_3&=\dfrac{1}{L_a}\bigl[-NK_bx_2-R_ax_3+u\bigr]
\end{align}	
$$

where $K_{sp}$ characterizes the spring stiffness (see Fig.1 above), $K_f$ is the friction coefficient, $N$ is the gear ratio, $K_t$ is the electric torque static gain relatively to the current $i_a$. $R_p$ is a constant radius, $\Delta_p=P_\text{atm}-P_m$ where $P_m=f(\theta, P_\text{atm}, N)$ is the manifold pressure that approaches the atmospheric pressure $P_\text{atm}$ when the throttle is wide open. 

The system is controlled using a backstepping feedback desgin the details of which are ommitted here since they lie out of the scope of the anomalies detection topics. 

The benchmark consists in detecting changes impacting the following three parameters: $K_b$, $K_t$ and $L_a$ using an anomaly detector that is fitted on the time series produced using the nominal values of the parameters. 

The raw version of the time series is shown in the Figure 2. below:

<p align="center">
  <img src="https://github.com/mazenalamir/ETC_dataset_BFD/blob/main/images/raw_etc.png" width="50%">
  <p align="center"> Fig. 2: Raw version of the time series incuded in the test dataframe.</p>
</p>

The dataset consists of four csv pandas dataframes: 

- `df_train.csv`: The Dataframe of features for training 
- `df_train_labels.csv` : The Dataframe of labels for training 
- `df_test.csv`: The Dataframe of features for test 
- `df_test_labels.csv` : The Dataframe of labels for test

In order to read the dataframe, use the following pandas command 

```python 
import pandas as pd
df_train = pd.read_csv('df_train.csv', index_col=0)
```

The following images show the columns in the `df_train` and `df_test_label` dataframes: 

- `df_train`

=============

<p align="left">
  <img src="https://github.com/mazenalamir/ETC_dataset_BFD/blob/main/images/df_train.png" width="30%">
</p>

- `df_test_label`

=============

<p align="left">
  <img src="https://github.com/mazenalamir/ETC_dataset_BFD/blob/main/images/df_test_labels.png" width="20%">
</p>

### Important information on test data

> Please note that the training data lies in the first block of the `df_test`dataset. If you want to draw statistic, it is important to know that the first 6-th part of the test data is simply the training data. It is therefore expected that you get *nice* results on this part of the test data.

## Benchmark Description

Use the training dataset `df_train`in order to fit your anomalies detector. 
Use the test dataset `df_test`to predict the presence or not of anomalies in dataset. 
Compare your prediction to the column `label`of the dataframe `df_test_labels`. Note that `0`represent normal data while `1`represent anomalous data. 
The prediction can be performed over a moving window spanning the time series or using point-wise prediction. 
The nominal benchmark involves only the columns `x1`and `u`of the dataframe, but you might feel free to use less or more columns. 
The other columns in the `df_test_labels` are provided as extra columns that explains the origin of the anomalies. 

If interested in having more rich set of anomalies values, please contact me. 
