---
title: Mobile Manipulation
summary: Pick and place a block using the youBot mobile manipulator.
skills: Skills - Trajectory Generation, Omnidirectional Robot
tags:
date: "2019-12-11T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link:

image:
  caption:
  focal_point:

links:
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---

*Skills: Trajectory Generation, Forward Kinematics, Jacobian, PI controller, Omnidirectional Robot*

## Demo:

![demo](https://github.com/shangzhouye/portfolio-website/blob/master/content/project/mobile_manipulation_capstone/demo.gif?raw=true)

For a video of the robot in action, please watch this video.

{{< youtube _jVVm3mORgU >}}

## Overview:

The project includes:

- Simulation: Calculate the configuration of the robot given the robot's current configuration and joint speeds. It includes an omnidirectional robot odometry which calculate the base configuration (x, y, phi) given the wheel speed.

- Trajectory generation: Generate a smooth reference trajectory for the end-effector. The trajectory generated is a screw motion about a constant screw axis with fifth-order polynomial time scaling

- Feedforward and Feedback controller: A PI controller was designed to follow the desired end-effector trajectory using five arm-joints and four base-wheels. The equation of the control law is shown below. The end-effector twist $V$ calculated is then turned into the commanded wheel and arm joint speeds using the pseudoinverse of the mobile manipulator Jacobian.

![](https://github.com/shangzhouye/portfolio-website/blob/master/content/project/mobile_manipulation_capstone/equ.png?raw=true)

This project is the final project of ME449: Robot Manipulation, Northwestern University, Evanston.

## Modules:

*The code is removed due to copyright of the capstone. Please contact me if you are interested in this project.*

The program takes the initial cube position, desired final cube position, the actual initial configuration of youBot, and reference initial configuration of youBot as inputs. It outputs a `csv` file which drives the youBot picking and placing the block, and the end-effector error as a function of time.

The youBot has nine degrees of freedom in total, where J1 to J5 are the arm joint angles, and W1 to W4 are the four wheel-angles. The figure below shows the the robot at its home configuration and the frames {s}, {b}, {0}, and {e}.

![](https://github.com/shangzhouye/portfolio-website/blob/master/content/project/mobile_manipulation_capstone/Yb-book.png?raw=true)

The project is divided into four python scripts:

- `ref_traj.py` would generate the desired reference trajectory for the end-effector.
- `feedback.py` defines the FeedbackControl class:
  - Calculate the command with feedforward and feedback components
  - Calculate the jacobian matrix of the manipulator
  - Calculate the joint speeds for controlling the mobile manipulator
- `simulator.py` will do the simulation. 
  - Given the current configuration and joint speeds, it will calculate the next configuration.
- `run.py` would use all other python scripts to generate the trajectory.

## Enhancement implemented

- Singularity avoidance
    - Ignore requested twist components in directions that is near singularity to avoid unreasonable large joint speeds.
- Add joint limits to avoid self-collision.
- Acceleration limis
    - Add maximun acceleration limitation to avoid jerky motion.

## How to run the code:

- It depends on the modern robotics library: [Link](https://github.com/NxRLab/ModernRobotics)
- The scripts are written in Python 2.7
- Run the script `ref_traj.py`, then run `run.py`.
- The results can be demontrated in v-rep simulation.