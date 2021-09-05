---
layout: page
title: Projects
permalink: /projects/
published: true
---

Following is a list of projects that I have worked in.

- [**Taskwarrior - Google Calendar Sync**](/projects/taskw-gcal-sync)
- [**Aerodynamic and Control Analysis of J35 Draken**](https://github.com/bergercookie/Flight-Mechanics)

  A very interesting project that I took up during the _Flight Mechanics_
  course of my ERASMUS experience in KTH.

- [**Pattern recognition and Line-Follower robot: DRK8080**](https://www.best.eu.org/event/details.jsp?activity=afdp71v)
- [**Thermal Turbomachines - Computational Project**](https://github.com/bergercookie/Turbomachines-Project)

  First real project that I undertook using _Python_

- [**Pump3000: A Graphical User Interface for Cavro XP3000**](/projects/Pump3000/)
- [**ElecMicroscope2000: GUI for arduino-driven electrical microscope motors**](/projects/ElecMicroscope2000/)
- [**SpermProject**](http://biotech-ntua.wikispaces.com/Project_20152016_Spermodiagram)

  - Design the hardware and software for a sperm-test device. The
    goal of the device is to offer an in-house cost-affordable alternative
    to the costly, and often uncomfortable for the patient, procedure of
    laboratory sperm exam
  - Design in CAD the device for magnification
  - Code an android application, which is to run on the phone of the
    consumer's phone
  - Implement a client-server protocol for sending a video of the sperm
    sample to an external server for image analysis. Implemented, so that
    the computational/time requirements are independent of the consumer's
    android device. The server side module was written in Python.
  - Boilerplate code of the image analysis algorithm for extracting total
    population and sperm motility statistics from the given video
  - Information about the overall project can be found
    [here](http://biotech-ntua.wikispaces.com/Project_20152016_Spermodiagram)
    while the code is can be accessed via Github.

  Relevant links:

  - [Android App](https://github.com/bergercookie/SpermProject)
  - [Spermproject_server](https://github.com/bergercookie/SpermProject_server)

- **Control of MIMO Four-Tank Process**
- **PID digital control of arduino-driven Pioneer-3DX**

- **Diploma Thesis - Investigation, design and implementation of single and multi-robot SLAM algorithms**

  - Study majority of implemented strategies in single-robot
    and multi-robot Simultaneous Localization and Mapping (SLAM).
  - Based on the aforementioned analysis, decide on implementing graphSLAM
    over other studied SLAM alternatives (particle-filtering/FastSLAM, EKF,
    EIF, etc).
  - Design and implement single-robot graphSLAM as part of my
    [Google Summer of Code (GSoC)](https://summerofcode.withgoogle.com/)
    internship for the
    [Mobile Robot Programming Toolkit (MRPT](http://mrpt.org)). Algorithm
    utilizes laser scans and (optionally) odometry measurements while the
    design is easily extensible to other types of sensors (3D point clouds,
    visual etc.). A robust loop-closure scheme based on the
    [work of Olson](https://april.eecs.umich.edu/pdfs/olson2009ras.pdf)
    was also implemented. Code is successfully incorporated in the MRPT
    codebase.
  - Added wrapper code for running graphSLAM in an online (real-time)
    fashion. ROS was used as the middleware for the inter-process
    communication, data exchange. Wrapper classes are available from the
    [mrpt_slam github repository](http://github.com/mrpt-ros-pkg/mrpt_slam)
  - Extended graphSLAM code to the multi-robot case using a variation of the
    algorithm presented by Lazaro et al.,
    [here](webdiis.unizar.es/~mtlazaro/papers/Lazaro-IROS13.pdf)
  - Intra-robot communication was implemented using the multi-master ROS
    package (multicast protocol) while the algorithm was tested in the _Gazebo_
    simulator
  - Algorithm is currently under testing in real-time multi-robot setup.

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/Pv0yvlzrcXk/0.jpg)](https://www.youtube.com/watch?v=Pv0yvlzrcXk)

Single-robot graphSLAM Demo

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/4RKS2jrvsYE/0.jpg)](https://www.youtube.com/watch?v=4RKS2jrvsYE)

Multi-robot graphSLAM Demo
