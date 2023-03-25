# Week 7 (2/19 - 2/25)

```{admonition} Under Construction
This page is currently under construction. Please return later for more updates.
```

## Assembly

## CAD

## Manufacturing

## Programming
This week, the swerve drive group adjusted the auto code to accommodate for the alliance.  Motion magic was tuned for the arm and elevator, allowing for consistent game piece pickup and scoring. Soft limits were also added to protect the elevator and arm from breaking. The vision group switched both limelights to have limelight firmware and added code for object detection and approach.

### Vision Group

This week, the vision group participated in a code review. We also refactored our vision code so we would have a pickup and score command. These would either pickup/score high, mid, or low, and pickup/score a cone or cube based on buttons pressed by the operator (see image below). We also helped assembly connect the limelight.

![Vision Flowchart](./images/Week7/visionflowchart.png)