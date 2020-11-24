---
title: EKF SLAM on Turtlebot3
summary: Built EKF SLAM with landmark detection using laser scanner.
skills: "**Skills - EKF, Odometry, C++, Unit Testing, CMake**"
tags:
date: "2020-03-15T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: 
  focal_point: 

links:
- icon: github
  icon_pack: fab
  name: Github Repository
  url: https://github.com/shangzhouye/EKF-SLAM-on-Turtlebot3
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides: example
---

*Skills - EKF SLAM, Unsupervised Learning, Odometry, ROS, TF, URDF, C++, Unit Testing, CMake*

## Demo

This repository builds feature-based EKF SLAM on Turtlebot3 from scratch. The demo below shows the algorithm in action (2x speed).

![](https://github.com/shangzhouye/EKF-SLAM-on-Turtlebot3/blob/public/figures/slam_in_control.gif?raw=true)

- Trajectories
  - The pink path shows the odometer estimated path.
  - The green path is the groundtruth.
  - Yello path is the SLAM result.
- Landmarks
  - Blue landmarks are groundtruth.
  - Green landmarks are measurements.
  - Indigo landmarks show where the SLAM algorithm thinks their positions are.

The figure below shows the result of the landmark detection algorithm using a 2D laser scanner.

![](https://github.com/shangzhouye/EKF-SLAM-on-Turtlebot3/blob/public/figures/landmark_detection.gif?raw=true)

## Overview

### Modules

This system has the following major components:

- A **2D Lie Group** library for differential drive robots with complete unit testing
- A waypoint following **feedback controller**
- **Turtlebot3 URDF** built from scratch for Gazebo simulation
- **Gazebo plugins** to control the robot and return the groundtruth data for evaluation
- An **odometer** that estimates robot states based on encoder reading
- **Turtlebot3 interface** that controls the motors with given velocity command
- **Feature detection** algorithm that identifies landmarks using a 2D laser scanner
- **EKF SLAM** algorithm that estimates robots states

### Packages

Six packages are built in this project.

- `nuturtle_description` develops Turtlebot3 URDF, and visualizes the wheeled robot in `Rviz`
- `nuturtle_gazebo` includes Gazebo plugins to simulate the robot in `Gazebo`
- `nuturtle_robot` implements the Turtlebot3 interface, and includes the test node for the odometer on the real robot
- `nuturtle_slam` consists of the feature detection algorithm and the EKF SLAM algorithm
- `tsim` implements the waypoints following feedback controller
- `rigid2d` is the 2D Lie Group library, including SO(2), SE(2) calculations, the odometer, and the fake encoder

## Algorithms

### Odometry

The video below shows the testing of the odometer in the real world.

![](https://github.com/shangzhouye/portfolio-website/blob/master/content/featured-projects/ekf_slam/nuturtle_real_world.gif?raw=true)

### Landmark Detection

Landmarks in the environment are cylinders. Therefore, the feature detection pipeline includes points clustering, circle fitting, and circle classification. The 2D laser scanner results are clustered into groups based on a distance threshold. Clusters with fewer than 4 points are then discarded to enhance the robustness of the circle fitting algorithm.

A circle fitting algorithm [1] was implemented to find the position and radius of landmarks. Circles identified with too large radius are removed. A circle classification algorithm [2] was also applied to help avoid false positives.

### EKF SLAM

The implemented EKF SLAM algorithm can be found [here](https://nu-msr.github.io/navigation_site/slam.pdf).

## Future Work

- Data association is currently assumed to be known. SLAM with unknown data association can be achieved by calculating the Mahalanobis Distance

## Reference

[1] A. Al-Sharadqah and N. Chernov, Error Analysis for Circle Fitting Algorithms, Electronic Journal of Statistics (2009), Volume 3 p 886-911

[2] J. Xavier et al., Fast line, arc/circle and leg detection from laser scan data in a Player driver, ICRA 2005