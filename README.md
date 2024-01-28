# Formation control scheme with Reinforcement Learning for Multiple Surface vehicles (SV)
A combination of formation control and optimal control based on reinforcement learning for multiple SVs    
Full report: [link](https://drive.google.com/drive/folders/1O79KVI5BtS4bu3oG9LMU0cJH48o4lHXR)

# 1. Introduction
This article presents a comprehensive approach to integrating formation tracking control and optimal control for a fleet of multiple surface vehicles (SVs), accounting for both kinematic and dynamic models of each SV agent. The proposed control framework comprises two core components: a high-level displacement-based formation controller and a low-level reinforcement learning (RL)-based optimal control strategy for individual SV agents. The high-level formation control law, employing a modified gradient method, is introduced to guide the SVs in achieving desired formations. Meanwhile, the low-level control structure, featuring time-varying references, incorporates the RL algorithm by transforming the time-varying closed agent system into an equivalent autonomous system. The application of Lyapunov’s direct approach, along with the existence of the Bellman function, guarantees the stability and optimality of the proposed design. Through extensive numerical simulations, encompassing various comparisons and scenarios, this study demonstrates the efficacy of the novel formation control strategy for multiple SV agent systems, showcasing its potential for real-world applications.
# 2. The proposed control scheme
<img width="800" alt="control_scheme" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/7090a2ba-3d5e-4ebe-8ce4-9b1e9ccee398">

# 2.1. The high-level displacement-based controller
The high-level formation control law, employing a modified gradient method, translates the desired formation and trajectory into individual reference trajectories that are feasible.
$$\dot{\bar{p_j}} = h_j h_j^T f_j,$$
$$\dot{h_j} = (I - h_j h_j^T) f_j, j \in S $$
The high-level displacement-based formation control protocol can be implemented for each SV:
$$\dot{\bar{x_j}} = \bar{v_j} cos \bar{\psi_j}, $$
$$\dot{\bar{y_j}} = \bar{v_j} sin \bar{\psi_j}, $$
$$\bar{\omega_j} = [-sin \bar{\psi_j},cos \bar{\psi_j}](-(\mathcal{L} \otimes I)(\bar{p_j} - \bar{p_j}^*)), $$

$$\bar{v_j} = [cos \bar{\psi_j}, sin \bar{\psi_j}](-(\mathcal{L} \otimes I)(\bar{p_j} - \bar{p_j}^*))$$

After that, we can obtain the desired trajectory for the low-level controller by integrating these derivatives.

# 2.2. Low-level RL-based control design for each SV
We approximate the Bellman function and the Optimal controller using a critic NN and an actor NN:

$$\widehat V_i(X_i) = {\widehat {W}_{ci}}^T\Psi_i (X_i)$$

$$\widehat u_i(X_i) =  - \frac{1}{2}{R^{ - 1}}{G_i^T}(X_i){(\frac{{\partial \Psi_i }}{{\partial x_i}})^T}{\widehat {W}_{ci}}$$

# 3. Multi-agent formation controller verification
# 3.1. Flower-shaped formation
The communication graph:   

<img width="276" alt="communication graph" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/ecba7c27-1c9b-4ac5-b507-be48af7ef5f1">   

Tracking trajectories of four agents following a straight line:   

<img width="249" alt="tracking_case1" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/5d37d348-2322-4869-a1d5-84e9b8ea5937">

<img width="360" alt="flower_shape_illu" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/138e2d97-5d80-46b5-b12e-90a22b64c998">

# 3.2. Square formation
The communication graph:   

<img width="276" alt="communication graph" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/8527b09a-b81e-4aaa-ad2a-075a6fa17d11">   

Tracking trajectories of four agents following a circle line:   

<img width="246" alt="tracking_case2" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/0b81008b-9f05-4383-afd9-e70fc66c3925">

<img width="360" alt="square_illu" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/9a3d6b41-cc0b-48b1-a5ca-ca8528a60414">

# 3.3. Diamond formation with more agents
The communication graph:   

<img width="349" alt="communication_graph_2" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/2b411450-51e5-48ff-88aa-e66d0a3fb1e3">

Tracking trajectories of eight agents following a circle line:   

<img width="265" alt="diamond_illu" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/c081de83-1612-49d5-ba7e-0bc32561604e">

# 3.4. Advantages of the RL-based method compared to a non-RL policy
The metric is formulated as follows:   

$$J_\Sigma = \int\limits_0^T\left(  {\eta_i^T}Q\eta_i + {\tau_i^T}R\tau_i \right)dt$$   

The cumulative cost with RL is consistently smaller than that without RL:   

<img width="260" alt="cost_func_compare" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/40d7b6c5-5f64-4ac7-aa2b-98b85c56acd0">

# 4. Conclusion
Project development direction:
* The authors plan to conduct experimental validation and extend the low-level tracking controller with model-free RL algorithms that do not necessarily require complete system dynamics.
* Direct implementation of RL algorithms to solve multi-agent control problems in nonlinear systems with uncertainty and disturbance is considered as a feasible approach for further research.




