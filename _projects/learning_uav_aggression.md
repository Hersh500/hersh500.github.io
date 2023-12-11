---
title: "Learning UAV Flight Aggression under Map Uncertainty"
collection: projects
permalink: /project/learning_uav_aggression
---
{% include base_path %}

Abstract: Fast autonomous flight through cluttered environments is an active re- search problem involving challenges in state estimation, localization, con- trol, and planning. State-of-the-art algorithms in these respective fields still pose limitations in computation time and complexity, rendering a typ- ical modular pipeline unusable at high speeds unless specifically tuned for the hardware setup. Furthermore, motion blurred sensor information can result in uncertain local map and obstacle information which can be risky in fast flight. We propose a learning based local planner that commands high-level control actions based on an approximation of local map un- certainty calculated directly from an onboard camera. 

Experiments were done in a photorealistic simulation environment with a standard configu- ration quadrotor. The reinforcement learning framework avoids an over- engineered reward function by only including positive rewards for for- ward flight and penalties for collisions. Current results achieve marginally higher task success rate when an estimate of the local map uncertainty is provided to the learner, and also variations in the drone’s velocity when noise is added to the depth image. Further experimentation and analy- sis is necessary to fully understand these difference in behavior and their utility.

<iframe src="/files/learning_uav_aggression.pdf" width="100%" height="500" frameborder="no" border="0" marginwidth="0" marginheight="0">
</iframe>
