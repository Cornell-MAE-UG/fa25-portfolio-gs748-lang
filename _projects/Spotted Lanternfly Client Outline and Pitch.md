---
layout: project
description: Rover-Compatible End Effector for Autonomous Spotted Lanternfly Removal
fontsize: 11pt
geometry: margin=1in
papersize: letter
pagestyle: empty
header-includes:
  - \pagenumbering{gobble}
  - \linespread{0.9}
  - \addtolength{\textwidth}{0.6in}
  - \addtolength{\oddsidemargin}{-0.3in}
  - \addtolength{\textheight}{0.6in}
  - \addtolength{\topmargin}{-0.3in}
---
![SpottedLanternfly]({{ "assets/images/SpottedLanternfly.png" | relative_url }}){: class="projects"}

# SWATR: A Scalable Robotic Lanternfly Removal Attachment
**Team:** The Bug Busting Crew  
**Client(s):** Cornell CALS Extension / E&J Gallo Winery / National Grape  

## Context and Problem statement

The Bug Busting Crew focused on a gap between existing vineyard robotics and direct pest removal. Agricultural rovers already support scouting, transport, and row navigation, but they typically do not carry a manipulator designed to physically remove spotted lanternflies from vines. That makes the end effector, rather than the rover itself, the key missing subsystem for real-time intervention [1-4]. From the original client outline, one design requirement remained constant through the semester: the mechanism had to integrate with pre-existing robotic systems rather than depend on a fully custom mobile platform. That constraint pushed the project toward a lightweight, electrically simple gripping system that could mount to larger robotic platforms while staying adaptable to multiple applications. Although the immediate use case was lanternfly removal, the underlying engineering problem is broader. A useful field manipulator must approach irregular targets, conform without crushing them, and complete the grasp with limited actuator mass, cost, and control complexity. Those requirements shaped both the compliant paddle design and the choice to favor simple servo-driven linkages over heavier linear hardware.

## Impact

A robotic removal tool integrated into existing field robots would reduce labor spent on manual scouting and removal, increase coverage across large areas, and allow growers to leverage platforms they already use instead of purchasing new systems - directly improving operational efficiency and crop protection.

## Proposed direction

### Concept: **SWATR Modular Removal Arm**

**What it is:** A lightweight, modular robotic arm with a specialized end-effector to **physically remove adult SLFs or egg masses** from surfaces, designed to mount on existing agricultural mobile robots.

**How it would be used:** A field robot patrols rows; when a target is detected or flagged, the arm positions itself, removes the insect, and stores it in a small onboard container.

**Why it’s better:** Builds on existing robots, automates a repetitive task, and supports future tool swaps.

**End-of-semester proof-of-concept:** A bench or small mobile demo showing a working end-effector removing mock targets from vertical surfaces, basic containment, and a simple approach–remove–retract sequence.

## Prototype and Testing Details

The mechanical design centered on a lightweight, low-friction linkage rather than a heavier linear stage. Two clamp servos produced the primary paddle motion by moving sliders along stainless rods, and a third servo shifted the pivot point vertically to create telescoping motion. The final system achieved 30 mm of travel, exceeding the 25 mm design goal while avoiding the mass and cost of a ball screw. Friction reduction was a recurring priority, so low-friction PTFE washers were included to ensure more servo effort went into useful motion rather than rubbing at the joints and collars. This choice of linkage was important for both cost and packaging. A servo-driven pivot shift kept the mechanism compact, visually understandable for the exhibit, and compatible with off-the-shelf parts that could be machined or assembled quickly. The control stack used an ESP32-S3 devkit, a PCA9685 I2C servo driver board, and serial communication to a Python GUI on a PC. The GUI acted as both controller and visualizer, allowing the team to command paddle gap, pivot position, wrist motion, and pre-scripted demos while also viewing a live geometry model. It also supported servo trimming, savable speed limits, savable range-of-motion constraints, and built-in demos that made repeatable exhibit operation much easier. That combination made calibration and exhibit explanation straightforward, but it also highlighted the present limitation of the system: the gripper can execute commands accurately once given a target state, yet it does not currently sense the object for itself. The pivot hardware shows another design choice that mattered during iteration: set screws and collars created a mostly glueless assembly, and PTFE washers reduced rubbing at the pivot interfaces while preserving more of the servo effort for useful motion. The paddle redesign was equally important. Rather than keep rigid flat paddles, the team used a mesh suspended with foam to introduce natural compliance into the gripping surface. That change helped the gripper hold a wider range of shapes more gently and reduced the rolling behavior seen in the earlier rigidpaddle prototype. For lanternfly removal, that compliance improves the ability to conform around fragile, irregular targets. For future agricultural or industrial use, it also makes the system more versatile when object shape, orientation, or stiffness varies from cycle to cycle. Overall, the prototype demonstrates a practical path from benchtop mechanism to integrated robotic attachment. The hardware choices kept the system inexpensive and understandable, while the testing results showed enough strength, speed, and range of motion to justify future closed-loop development with AI vision and rover-level deployment. A production version that adopted namebrand and legacy-protected parts would likely raise the BOM cost, but that increase would become negligible when spread across a robotic fleet and balanced against saved crop value or reduced product damage.

## Testing and Results

Testing focused on the criteria most relevant to a client deciding whether the concept should continue: strength, range of motion, and response speed. The poster results were used as the primary record, with a small amount of bench detail added here to make the trial methods explicit and consistent with the exhibit data. Strength checks used objects of different sizes and shapes at multiple approach angles, simulated target variability, and mild escape resistance. Motion timing was measured across ten GUI-commanded, hand-timed trials per axis. The telescoping range test was repeated over multiple full stroke cycles and consistently produced approximately 30 mm of travel, exceeding the 25 mm design goal. The GUI and geometry model also maintained roughly +/- 2 mm reoearability at the grippers during benchtop checks. Internal strength testing, therefore, separates static holding from dynamic holding while the gripper moves. The speed values on the poster were averaged from the ten hand-timed trials for each primary motion, and after those timing checks were completed, several software presets were intentionally slowed for exhibit ise so viewers could more easily see each degree of freedom. Together, these results show that the prototype fits more than barely satisfies its targets. Force capacity was an order of magnitude above the 5 gram goal, range of motion comfortably exceeded the required envelope, and the primary motions stayed below one second. That combination suggests the mechanism is strong enough, gast enough, and flexible enough to justify the next step of robotic integration rather than another complete concept change. 

## Final Prototype and Application

The final prototype was a four-DOF end effector with gripping, telescoping, wrist bending, and wrist rotation. Two servos drove sliders along 316 stainless steel rods to open and close the paddles, while a third servo shifted the pivot point vertically to create telescoping motion. Additional wrist joints provided orientation control so the gripper could approach targets from more useful angles than a fixed clamp. In its current exhibit configuration the system operates as an open-loop prototype. A Python GUI on a PC sends serial commands to an ESP32-S3 devkit, which then drives the servos through a PCA9685 I2C servo driver board. This architecture made the prototype straightforward to calibrate, visualize, and demonstrate, but it still depends on a human operator or upstream robotic platform to identify a target and issue the motion commands. The same compliant gripping approach also extends beyond grabbing bugs. A gentle, adaptive end effector could support fruit harvesting without bruising, robotic assembly handling for irregular parts, or any application where a rigid industrial clamp would be too unforgiving.

## Conclusion and Recommendation

The concept is worth continuing. The final prototype met the major benchtop success criteria, exceeded the motion and speed targets, and demonstrated enough grip strength to justify integration work. It is not yet ready for field deployment because target acquisition and grasp planning remain open-loop and the current validation was performed in a controlled test environment. The next design cycle should prioritize three linked tasks: integrate AI vision so the gripper can detect object shape, pose, and gripping requirements in real time; package the mounting, power, and control interfaces for compatibility with existing rover platforms; and preserve the compliant mesh paddle concept while improving durability and repeatability for longer test campaigns.

# References

## References

- A: https://extension.psu.edu/spotted-lanternfly-management-guide
- B: https://projects.sare.org/sare_project/gne22-288/
- C: https://plant-pest-advisory.rutgers.edu/slf-current-management-recommendations-in-vineyards-2/

- Burro Autonomous Field Robot - burro.ai (autonomous transport and patrol robot used in agriculture)  
- Bonsai Amiga - bonsairobotics.ai (modular agricultural mobile robot platform)  
- Naïo Technologies Agricultural Robots - naio-technologies.com (weeding and field robots)  
- Clearpath Robotics Husky UGV - clearpathrobotics.com (common research UGV platform used in outdoor robotics)