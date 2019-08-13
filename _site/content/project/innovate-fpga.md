+++
title = "Intel Innovate FPGA"
date = 2018-09-18T15:56:58-05:00
draft = false

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["machine-learning", "computer-vision"]

# Project summary to display on homepage.
summary = "Semi-finalist of [Innovate FPGA](http://www.innovatefpga.com/cgi-bin/innovate/teams.pl?Id=AS027). Accelerating a neural network with an FPGA (DE10-Nano) for detection of bicyclists at intersections."

# Optional image to display on homepage.
image_preview = "intel_fpga.png"

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Does the project detail page use source code highlighting?
highlight = true

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
[header]
image = ""
caption = ""

+++

![image](/project/intel/intel_fpga.png)

_This is my team's [semi-finalist submission](http://www.innovatefpga.com/cgi-bin/innovate/teams.pl?Id=AS027) for the Intel Innovate FPGA 2018 Challenge. I worked with two NVIDIA employees for 4 months designing and implementing the project on a DE10-Nano._

There are a number of problems that still plague traffic intersections. For example, during the night, one still has to wait for the light to turn green in spite of being alone at the crossing. Or when riding a motorcycle or a bicycle, the automated lights don’t register a rider and one is left to wait until a car (with a larger metal footprint) arrives, etc. We propose a method to increase efficiency and safety of traffic, especially during off hours.

We use the Intel DE10-NANO board and one or more existing digital cameras placed at traffic intersections. We then run a trained neural network on our video feed, and correct or change the usual traffic patterns through a connection to traffic infrastructure.

We plan a proof of concept with the following goals and motivators:
1. If there exist vehicles on a road waiting in a no traffic situation, alter lights accordingly
2. Help existing intersection sensors to detect motorcycles and bicycles as traffic
3. If a car is predicted to run a red light, alter traffic optimally for safety

More scenarios may easily be added later due to FPGA’s configurable nature.


## High-level Project Description

### Motivation

The purpose of this project is to increase traffic safety and efficiency for all vehicles on the road. Our project was inspired by an accident that a friend of had while crossing an intersection on his bicycle, unnoticed by both the traffic and intersection signal. This and several other kinds of accidents could be completely avoided with our solution.

### Method

We begin by feeding the traffic camera feed into a DE10 board. A YOLO classifier is applied that recognizes and classifies objects located at the line where vehicles stop [1]. We classify cars, motorcycles and bicycles. Depending on the installation configuration, time of day and individual setup, the DE10 processor will issue hints to the existing intersection system to improve traffic flow.

We are using several inexpensive and widely available IoT cameras. Since the resolution required depends on a combination of factors, such as distance to target or orientation to street, we can swap cameras and use the most appropriate combination in a final solution.

The following cameras are used to prototype our solution:

* OV7675 (0.3MP or 640x480)

* OV9650 (1.3MP or 1300x1028)

* OV5640 (5MP or 2592x1944)

These cameras are connected to IO ports on the board leading to the FPGA, which sequences the incoming image stream and does optional pre-processing before storing them onto the DRAM.

The ARM CPU processes the images, and detects the objects we consider at a given intersection using our trained network. Finally, it generates hints to supply the intersection computer with using its own I/O and appropriate protocol. Since this is all code and not hardware, we can implement and modify the protocols to suit individual installations.

We can meet the bandwidth necessary to do the image processing and inference on the FPGA while keeping the more mundane tasks to execute on the CPU. The flexibility of the board and the ease of configuration enables a rapid prototyping and debugging cycle.

The scope of our project is limited to the three motivators outlined in the general description. However, If we were to come up with additional solutions, deploying them would be possible given FPGA’s dynamic functionality. We would simply load the new trained network and hint generator, as well as a new FPGA configuration, without the need to change hardware.

We plan to train our neural network to recognize cars, bicycles, and cars using the ImageNet database, tensorflow, and an auxiliary training machine. We can then utilize tensorflow for mobile devices, which may allow for tractable computation time given our limited runtime hardware.

We also plan to accelerate our neural network implementation with efficient FPGA structuring. This will offload computation to the FPGA, which we can tailor to have an efficient execution pipeline for the specific network we choose to implement, be it YOLO or a newer, state of the art solution.

The scope of our project is limited to the three motivators outlined in the general description. However, If we were to come up with additional solutions, deploying them would be possible given FPGA’s dynamic functionality. We would simply load the new trained network and hint generator, as well as a new FPGA configuration, without the need to change hardware.

In practice, this solution can use one of ~4,000 existing intersection cameras to determine if vehicles are waiting [2]. Using FPGA’s natively broad I/O, we can accept the camera feeds without specialized input hardware, and across different camera models.

 
### Expanding I/O

This project uses cameras as an input image stream to our Intel FPGA board. The board provides enough GPIO pins to connect the cameras and enough bandwidth to consume/process all video data in parallel without frame drops. Using FPGA I/O, we are able to accept all kinds of camera input, at any resolution. This would be helpful given a real world implementation where we use existing camera infrastructure.

Once deployed, this solution could also as easily be reconfigured and improved as needed.

### Adapting to Changes and Boosting Performance

FPGA’s also facilitate deep learning’s ever evolving nature. New methods are constantly being created to train and better exploit neural networks, and state of the art methods are rendered obsolete within a few months. With solely software, we can remotely update our network and corresponding FPGA configuration. We can also leverage FPGA’s for large scale linear algebra operations.

### Block Diagram
![Block Diagram](/project/intel/block.png)

### References
[1] YOLO is a specific neural network architecture which works well with video feeds and low powered systems due to its inherent computational feasibility.

[2] 4,150 traffic cameras: https://www.vox.com/a/red-light-speed-cameras
