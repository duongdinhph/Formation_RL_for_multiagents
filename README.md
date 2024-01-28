# Formation control scheme with Reinforcement Learning for Multiple Surface vehicles (SV)
A combination of formation control and optimal control based on reinforcement learning for multiple SVs    
Full report: [link](https://drive.google.com/drive/folders/1O79KVI5BtS4bu3oG9LMU0cJH48o4lHXR)

# 1. Introduction
This article presents a comprehensive approach to integrating formation tracking control and optimal control for a fleet of multiple surface vehicles (SVs), accounting for both kinematic and dynamic models of each SV agent. The proposed control framework comprises two core components: a high-level displacement-based formation controller and a low-level reinforcement learning (RL)-based optimal control strategy for individual SV agents. The high-level formation control law, employing a modified gradient method, is introduced to guide the SVs in achieving desired formations. Meanwhile, the low-level control structure, featuring time-varying references, incorporates the RL algorithm by transforming the time-varying closed agent system into an equivalent autonomous system. The application of Lyapunov’s direct approach, along with the existence of the Bellman function, guarantees the stability and optimality of the proposed design. Through extensive numerical simulations, encompassing various comparisons and scenarios, this study demonstrates the efficacy of the novel formation control strategy for multiple SV agent systems, showcasing its potential for real-world applications.
# 2. The proposed control scheme
<img width="544" alt="control_scheme" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/7090a2ba-3d5e-4ebe-8ce4-9b1e9ccee398">

# 2.1. The high-level displacement-based controller
The high-level formation control law, employing a modified gradient method, translates the desired formation and trajectory into individual reference trajectories that are feasible.
$$\dot{\bar{p_j}} = h_j h_j^T f_j,$$
$$\dot{h_j} = (I - h_j h_j^T) f_j, j \in S $$
The high-level displacement-based formation control protocol can be implemented for each SV:
$$\dot{\bar{x_j}} = \bar{v_j} cos \bar{\psi_j}$$
$$\dot{\bar{y_j}} = \bar{v_j} sin \bar{\psi_j}$$
$$\bar{v_j} = [cos \bar{\psi_j}, sin \bar{\psi_j}](-(\mathcal{L} \otimes I)(\bar{p_j} - \bar{p_j}^*))$$
After that, we can obtain the desired trajectory for the low-level controller by integrating these derivatives.

# 2.2. Low-level RL-based control design for each SV
We approximate the Bellman function and the Optimal controller using a critic NN and an actor NN:
$$\widehat V_i(X_i) = {\widehat {W}_{ci}}^T\Psi_i (X_i)$$
$$\widehat u_i(X_i) =  - \frac{1}{2}{R^{ - 1}}{G_i^T}(X_i){(\frac{{\partial \Psi_i }}{{\partial x_i}})^T}{\widehat {W}_{ci}}$$






