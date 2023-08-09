# Digital Twin at MFI

Welcome to the Digital Twin page of the Manufacturing Futures Institute (MFI) Codebase. Here you will find a collection of projects, code, and packages specifically related to our work in Digital Twin.

## Testbed Project

The objective of the project is to emulate high-mix/low-volume continuous manufacturing. The envisioned testbed is a circular manufacturing ecosystem where parts are assembled, then disassembled such that no material is wasted and where 24/7 operational costs are low, providing potential to generate large datasets. An initial target application is the assembly and disassembly of LEGO® blocks as a fun and compelling technology demonstrator and driver. The expected testbed will grow and build upon a reusable and open-sourced codebase.

![Frame 2](https://github.com/cmu-mfi/.github/assets/8982264/627759fe-e36f-4b4b-a254-6b11e42cf814)

Below are various subsystems of the testbed and associated repos.

1. **Yaskawa GP4 Robots**:
    - [motoman_ros1](https://github.com/cmu-mfi/motoman_ros1) : ROS1 implementation of robot controller interface. Includes GP4 assets, MoveIt configuration, and service implementation. 
    - [gp4-lego-assembly](https://github.com/cmu-mfi/gp4-lego-assembly) : Lego assembly package for GP4

2. **Programmable Light Curtains for Safety**:
    - [bluelc-rpi](https://github.com/cmu-mfi/bluelc-rpi): Onboard compute utilities (like: curtain profile generation) for the blue device.
    - [redlc-rpi](https://github.com/cmu-mfi/redlc-rpi): Onboard compute utilities for the red device.
    - [lc-utils](https://github.com/cmu-mfi/lc-utils): Visualization and calibration utilities for the tesbed
    - [LC-CORE](https://github.com/cmu-mfi/LC-CORE): Driver code for light curtain devices [limited access]
      
3. **Autonomous Mobile Robots (AMR)**: [Link to Repo 1] [Link to Repo 2]
4. **MES and Scheduling**: [Link to Repo 1] [Link to Repo 2]
...

We encourage you to explore these projects and make use of our codebase. If you have any questions or need any help, don't hesitate to reach out to us via our [Contact Us](CONTACT.md) page.

<!-- ## Get Involved

If you're interested in contributing to our work in digital twin, we would love to hear from you! Please check out our [Contribution Guidelines](CONTRIBUTION.md) for information on how to get started.

Thank you for your interest in our work in Digital Twin. We look forward to your collaboration as we continue to innovate in this field.

Stay updated with our latest projects and code releases by subscribing to our newsletter. [Subscribe Here](SUBSCRIPTION.md).
-->

[**Go to Main Page**](https://github.com/cmu-mfi/)
