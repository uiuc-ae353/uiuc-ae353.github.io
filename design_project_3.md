---
layout: page
title: Design Project 3 - Drone
nav_order: 3
math: katex
---

## Design Project \#3 (Drone)

### System

The third project that you will complete this semester is to design, implement, and test a controller that enables a quadrotor - aka "the drone" - to race through rings from start to finish without crashing:

![CMG Image](https://raw.githubusercontent.com/uiuc-ae353/ae353-fa24/main/assets/Drone.png)

### Context

Imagine that, working as a control systems engineer, you have been hired by [Tiny Whoop](https://www.tinywhoop.com/) to design a controller for a small-scale drone. In particular, imagine that Tiny Whoop intends to market this drone to amateur pilots for racing (e.g., see their [alley cat coffee cup invitational race](https://youtu.be/jnXgoRxyVqU?t=283)). Your job is to show that this drone — with a suitable controller — is capable of high-speed, agile flight.

As you work on this project, we encourage you to think about other possible applications of drones such as these. [PowderBee](https://snowbrains.com/new-avalanche-rescue-drone-in-the-works/) from [Bluebird Mountain](https://www.springwise.com/innovation/sport-fitness/powderbee-drone-avalanche-rescue/), for example, is intended to find avalanche victims (i.e., people buried under thick snow) quickly so they can be rescued before succumbing to asphyxiation, hypothermia, or other injuries — every second counts in rescue applications, just as for racing drones.

### Model

The motion of each drone is governed by ordinary differential equations with the following form:

$$
\begin{bmatrix}
\dot{p}_x \\
\dot{p}_y \\
\dot{p}_z \\
\dot{v}_x \\
\dot{v}_y \\
\dot{v}_z \\
\dot{\phi} \\
\dot{\theta} \\
\dot{\psi} \\
\dot{\omega_x} \\
\dot{\omega_y} \\
\dot{\omega_z}
\end{bmatrix}
= f
\begin{bmatrix}
p_x, p_y, p_z, v_x, v_y, v_z, \phi, \theta, \psi, \omega_x, \omega_y, \omega_z, \tau_x, \tau_y, \tau_z, f_z
\end{bmatrix}
$$

In these equations:

- $$ p_x $$: the $$x$$ position (m)
- $$ p_y $$: the $$y$$ position (m)
- $$ p_z $$: the $$z$$ position (m)
- $$ v_x $$: the linear velocity along the body-fixed $$x$$-axis (m/s)
- $$ v_y $$: the linear velocity along the body-fixed $$y$$-axis (m/s)
- $$ v_z $$: the linear velocity along the body-fixed $$z$$-axis (m/s)
- $$ \phi $$: the roll angle (rad)
- $$ \theta $$: the pitch angle (rad)
- $$ \psi $$: the yaw angle (rad)
- $$ \omega_x $$: the angular velocity about the body-fixed $$x$$-axis (rad/s), which points forward
- $$ \omega_y $$: the angular velocity about the body-fixed $$y$$-axis (rad/s), which points left
- $$ \omega_z $$: the angular velocity about the body-fixed $$z$$-axis (rad/s), which points up
- $$ \tau_x $$: the net torque about the body-fixed $$x$$-axis (N·m)
- $$ \tau_y $$: the net torque about the body-fixed $$y$$-axis (N·m)
- $$ \tau_z $$: the net torque about the body-fixed $$z$$-axis (N·m)
- $$ f_z $$: the net force along the body-fixed $$z$$-axis (N)

A symbolic description of these equations of motion is provided with the project code in the repository.

The actuators that produce the net torques $$ \tau_x, \tau_y, \tau_z $$ and net force $$ f_z $$ are the four rotors on the drone, each of which is driven by an electric motor. These rotors can spin in only one direction and have minimum and maximum speeds. These bounds limit the torques and forces that can actually be produced.

Sensors provide a noisy measurement of the position in space of four markers:

- `kwargs["mocap_1"]`
- `kwargs["mocap_2"]`
- `kwargs["mocap_3"]`
- `kwargs["mocap_4"]`

These markers are positioned over each rotor of the quadrotor. This is the sort of measurement that would be provided by a standard commercial motion capture system (e.g., [OptiTrak](https://optitrak.com) or [Vicon](https://www.vicon.com)). A symbolic description of the sensor model is provided with the project code repository.

In addition to these marker position measurements, your controller is also provided the following information:

- The position (`kwargs["next_gate"]`) of the center of the next gate that the drone needs to pass through
- The vector (`kwargs["dir_gate"]`) normal to this next gate (i.e., pointing through its center)
- A flag (`kwargs["is_last_gate"]`) that indicates if this next gate is the last gate, a.k.a., the "finish"
- The position (`kwargs["pos_others"]`) of all other drones

The `ae353_quadrator-template.ipynb` file simulates the motion of this system and also derives the dynamic model and sensor model in symbolic form (`ae353_quadrotor-EoM.ipynb`).

The goal is to race as fast as possible from the start to the finish line, passing through all the gates in between.

### Tasks

First, you must do **all** of the following things:

- Define a requirement and a verification, just as you did in the previous design projects.
- Linearize the equations of motion and a sensor model (the sensor model is straightforward,
  ask in Canvas if you have questions). Verify that the equilibrium point you
  picked is indeed an equilibrium point.
- Show that the linearized system is both controllable and observable.
- Design a stable controller and a stable observer with respect to the linearized system.
- Add trajectory tracking to enable movement between rings. This could be something
  as simple as switching the equilibrium point to the latest target ring center. However,
  you could always come up with better ways to do this – gradually changing your target
  point to the center of next target ring is one particular option.
- Implement the controller and observer and test them in simulation.
- Access the stored data from the simulation and create at least one plot that shows
  your trajectory from origin to target -- your plot should also have the the rings that it passed through (these rings can be very simple 3 dimensional torus). Code for sample plots is provided in the DroneDemo.ipynb notebook. **You are also required to submit a video showing your drone moving from the initial position to the final goal ring.**
- Your report must contain a section (in words) about how the controller was designed -- make sure to include all relevant mathematical formulations.

### Bonus Questions

#### Bonus 1: Early submission:

**If you submit all your deliverables 2 days before the deadline (i.e. by 12/04/2024, 11:59PM), you will be given a full 7% bonus credit.**
_Please note:_ If you choose to submit before time, please do not submit a second time after Friday -- if you choose to, please email the TA (gokulp2@illinois.edu) or else, only your first submission will be marked.

#### Bonus 2: Minimizing Time to Rings

Once you have a working control design, you can turn your attention to the following additional
analysis for bonus points:

- Designing a controller that can reach the last ring through all the 5 rings – you should
  submit working code for verification and also mention this addition work in the report
  under a title “Bonus Work”.
- The goal in this project is to minimize the time your drone takes to reach the last
  ring.
  <span style="color:red">Please record the timings if the drone is successful in reaching the last state, and include them in your report. We will have a leaderboard (Top 7) for the fastest drone to reach the last ring on the website!</span>. If you do not want to be included in the leaderboard, please email the TA (gokulp2@illinois.edu).

### Deliverables

We will use Canvas for submitting design projects and the video file. You must create a compressed folder (.zip) titled DP3-submission with the
code and the report in the format described below and submit by 11:59PM CST on December
6 (early submission bonus by 11:59 PM, December 4).

#### Code:

This code will satisfy the following requirements:

- It must be in a folder called code (lower case).
- It must include a single notebook called GenerateResults.ipynb that could be used
  to reproduce all of the results that you show in the report.
- It must include all the other files (with the right folder structure) that are necessary
  for GenerateResults.ipynb to function.
- It must not rely on any dependencies other than those associated with the conda
  environment described by ae353-bullet.yml.

#### Report:

- It must be a single PDF document that conforms to the guidelines for [Preparation of Papers for AIAA Technical Conferences](https://www.aiaa.org/events-learning/events/Technical-Presenter-Resources). In particular, you **must** use either the [Word](https://www.aiaa.org/docs/default-source/uploadedfiles/aiaa-forums-shared-universal-content/preparation-of-papers-for-technical-conferences.docx?sfvrsn=e9a97512_10) or [LaTeX](https://www.overleaf.com/latex/templates/latex-template-for-the-preparation-of-papers-for-aiaa-technical-conferences/rsssbwthkptn#.WbgUXMiGNPZ) manuscript template.
- It must have a descriptive title that begins with "DP3" (e.g., "DP3:[Title]").
- It must have the author name and affiliations.
- It must tell a story that shows you have found and explored something that interests you.
- You may organize your report however you like, but it should at the minimum have these sections:
  - _Abstract._ Summarize your entire report in one short paragraph.
  - _Nomenclature._ List all symbols used in your report, with units.
  - _Introduction._ Prepare the reader to understand the rest of your report and how it fits within a broader context.
  - _Theory._ Derive a model and do control design.
  - _Experimental methods._ Describe the experiments you performed in simulation in enough detail that they could be understood and repeated by a colleague. At minimum, this section should clearly define your requirement and verification.
  - _Results and discussion._ Show the results of your experiments in simulation (e.g., with plots and tables) and discuss the extent to which they validate your control design - in particular, the extent to which they verify your requirement. As always, remember to [focus on establishing limits of performance](#segbot-your-tasks).
  - _Conclusion._ Summarize key conclusions and identify ways that others could improve or build upon your work.
  - _Acknowledgements._ Thank anyone outside your group with whom you discussed this project and clearly describe what you are thanking them for.
  - _References._ Cite any sources, including the work of your colleagues.
- It should preferably be about 5 pages in length — it will be hard to show off your work with anything shorter, and it will be hard to keep readers’ attention with anything longer.

#### Video:

- You are also required to submit a video showing your drone moving from the initial position to the final goal ring.
- There will be a separate Canvas submission section for video submission.
- You can record the video using a screenrecorder or use PyBullet's in-built video recorder, the code for the same is provided in the template file.

#### Submission Instructions (for code and report)

To make it easier logistically, there will be _three_ assigned submissions for this project on Canvas. Please submit the following _separately_:

- Report: Submit a pdf version of your report
- Code: Compress your code into a zip file and submit the zip file.
- Video: Submit your video as a .mp4 file.

### Evaluation

Your work will be evaluated based on completion of the tasks and the resulting description
of the results, on submission of working code, video and your report being formatted correctly.

_Please note:_ You will be allowed only _one_ late submission for this project.

### Frequently asked questions

##### How do I get started?

The first thing you should do is update your local copy of the repository with the DesignProblem02 file, to do this, please follow the [installation instructions](https://github.com/uiuc-ae353/ae353-fa23/wiki/Installation-instructions), very specifically, follow the 'Do this every time' section and run the command

```
git pull
```

This will update your local copy of the repository with the code for Design Problem 02. Verify that you can run the simulation, and mess around a little bit with different actuator commands (e.g., constant wheel torques) to get a sense for how the system responds.

After that, if you have read the entire project description and are not sure how to proceed, then take your best guess and ask a question on Canvas. Improving your ability to get unstuck by asking a good question is an explicit goal of this course.
