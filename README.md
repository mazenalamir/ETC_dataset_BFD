# ETC_dataset_BFD
A Synthetic benchmark for blind anomaly detectors for industrial time series

## Description of the dataset 
This is a synthetic dataset that might be used to challenge **Blind anomaly detector for time series**

a very common situation is investigated where a controlled system is involved which is based on the set of nominal parameters of the system. In this case, the very closed-loop nature implies that the feedback control could hide some of the consequences of the parametric changes representing anomalies. On the other hand, the variability of contexts materializes in the values of the set-point changes that can be applied and fed to the control feedback algorithm. A schematic view of the system used to build the dataset bencmark is shown hereafter: 

<p align="center">
  <img src="https://github.com/mazenalamir/ETC_dataset_BFD/blob/main/images/etc.png" width="30%">
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
