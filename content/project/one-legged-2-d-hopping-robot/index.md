---
title: One-legged 2-D Hopping Robot Simulation
summary: Modeled a 2D one-legged hopping robot on a flat ground.
skills: Skills - Lagrangian Mechanics, Numerical Method
tags:
date: "2019-12-11T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: 

image:
  caption: 
  focal_point: 

links:
- icon: github
  icon_pack: fab
  name: Github Repository
  url: https://github.com/shangzhouye/one-legged-2-D-hopping-robot/
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---
*Skills: Lagrangian mechanics, impact dynamics, numerical simulations, multi-body systems modeling, Python, variational principles*

# Demo

This project models a 2D one-legged hopping robot on a flat ground.

![demo](https://github.com/shangzhouye/one-legged-2-D-hopping-robot/blob/master/demo.gif?raw=true)

# Overview

The motion includes five phases:

- Flight phase 1

    The constraint is the length of the leg is at its desired length. Currently, the desired length is set at 0.65 m with a pre-compression of 0.002 m. No external force was added at this stage.

- Touch down impact

    The robot experienced a plastic impact. Impact equations include 'change of momentum lies perpendicular to the contact surface' and 'foot arrested to the ground'. Velocity is discontinuous. There is energy loss due to the plastic impact.

- Stance phase

    The robot did a passive jump here. The constraint is that the foot is arrested to the ground. The robot took off when the leg length is at its maximum (0.65 m) and hits the mechanical stop.

- Take off impact

    Velocity is discontinuous here again. Impact equations include 'change of momentum lies perpendicular to the contact surface' and 'leg is at its maximum length'. 

- Flight phase 2

    A torque is applied to the hip joint $\theta$ to rotate the leg forward and prepare for the next jump.

A few assumptions were made for simplicity:

- The foot is arrested to the ground during stance (no slip).
- The robot takes off when the leg hits the mechanical stop.
- Impacts are plastic impacts.

The robot has four degrees of freedom: 

- Position of the body CoM $x$, $y$
- Orientation of the body $\theta$
  - an actuated DoF, a hip rotation torque $\tau$ is applied
- Leg length $l$

This is my final project of ME314 Machine Dynamics (Dec. 2019), NU. 

# Multi-body mechanics

This [figure](https://github.com/shangzhouye/one-legged-2-D-hopping-robot/blob/master/Figures/model.jpg?raw=true) (adapted from [2]) shows the system I'm modeling. This [figure](https://github.com/shangzhouye/one-legged-2-D-hopping-robot/blob/master/Figures/frames.jpg?raw=true) shows the frames I'm using.

Rigid body transformations:

![$g_{wa} = \left\[\begin{matrix}1 & 0 & 0 & x{\left (t \right )}\\0 & 1 & 0 & y{\left (t \right )}\\0 & 0 & 1 & 0\\0 & 0 & 0 & 1\end{matrix}\right\]$](https://render.githubusercontent.com/render/math?math=%24g_%7Bwa%7D%20%3D%20%5Cleft%5B%5Cbegin%7Bmatrix%7D1%20%26%200%20%26%200%20%26%20x%7B%5Cleft%20(t%20%5Cright%20)%7D%5C%5C0%20%26%201%20%26%200%20%26%20y%7B%5Cleft%20(t%20%5Cright%20)%7D%5C%5C0%20%26%200%20%26%201%20%26%200%5C%5C0%20%26%200%20%26%200%20%26%201%5Cend%7Bmatrix%7D%5Cright%5D%24)

![$g_{ab} = \left\[\begin{matrix}\cos{\left (\theta{\left (t \right )} \right )} & - \sin{\left (\theta{\left (t \right )} \right )} & 0 & 0\\\sin{\left (\theta{\left (t \right )} \right )} & \cos{\left (\theta{\left (t \right )} \right )} & 0 & 0\\0 & 0 & 1 & 0\\0 & 0 & 0 & 1\end{matrix}\right\]$](https://render.githubusercontent.com/render/math?math=%24g_%7Bab%7D%20%3D%20%5Cleft%5B%5Cbegin%7Bmatrix%7D%5Ccos%7B%5Cleft%20(%5Ctheta%7B%5Cleft%20(t%20%5Cright%20)%7D%20%5Cright%20)%7D%20%26%20-%20%5Csin%7B%5Cleft%20(%5Ctheta%7B%5Cleft%20(t%20%5Cright%20)%7D%20%5Cright%20)%7D%20%26%200%20%26%200%5C%5C%5Csin%7B%5Cleft%20(%5Ctheta%7B%5Cleft%20(t%20%5Cright%20)%7D%20%5Cright%20)%7D%20%26%20%5Ccos%7B%5Cleft%20(%5Ctheta%7B%5Cleft%20(t%20%5Cright%20)%7D%20%5Cright%20)%7D%20%26%200%20%26%200%5C%5C0%20%26%200%20%26%201%20%26%200%5C%5C0%20%26%200%20%26%200%20%26%201%5Cend%7Bmatrix%7D%5Cright%5D%24)

![$g_{bc} = \left\[\begin{matrix}1 & 0 & 0 & - l{\left (t \right )}\\0 & 1 & 0 & 0\\0 & 0 & 1 & 0\\0 & 0 & 0 & 1\end{matrix}\right\]$](https://render.githubusercontent.com/render/math?math=%24g_%7Bbc%7D%20%3D%20%5Cleft%5B%5Cbegin%7Bmatrix%7D1%20%26%200%20%26%200%20%26%20-%20l%7B%5Cleft%20(t%20%5Cright%20)%7D%5C%5C0%20%26%201%20%26%200%20%26%200%5C%5C0%20%26%200%20%26%201%20%26%200%5C%5C0%20%26%200%20%26%200%20%26%201%5Cend%7Bmatrix%7D%5Cright%5D%24)

![$g_{cd} = \left\[\begin{matrix}1 & 0 & 0 & 0.25\\0 & 1 & 0 & 0\\0 & 0 & 1 & 0\\0 & 0 & 0 & 1\end{matrix}\right\]$](https://render.githubusercontent.com/render/math?math=%24g_%7Bcd%7D%20%3D%20%5Cleft%5B%5Cbegin%7Bmatrix%7D1%20%26%200%20%26%200%20%26%200.25%5C%5C0%20%26%201%20%26%200%20%26%200%5C%5C0%20%26%200%20%26%201%20%26%200%5C%5C0%20%26%200%20%26%200%20%26%201%5Cend%7Bmatrix%7D%5Cright%5D%24)

Specification are listed below. The free length of the spring is $L_{UB} + L_{LB} + \delta$:

- h = 0.25           # leg CG height
- $m_b$ = 3          # body mass
- $m_l$ = 0.3        # leg mass
- $I_b$ = 0.8        # body inertia
- $I_l$ = 0.008      # leg inertia
- $L_{UB}$ = 0.25      # Upper body length 
- $L_{LB}$ = 0.15      # Lower body length 
- $\delta$ = 0.002   # Spring pre-compression
- $L_L$ = 0.5        # Rigid length of leg
- $K_S$ = 2000       # spring stiffness
- $L_d$ = $L_L$ + $L_{LB}$ # desired leg length

# Future work

- The impact update at the touch-down and take-off phases are manually set as the initial condition of the next phase. An automatic transfer can be implemented.
- The primary purpose of this project is to make the simulation using Lagrangian dynamics. No stable control law is implemented at this stage.

# Reference

- [1] Raibert, M.H. (1984). Hopping in legged systems — Modeling and simulation for the two-dimensional one-legged case. IEEE Transactions on Systems, Man, and Cybernetics, SMC-14, 451-463.
- [2] Sayyad, A., Seth, B., & Issac, K.K. (2007). Dynamics and Control of a One-legged 2-D SLOM Hopping Robot.