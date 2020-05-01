---
title: Design of Chassis for a Single-Seater Race Car
summary: Designed a chassis structure that complies with design rules.
skills: Skills - FEA, ANSYS, SolidWorks
tags:
date: "2018-08-01T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption:
  focal_point:

links:
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

*Skills: FEA, ANSYS, SolidWorks, Pareto Efficiency*

## Project Overview:

This project is to design a tubular steel space frame chassis structure for a single-seater race car and comply with design rules. 

![](https://www.dropbox.com/s/ijezf7m2bi1kuhv/SkxpMBnzH_SyE3xIhzS.png?dl=1)

The design also has to satisfy three load cases (torsional stiffness, bump, and frontal impact) and be as lightweight as possible. The conceptual design was generated in SolidWorks, and ANSYS FEA was used to optimize the designs through an iterative process.

## Design Rules:

Some of the major design rules include:

-   The rear chassis tubes should terminate at the corners on the front face of the engine plate. There should be no tubes directly linking these points and overlapping the engine plate.
-   The bottom of your lower cockpit tubes (with cross-section applied) must be at least as low as the bottom of the driver.
-   It is required to connect the four front suspension points on each side with a four-tube box and a single diagonal cross either way. All must be a minimum of 25mm diameter and 1.5mm wall thickness.
-   The chassis must include a Shoulder Harness Mounting bar, which is a horizontal tube attached to either the main roll hoop or its support tubes. The bar must be within ± 100 mm of the top surface of the driver's shoulders in side-view.

Three load cases are:
-   Torsional Stiffness
	-   The chassis should have a torsional stiffness of 2500 Nm/deg or higher.
-   Bump 
	-   -25,000 N applied vertically down at the two lower roll hoop nodes;
	-   10,000 N applied vertically up at the front suspension nodes;
	-   Not experience material yield given a Safety Factor of 2.5 (i.e., below 100 MPa).
-   Frontal Impact:
	-   25,000N applied at the front four bulkhead nodes, acting horizontally towards the back of the car;
	-   Not experience material yield given a Safety Factor of 2.5 (i.e., below 100 MPa).
    
The design is required to satisfy all these criteria while being as lightweight as possible.

## Design Evolution:

Our design went through 17 iterations in total. The chart below shows the weight, max stress, and torsional stiffness for each iteration:

Legend:

-   Weight of the chassis in kg x 10 (in Blue Dots)
-   Max Stress in Mpa (in Red Dots)
-   Torsional Stiffness divided by 10 in Nm/deg (in Green Dots)

![](https://www.dropbox.com/s/y5jzdferz0as4bn/SkxpMBnzH_Bk3GeUnMH.png?dl=1)

The teamwork went through a cyclic, iterative process of designing, analyzing, and refining. Initially, we each explored our own ideas to form the initial concepts. We chose one of them as our first concept. After that, each team member focused on a specific area to investigate. Then, the team worked closely to integrate and refine each design iteration. Iteration 13 eventually became our focus as it had the best chances of being light and complying to rules. A full rule check was completed, and further optimization took place to conclude iteration 17 as our final design.

## Final Design:

The chassis design includes:

-   Front bulkhead
-   Front hoop
-   Main roll hoop
-   Rear bulkhead (Engine plate)
-   Main roll hoop bracing
-   Dash hoop supports
-   Main roll hoop bracing support

Attached is our final design:

![](https://www.dropbox.com/s/k3u0im7gaoyn7um/SkxpMBnzH_SynmMvnGr.png?dl=1)

Torsion load case (ANSYS FEA):

![](https://www.dropbox.com/s/4mjxete55mav29j/SkxpMBnzH_BkAvMw2Gr.png?dl=1)

Bump load case (ANSYS FEA):

![](https://www.dropbox.com/s/zbr5p092r04sacr/SkxpMBnzH_B13aMPnMr.png?dl=1)

Frontal impact load case (ANSYS FEA):

![](https://www.dropbox.com/s/x36lmz8pqsx8p5z/SkxpMBnzH_S1cmmD3zB.png?dl=1)

Some insights we noticed regarding the design:
-   Rearward main hoop design allows the bracing to comply with the rule while saving weight.
-   Decreasing the width of the chassis can reduce the tendency to buckle during a crash.
-   Thin wall tube is sometimes more efficient against bending.
-   Reduce rigidity in the front section can generate a more even stress distribution.
-   Uniform stress distribution is of crucial importance to a lightweight and high-performance chassis structure.
    

## Acknowledgment:

This project was the teamwork of group No. 25 - Lexus (MEC4407, Semester 2, 2018) at Monash University.