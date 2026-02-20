---
layout: project
description: Client Outline and Pitch for MAE2250 ODP
image: assets/images/Spotted Lanternfly.jpeg
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

# SWATR: A Scalable Robotic Lanternfly Removal Attachment
**Team:** The Bug Busting Crew  
**Client(s):** Cornell CALS Extension / E&J Gallo Winery / National Grape  

## Problem statement

Spotted lanternflies (SLF) cause major damage to vineyards, but current control methods do not scale. Adult SLFs frequently jump to evade capture when approached, making them difficult to remove by hand even once spotted ([A](https://extension.psu.edu/spotted-lanternfly-management-guide)). Growers often require **2–6+ pesticide applications per season** due to continual reinfestation, indicating high labor and input costs ([B](https://projects.sare.org/sare_project/gne22-288/)). In heavy infestations, SLF densities can exceed **10 per vine and reach hundreds per vine**, making manual control impractical ([C](https://plant-pest-advisory.rutgers.edu/slf-current-management-recommendations-in-vineyards-2/)). Meanwhile, agricultural mobile robots already exist for transport and patrol, but **lack tools for targeted pest removal**. The result is a technology gap: growers have mobile platforms and labor, but no **scalable, purpose-built physical removal tool** that integrates with these systems to target SLF at a specific life stage.

## Impact

A robotic removal tool integrated into existing field robots would reduce labor spent on manual scouting and removal, increase coverage across large areas, and allow growers to leverage platforms they already use instead of purchasing new systems - directly improving operational efficiency and crop protection.

## Proposed direction

### Concept: **SWATR Modular Removal Arm**

**What it is:** A lightweight, modular robotic arm with a specialized end-effector to **physically remove adult SLFs or egg masses** from surfaces, designed to mount on existing agricultural mobile robots.

**How it would be used:** A field robot patrols rows; when a target is detected or flagged, the arm positions itself, removes the insect, and stores it in a small onboard container.

**Why it’s better:** Builds on existing robots, automates a repetitive task, and supports future tool swaps.

**End-of-semester proof-of-concept:** A bench or small mobile demo showing a working end-effector removing mock targets from vertical surfaces, basic containment, and a simple approach–remove–retract sequence.

## Key risks / unknowns

- **Tool effectiveness:** If insects are dislodged but not retained, impact is low
- **Robot compatibility:** Payload, power, and mounting limits may constrain design 
- **Cycle time:** If removal is too slow, field throughput may be worse than manual labor
- **Surface variability:** Bark, posts, and trellises vary in roughness, curvature, and form;

*De-risking plan:* We will address these risks through benchtop prototyping and testing of the end-effector across representative surfaces, payload constraints, and timed removal cycles.


## Questions for the client

1. **Are mobile or robotic platforms already part of your day-to-day workflow? If so, which ones and what tasks do they perform?**  
   *Decision affected:* Whether we design for integration (mounting, power) or assume a standalone system.

2. **Is any active SLF removal happening today, or is it largely impractical at scale? If it is happening, where does it consume the most time?**  
   *Decision affected:* Replace an existing task vs. enable a new one, which surfaces/use cases to prioritize.

3. **Would you prefer a few high-capability tools or many simpler tools distributed across the field - and what constraints drive that?**  
   *Decision affected:* System architecture (single high-performance attachment vs. scalable, low-complexity fleet).


# References

## References

- A: https://extension.psu.edu/spotted-lanternfly-management-guide
- B: https://projects.sare.org/sare_project/gne22-288/
- C: https://plant-pest-advisory.rutgers.edu/slf-current-management-recommendations-in-vineyards-2/

- Burro Autonomous Field Robot - burro.ai (autonomous transport and patrol robot used in agriculture)  
- Bonsai Amiga - bonsairobotics.ai (modular agricultural mobile robot platform)  
- Naïo Technologies Agricultural Robots - naio-technologies.com (weeding and field robots)  
- Clearpath Robotics Husky UGV - clearpathrobotics.com (common research UGV platform used in outdoor robotics)