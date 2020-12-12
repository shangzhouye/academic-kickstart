---
title: Autonomous Disinfection Robot
summary: Built a full-stack disinfection robot with perception, localization, mapping, and navigation capability.
skills: "**Skills - ROS, Mask R-CNN, Image-LiDAR Fusion, SLAM**"
tags:
date: "2000-01-01T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Autonomous Disinfection Robot
  focal_point: Smart

links:
- icon: github
  icon_pack: fab
  name: Github Repository
  url: https://github.com/shangzhouye/disinfection-robot-ros
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

_Skills - ROS, C++, Detectron2, Instance Segmentation, Image-LiDAR Fusion, SLAM_

## Demo

{{< youtube Hjzabal8oYw >}}

## Overview

As COVID-19 spreads across the world, disinfecting surfaces on a regular basis is important for reducing the spread of the infectious disease. An autonomous robot can operate such no-touch disinfection with less operating cost, and minimize the risk for people. In this project, I built a full-stack disinfection robot with perception, localization, mapping, and navigation capability. The robot is able to classify and localize tables/desks/chairs, as well as to detect and track people in an indoor environment. After a table/desk/chair being used by a human, the robot will approach the table/desk/chair to do the disinfection.