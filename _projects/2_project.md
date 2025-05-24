---
layout: page
title: "DOG: Dynamic Object Grasping"
description: Robotic grasping of object moving on 2D Deterministic Path with real-time Recursive Least Squares motion prediction.
img: assets/img/dog/dog.gif
importance: 2
category: research
related_publications: false
---

<section id="badgeproj-section">
<h2 class="badgeproj-title">Tech Stack 💻 & Resources📚</h2>
  <div class="badgeproj-container">
    <span class="badgeproj">Robot Manipulation</span>
    <span class="badgeproj">ROS</span>
    <span class="badgeproj">Gazebo</span>
    <span class="badgeproj">PyBullet</span>
    <span class="badgeproj">NumPy</span>
  </div>

<!-- Links Section -->
  <div class="linksproj-container">
    <a href="https://github.com/adityavkulkarni/2D_dynamic_object_grasping" target="_blank" class="linkproj">
      <i class="fab fa-github"></i> GitHub Repository
    </a>
    <a href="https://drive.google.com/file/d/16bMPWcBXGA10P0gyKAaFOmN-yCimzDyW/view?usp=sharing" target="_blank" class="linkproj">
      <i class="fas fa-file-alt"></i> Report
    </a>
    <a href="https://drive.google.com/file/d/1cyYIJvOVgrl79BqiMGc6voBraZUoIiu_/view?usp=sharing" target="_blank" class="linkproj">
      <i class="fas fa-file-powerpoint"></i> Slides
    </a>
    <a href="https://utdallas.app.box.com/s/tb7logwkyp9kxky6ieu988e71gn74qph" target="_blank" class="linkproj">
      <i class="fas fa-video"></i> Demo Video
    </a>
  </div>
</section>

**Authors**: <a href="https://sauravdosi.github.io/">Saurav Dosi</a>, <a href="https://adityavkulkarni.github.io/">Aditya Kulkarni</a>, and <a href="https://www.linkedin.com/in/ferozhatha/">Feroz Hatha</a>

**Course**: CS 6301 - Robotics, taught by [Dr. Yu Xiang](https://yuxng.github.io/), The University of Texas at Dallas

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dog/dog.gif" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Project Demo GIF.
</div>

## 1. Abstract
Robotic grasping has always been a fascinating challenge—especially when it comes to grabbing objects on the move. In this project, we tackled the problem of efficiently and accurately grasping a dynamic object traveling along a predictable (deterministic) path.

Our solution involves designing a control system that predicts the object's future pose, calculates the optimal interception point, and ensures precise grasping—all while accounting for trajectory feedback and timing constraints.

## 2. Introduction

Grasping objects in motion is no easy task, particularly when the object follows a deterministic path. Yet, this problem is highly relevant in industrial robotics, where manipulators need to pick up items moving on conveyor belts or perform mobile manipulations in dynamic environments.

To tackle this challenge, we developed a control system that enables a robotic manipulator to adapt to the future positions of a moving object. By interpreting the object's trajectory in real time, the robot can plan its motion to intercept and grasp the object with precision.

#### 2.1. Why This Matters
Dynamic object grasping combines key aspects of robotics: perception, planning, and control. Mastering this opens doors to solving real-world industrial problems, such as:

- Picking up objects from conveyor belts.
- Mobile robots interacting with static/moving environments.

#### 2.2. Inspiration and Methodology
Our approach builds on the Grasping Trajectory Optimization with Point Clouds (GraspTrajOpt) technique by Xiang et al., originally designed for static objects. We extended this for dynamic scenarios by:

1. Predicting future object poses.
2. Optimizing the robot's trajectory for interception.
The Fetch robot, paired with ROS and PyBullet simulations, served as our testbed, offering a robust platform to test and refine our ideas.

#### 2.3. A Progressive Approach
The project unfolds across three phases:

1. **Linear Motion**: Simplifying the problem with objects moving linearly (like on a conveyor belt).
2. **Complex Trajectories**: Expanding to circular and sinusoidal paths, integrating kinematic adjustments.
3. **Perception Integration**: Using an egocentric camera to detect object positions and model their motion dynamically.

## 3. Related Work
Dynamic object grasping has been an active area of research, with numerous approaches tackling different aspects of this challenge. Here's a look at some key contributions that inspired and guided our work:

#### 3.1. Reachability-Aware Grasping
Akinola, Xu, and colleagues presented a [dynamic grasping framework](https://arxiv.org/abs/2103.10562) designed to account for both reachability and motion. They introduced:

- **Signed Distance Fields**: Used to model the robot's reachability space, making it easier to eliminate unreachable grasps quickly.
- **Neural Network Predictions**: A model predicts the quality of potential grasps based on the object's motion, enabling real-time filtering of grasp options.
- **Motion Stability**: By using solutions from the previous time step, the system generates new arm trajectories close to prior plans, avoiding instability or fluctuation.

The framework leverages a recurrent neural network (RNN) to model and predict object motion, creating a robust and adaptable grasping strategy.

#### 3.2. Human-to-Robot Handovers
Robotic systems often struggle with the diverse sizes, shapes, and deformability of objects during handovers. [Yang et al](https://arxiv.org/abs/2011.08961). tackled this problem by developing a vision-based system for reactive handovers, focusing on:

- **Closed-Loop Motion Planning**: Ensures smooth and reactive grasping, even when objects are positioned unpredictably.
- **Real-Time Grasp Generation**: Adapts dynamically to rigid and non-rigid objects alike.

Their approach demonstrated exceptional robustness, tested on 26 diverse household objects and further validated through user studies.

#### 3.3. Learning to Grasp Dynamically
[Wu's work](https://arxiv.org/pdf/2203.02119) took a different angle by introducing an adversarial reinforcement learning framework called GraspARL. This method frames the dynamic grasping challenge as a "move-and-grasp" game, where:

- The robot attempts to grasp the object.
- An adversarial mover tries to escape, simulating complex, unpredictable trajectories.

By auto-generating diverse motion patterns, this framework enhances the robot's generalization capabilities. The results? Improved performance in both simulations and real-world scenarios.

#### 3.4. Insights for Our Approach
These studies provided valuable insights, such as using predictive models for motion-aware grasping and leveraging reinforcement learning for adaptability. Building on these principles, our project aims to develop a streamlined, deterministic approach that bridges the gap between trajectory prediction and efficient grasping.

## Method
#### 4.1. Simulation Setup

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dog/6301.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Workflow diagram of the architecture.
</div>

To simulate a robotic manipulation task involving a Fetch robot, we utilized Robot Operating System (ROS) integrated with Gazebo. The simulation environment consisted of a Fetch mobile manipulator robot, a table or conveyor belt, and a cube moving on the table/conveyor belt. The primary objective of Phase 1 was to intercept and grasp the moving cube using the robot's arm.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dog/dog1.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dog/dog2.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dog/dog3.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On the left, is the simple_grasp setup from fetch_gazebo repository. Middle, has a longer table. Right, is the final setup with a moving conveyor belt.
</div>

##### 4.1.1. Table Setup with Uniform Rectilinear Motion
Initially, the cube was programmed to move in a straight line on a table surface at a constant velocity.

- **Implementation Details**:

  - A Python script was developed to create a ROS node, publishing to the `/gazebo/set_model_state` topic.
  - The cube's initial position and velocity (0.01 m/s) were defined, with its position updated iteratively in the y-axis. The script ensured the cube reset to its initial position once it reached the table's edge.

- **Challenges**:
  - The default table length in the fetch_gazebo package was insufficient for dynamic grasping tasks.
  - High-frequency oscillations were observed due to teleportation-based movement, conflicting with Gazebo's physics engine.
  - The cube's velocity persisted after grasping, causing grip instability.
  
##### 4.1.2. Table Replacement with Extended URDF Setup
To address the short table issue, a custom URDF file for a longer table was created.

- **Configuration**:
  - The URDF defined the table's material properties, dimensions, and fixed joints.
  - The longer table was integrated into the Gazebo environment by modifying the launch file.

Despite mitigating oscillation issues by adjusting friction coefficients, complete resolution was unattainable due to the limitations of teleportation-based motion.

##### 4.1.3. Conveyor Belt Setup
To overcome the motion and grip issues, a conveyor belt plugin was used to simulate the cube's movement.

- **Advantages**:
  - Cube motion was governed by the conveyor surface instead of direct velocity application.
  - Conveyor speed was adjustable via ROS service calls, ensuring synchronization with the robot's grasping task.
  
#### 4.2. Motion Planning and Grasping
The robot's trajectory planning was divided into two steps:

- **Horizontal Alignment**:
  - The robot moved horizontally to align 0.5 units above the predicted intercept point on the y-axis.

- **Vertical Descent and Grasping**:
  - After alignment, the robot descended vertically to grasp and pick up the cube.

- **Verification**:
  - Successful grasps were verified by checking the cube's z-coordinate after lifting, ensuring it was above the table's surface.

- **Integration with MoveIt**:
  - MoveIt was utilized for motion planning and collision-free trajectory generation.
  - Time parameterization tools in MoveIt enabled synchronization between the robot's motion and the cube's velocity.

#### 4.3 Evaluation
During Phase 1 testing, the cube was moved linearly at a velocity of 0.1 units along the y-axis.

- Initial intercept coordinates were manually determined and updated dynamically after each successful grasp.
- The robot's pre-grasp position and motion planning time were tuned based on the cube's speed and trajectory, achieving consistent grasping performance.

This method provided a robust framework for addressing dynamic object manipulation in a simulated environment while highlighting practical challenges and solutions.

#### 4.4 Trajectory Prediction

To predict the trajectory of an object moving on a deterministic path, we use Recursive Least Squares (RLS). We take position coordinates of the moving object
$$ (x,y) $$ as input from the Gazebo simulation, update/train the RLS fitter separately for $$ x(t) $$ and
$$ y(t)$$, and then predict the position for future time steps
$$ T $$. While the fitter can be a polynomial of any degree, we incorporate sines and cosines for circular and sinusoidal motion of the object for future work.

##### 4.4.1. Objective: 
The goal of RLS is to minimize the weighted sum of the squared errors between the predicted output and the actual output. Given a linear model 

$$ 
y(t) = w^T x(t) + ϵ(t) 
$$ 
, where:

- $$ y(t) $$ is the observed output at time $$ t $$.
- $$ w $$ is the parameter vector to be estimated.
- $$ x(t) $$ is the input vector (features).
- $$ ϵ(t) $$is the error term.

##### 4.4.2. Error Definition: 
The error $$ e(t) $$ at time $$ t $$ is defined as:

$$
e(t) = y(t) - \mathbf{w}^T \mathbf{x}(t)
$$

The objective is to minimize the cost function:

$$
J(t) = \sum_{k=0}^{t} \lambda^{t-k} e(k)^2
$$
 
where $$ λ $$  (forgetting factor) controls the weight given to older observations.

##### 4.4.3. Recursive Update: The key steps in RLS involve:

- **Initialization**: Start with an initial guess for the parameter vector $$ w(0) $$ and an initial covariance matrix $$ P(0) $$, often chosen to be large to allow flexibility in the initial estimates.

- **Gain Calculation**: For each new observation, compute the gain vector $$ K(t): $$

$$
\mathbf{K}(t) = \frac{\mathbf{P}(t-1) \mathbf{x}(t)}{\lambda + \mathbf{x}(t)^T \mathbf{P}(t-1) \mathbf{x}(t)}
$$
 
This gain vector indicates how much to adjust the parameters based on the current error.

- **Parameter Update**: Update the parameter vector:

$$
\mathbf{w}(t) = \mathbf{w}(t-1) + \mathbf{K}(t) e(t)
$$

- **Covariance Matrix Update**: Update the covariance matrix:

$$
\mathbf{P}(t) = \frac{1}{\lambda} \left( \mathbf{P}(t-1) - \mathbf{K}(t) \mathbf{x}(t)^T \mathbf{P}(t-1) \right)
$$

#### 4.5. Intercepting a Moving Object
Intercepting a moving object to grasp it while it moves along a deterministic path is tricky. This involves considering the time needed for Inverse Kinematics (IK), executing the IK solution, and closing the gripper to pick the object. Here, we developed an algorithm to predict the best time to intercept a moving cube on the table along the y-axis.

##### 4.5.1. Intercept Algorithm:
We used a recursive least squares (RLS) approach to predict the cube's trajectory. The algorithm involves sampling future positions of the cube, calculating the required time for the gripper to reach the target, and then selecting the closest reachable point where the IK solution can be executed.

This allows the robot to intercept the cube at the correct time by aligning the gripper with the predicted position and grabbing it before it moves out of reach. Fine-tuning was required, especially due to uncertainties in the time needed for IK solutions.

<div class="row">
    <div class="col-sm mt-3 mt-md-0" style="max-width: 500px; margin: auto;">
        {% include figure.liquid loading="eager" path="assets/img/dog/doga4.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Interception Algorithm.
</div>

## 5. Experiments
#### 5.1. Pre-grasp to Grasp Time
We measured the time taken for the robot to move from the pre-grasp position to the grasp position. As the cube moved along the y-axis, we saw that it became more challenging for the robot to reach the target when the cube moved lower down the table. A sharp increase in time was observed when the cube reached lower y-coordinates.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dog/grasp_pose_estimate_time80.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Distribution of duration for pre-grasp to grasp position movement.
</div>

**Key Observations**:

- From iterations 0 to 30, the robot's efficiency in reaching the cube improved, requiring less time.
- Beyond iteration 30, the time to grasp increased due to the robot's limitations in reaching lower positions on the y-axis.
- A significant spike in time occurred at iteration 70 when the cube reached near the table's edge.

##### 5.1.1. Estimated vs Actual Time
We also measured the offset between the estimated and actual time taken to execute a trajectory. Generally, the offset remained small, except for a sharp spike at iteration 70, when the robot had to reconfigure its joints for a more complex grasp.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dog/offset80.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Difference between MoveIt estimate and actual movement duration.
</div>

#### 5.2. Gazebo Time vs Real-World Time
We compared the solution calculation time in Gazebo with real-world performance. In general, Gazebo and real-world times followed similar trends, with noticeable spikes in computation time at certain points. However, real-world execution consistently took longer during these spikes.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dog/solution_time_sim_real80.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Intercept solution calculation duration trend.
</div>

#### 5.3. Evaluation
We conducted 25 iterations to evaluate grasp success and time:

- **Grasp Success Rate**: The system successfully grasped the cube in 24 out of 25 attempts, achieving a 75% success rate.
- **Grasp Time**: The average grasp time was 7.2 seconds across all successful iterations.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/dog/total_time25.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Total actual Grasp time.
</div>

This evaluation confirms the effectiveness of the interception algorithm in simulating the grasping task.

## 6. Limitations and Future Work
#### 6.1. Perception
Currently, we rely on Gazebo for object pose estimation. In the future, we aim to improve the perception system by using the robot’s egocentric camera for real-time object tracking. This will involve RGBD data, object detection/segmentation, and computational geometry to track the object’s position relative to the depth camera. Integrating this with our current logic will improve grasping accuracy and efficiency, particularly for dynamic objects with non-linear paths or varying velocities.

#### 6.2. Exploring Non-linear Paths
We plan to extend our system to handle objects moving along non-linear paths, such as circular or sinusoidal trajectories. By using real-time sensor data and Recursive Least Squares (RLS) for trajectory prediction, we’ll incorporate periodic functions like sine and cosine to accurately predict object positions along these complex paths.

#### 6.3. Reinforcement Learning
We are considering the use of Reinforcement Learning (RL) to refine our interception logic. With RL, the system can learn a reward function based on grasp quality and interception success, automating fine-tuning and reducing human effort.

#### 6.4. Mobile Manipulation
We also plan to apply the system to mobile manipulation, where the robot approaches an object at a constant velocity, planning and executing the grasp while in motion. This will make the process more efficient by reducing time delays in adjusting to the object’s position.

## 7. Conclusion
This study demonstrates the successful implementation of robotic grasping for dynamic objects moving along deterministic paths, achieving an 80% grasp success rate with the Fetch robot in simulated environments. By integrating trajectory prediction with Recursive Least Squares and effective control strategies, we’ve created a robust system for grasping in dynamic scenarios.

Our experiments provide valuable insights into areas for optimization, such as reducing time delays in grasping. This research has significant implications for automated systems like conveyor belt sorting, where precision and efficiency are essential.

Looking ahead, we plan to enhance the system’s adaptability by exploring non-linear object paths, improving perception techniques, and developing more sophisticated control strategies. These advancements will contribute to more versatile and efficient automation solutions in dynamic environments.

<div style="font-size: 1em; font-weight: bold; text-align: center; margin-bottom: 20px;">
"With each grasp, we're not just reaching for objects, but for the future of smarter, more agile robotics."
</div>


