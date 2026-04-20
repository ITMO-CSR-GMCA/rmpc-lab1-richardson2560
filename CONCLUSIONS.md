# Conclusions and Analysis of Laboratory Work No. 1: Dynamic Model of the ABB IRB140

## 1. Overview of the Performed Work
In this laboratory work, the dynamic model of the **ABB IRB140** 6-degree-of-freedom industrial manipulator was developed and analyzed. The focus was on validating inverse dynamics using the Newton-Euler algorithm, employing simulation tools to evaluate the robot's behavior under various motion conditions.

## 2. Modeling and Dynamic Parameters
The kinematic and dynamic model was implemented based on the manufacturer's technical specifications [3].
* **Mass and Inertia:** Values for mass, centers of mass, and inertia tensors were loaded for each link.
* **Note on Omitted Parameters:** Friction coefficients (viscous and Coulomb) and gear ratios were not integrated into the final model. This decision is based on the fact that such information is not explicitly available in the official data sheets [3] or in the primary technical studies referenced [1, 2]. Therefore, the model is considered valid for ideal rigid body dynamics analysis.

## 3. Trajectory Planning with Waypoints
A non-trivial joint trajectory was implemented using **quintic polynomials** (5th degree), divided into two segments with an intermediate waypoint.
* **Continuity:** This approach ensures continuity not only in position and velocity but also in acceleration at the connection point.
* **Dynamic Impact:** By avoiding abrupt changes in acceleration, smooth torque profiles are achieved, which is critical for preventing mechanical stress and actuator saturation in real industrial robots.

## 4. Inverse Dynamics Analysis
Three distinct scenarios were solved to compare torque requirements:

1.  **Full Dynamics ($\dot{q} \neq 0, \ddot{q} \neq 0$):** Represents the total required torque. The graphs show peaks coinciding with the maximum acceleration phases of the quintic polynomial.
2.  **Quasi-statics ($\dot{q} \neq 0, \ddot{q} \approx 0$):** By neglecting acceleration, the resulting torque is primarily due to overcoming gravity at cruise velocities.
3.  **Static / Gravity Compensation ($\dot{q} = 0, \ddot{q} = 0$):** Shows the minimum torque needed to maintain the robot's configuration. The plots confirm that for the base links, the gravitational load represents the largest component of the motor effort.

## 5. Metric Analysis ($M, C, G$)
* **Inertia Matrix ($M$):** The Frobenius norm of $M$ remained stable throughout the motion, and the condition number indicates that the trajectory stayed well away from dynamic singularities.
* **Coriolis Matrix ($C$):** Its magnitude varies proportionally to the square of the velocity, reaching its peak at the center of the trajectory segments.
* **Gravity Vector ($G$):** This depends exclusively on the configuration $q$, acting as a constant bias that the actuators must compensate for at all times.

## 6. Bibliographic References
This work was supported by the following technical documentation:

1.  **Fazilat, M., & Zioui, N. (2024).** *The Impact of Simplifications of the Dynamic Model on the Motion of a Six-Jointed Industrial Articulated Robotic Arm Movement*. Journal of Robotics and Control (JRC).
2.  **Baquero Suárez, M., & Ramírez Heredia, R.** *Kinematics, Dynamics and Evaluation of Energy Consumption for ABB IRB-140 Serial Robots in the Tracking of a Path*. Universidad Nacional de Colombia.
3.  **ABB Robotics.** *Product Specification: IRB 140*. Document ID: 3HAC041346-001.