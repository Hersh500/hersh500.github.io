---
title: "Fast Footstep Planning on Uneven Terrain Using Deep Sequential Models"
collection: publications
permalink: /publication/fast-footstep-planning
excerpt: ''
date: 2022-05-23
venue: 'International Conference on Robotics and Automation'
citation: 'H. Sanghvi, C.J. Taylor. &quot;Fast Footstep Planning on Uneven Terrain Using Deep Sequential Models&quot; in <i>International Conference on Robotics and Automation</i> 2022.'
link: "https://arxiv.org/abs/2112.07080"
---
[arXiv link](https://arxiv.org/abs/2112.07080)

Abstract: One of the fundamental challenges in realizing the potential of legged robots is generating plans to traverse challenging terrains. Control actions must be carefully selected so the robot will not crash or slip. The high dimensionality of the joint space makes directly planning low-level actions from onboard perception difficult, and control stacks that do not consider the low-level mechanisms of the robot in planning are ill-suited to handle fine-grained obstacles. One method for dealing with this is selecting footstep locations based on terrain characteristics. However, incorporating robot dynamics into footstep planning requires significant computation, much more than in the quasi-static case. In this work, we present an LSTM- based planning framework that learns probability distributions over likely footstep locations using both terrain lookahead and the robot’s dynamics, and leverages the LSTM’s sequential nature to find footsteps in linear time. Our framework can also be used as a module to speed up sampling-based planners. We validate our approach on a simulated one-legged hopper over a variety of uneven terrains.'
