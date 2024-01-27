# Formation control scheme with Reinforcement Learning for Multiple Surface vehicles
A combination of formation control and optimal control based on reinforcement learning for multiple SVs    
Full report: [link](https://drive.google.com/drive/folders/1O79KVI5BtS4bu3oG9LMU0cJH48o4lHXR)

# Introduction
This article presents a comprehensive approach to integrating formation tracking control and optimal control for a fleet of multiple surface vehicles (SVs), accounting for both kinematic and dynamic models of each SV agent. The proposed control framework comprises two core components: a high-level displacement-based formation controller and a low-level reinforcement learning (RL)-based optimal control strategy for individual SV agents. The high-level formation control law, employing a modified gradient method, is introduced to guide the SVs in achieving desired formations. Meanwhile, the low-level control structure, featuring time-varying references, incorporates the RL algorithm by transforming the time-varying closed agent system into an equivalent autonomous system. The application of Lyapunov’s direct approach, along with the existence of the Bellman function, guarantees the stability and optimality of the proposed design. Through extensive numerical simulations, encompassing various comparisons and scenarios, this study demonstrates the efficacy of the novel formation control strategy for multiple SV agent systems, showcasing its potential for real-world applications.
# 1. The proposed control scheme
<img width="544" alt="control_scheme" src="https://github.com/duongdinhph/Formation_RL_for_multiagents/assets/56771011/7090a2ba-3d5e-4ebe-8ce4-9b1e9ccee398">

# 1.1. The high-level displacement-based controller
The high-level formation control law, employing a modified gradient method, translates the desired formation and trajectory into individual reference trajectories that are feasible.
$$\dot{\bar{p_j}} = h_j h_j^T f_j, \\ $$
         $$\dot{h_j} = (I - h_j h_j^T) f_j, j \in S $$
The high-level displacement-based formation control protocol can be implemented for each SV:
$$\dot{\bar{x_j}} = \bar{v_j} cos \bar{\psi_j}, $$
$$\dot{\bar{y_j}} = \bar{v_j} sin \bar{\psi_j}, $$
$$\bar{v_j} = [cos \bar{\psi_j}, sin \bar{\psi_j}](-(\mathcal{L} \otimes I)(\bar{p_j} - \bar{p_j}^*)), $$
# 1.2. The high-level displacement-based controller
The HJB equation:
$$ H\left(X_i,u_i^*,\frac{{\partial {V_i^*}}}{{\partial X_i}}\right)=r(X_i(\tau ),{u_i^*}(\tau )) + \frac{{\partial {V_i^*}}}{{\partial X_i}}(K_i(X_i) + L_i(X_i){u_i^*}) = 0 $$
We approximate the Bellman function and the optimal controller using a critic NN and an actor NN:
$$\widehat V_i(X_i) = {\widehat {W}_{ci}}^T \Psi_i (X_i) $$
$$\widehat u_i(X_i) =  - \frac{1}{2}{R^{ - 1}}{G_i^T}(X_i){(\frac{{\partial \Psi_i }}{{\partial x_i}})^T}{\widehat {W}_{ci}} $$
# 3. Simulation
![3D_tracking_skew](https://github.com/duongdinhph/OTCP_Quad/assets/56771011/5f818f3d-f018-494b-a6ec-4f97d2e55295)

Consider a quadrotor with the desired trajectory as a spiral trajectory
In the first stage, we use 2 PID controllers for both outer and inner loops to collect data for the next
stage of training to obtain the optimal controllers. Note that noises are added to the system to guarantee
the PE condition.

![xyz_wrt_ref](https://github.com/duongdinhph/OTCP_Quad/assets/56771011/be6b3386-5f5b-419b-b4d3-0e306fc9f110)

The position tracking error in this stage is illustrated in the figure above.
Then, we use the data as the input to the algorithms which are proposed in the previous section. The
convergences of the weights are shown in the figure above.
After we obtain the weights, estimated optimal controllers are applied to the object. The tracking
performance is illustrated in figure above.
# 4. Conclusion
In this project, a novel control strategy that consists of the Off-policy RL algorithm was proposed. By
collecting data to train two actor-critic networks (NNs) which aim to estimate the optimal controllers
which includes a position controller and attitude controller, this structure has the advantage of no need
of any prior information on the high coupling system. Finally, simulation results are provided to
illustrate the tracking performance of a sophisticated trajectory of the system.


