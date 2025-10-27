---
title: "Sim2Real Quadrotor RL Policy with Accelerated RotorPy"
collection: projects
permalink: /project/rotorpy_rl
order: 1
---
{% include base_path %}

For the past few years, a primary research interest of mine has been how we can adapt control policies for robots (both learned and not) to new "situations". These could be new environments (i.e. moving from indoors to outdoors), new robots (i.e. deploying the same controller on two quadrotors with different masses), or new tasks (i.e. prehensile vs. non-prehensile manipulation). I recently investigated the last question with my colleague [Spencer Folk](https://spencerfolk.github.io)  in the case of trajectory tracking with quadrotors: do we need to tune our controllers differently if we change the trajectory? 

Our answer to this question involved trying a feedback controller with differently tuned parameters on a wide variety of different trajectories, observing how the tracking performance varied, and using machine learning to build a model of that relationship. Due to the variety of trajectories that the drone could be asked to follow (different shapes, speeds, etc.), we needed to generate a large amount of data to show the model how all combinations of gains interacted with different trajectories. For previous projects in this vein, we had used RotorPy, an aerial robotics simulator written using NumPy. To make data collection for this project feasible, we explored how we could accelerate the RotorPy simulation.

We took advantage of vectorization and rewrote RotorPy's simulation backend, controller, and trajectory generators in PyTorch [to obtain a speedup of over 25X purely on CPU (and even more using multithreading or the GPU!)](https://github.com/spencerfolk/rotorpy/pull/17), which made data collection for our project ([which you can read about here](https://drive.google.com/file/d/12A1wQHf09_PFNq8WHvCGY-lR4oWCnFFP/view)) much faster.

We also realized that the accelerated version of RotorPy would be great to use to train an RL policy for quadrotor flight - especially given the sim2real transfer we had been able to achieve with RotorPy before. The policy receives an observation containing the position error, velocity error, the orientation, and body rates (all obtained using a motion capture system). The observation also includes a horizon of future position commands from the trajectory.  The policy outputs a desired collective thrust and angle command, which are tracked with low-level controllers onboard the quadrotor. 

With the accelerated simulation, we were able to train this policy using PPO for 4 million timesteps in under 3 minutes on my M3 MacBook Air. We achieved a surprisingly robust policy that successfully transferred to a real CrazyFlie Brushless without any finetuning on real data! In this video, our collaborator Kashish perturbs the quadrotor by flapping a large piece of foam to create a gust, and also pulls the drone out of place. In both cases, the policy smoothly recovers!

<iframe width="560" height="315" src="https://www.youtube.com/embed/ygEcPqkt3oY?si=-quSxk4wakwfVICJ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Even though RotorPy goes beyond other physics simulators by simulating aerodynamic forces and motor saturation constraints, getting the policy to transfer still required:
1. Careful reward tuning to ensure the policy outputted smooth actions (otherwise, it has a tendency to produce very jittery actions that work in sim but don't transfer well)
2. Domain randomization in simulation over the quadrotor's mass, thrust coefficient, inertia tensor, and motor latency.
3. Further randomization of the low-level attitude controller feedback gains in simulation. We suspect that the low-level attitude controller behaves very different on the real quadrotor versus the simulated one, so exposing the policy to variations in the attitude controller makes it more robust to this gap.

We also trained a policy for trajectory tracking, which also trains in a few minutes:

<iframe width="560" height="315" src="https://www.youtube.com/embed/a8HOyCkUV4c?si=4pDqmIQyZ36KzyH1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Although not the most academically novel, we were excited about these results due to the exceptionally fast training times that we achieved on CPU and zero-shot sim2real transfer. This made iterating on experiments much easier, as we could fiddle with simulation/training hyperparameters and then try the resulting policy on the real drone in under 5 minutes.

Of course, the classic geometric controller for quadrotors is more than sufficient in the scenarios that we tested. However, the promising results so far open up the possibility to train policies in more difficult tasks where the GC falls short, such as flying in extreme wind using the IMU (which RotorPy already models!), flying aggressive trajectories where drag becomes significant, and executing acrobatic maneuvers such as backflips.
