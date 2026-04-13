# Intelligent Robotics – Lecture 3: Wheeled Locomotion (ICAT3110)

**Instructor:** Mahmoud Elsanhoury – University of Vaasa

This lecture covers wheeled locomotion mechanisms, wheel types, geometry, maneuverability, controllability, and introduces kinematics for mobile robots.

---

## Recap: Legged Locomotion

- Biologically inspired.
- Number of possible gait events: `N = (2k – 1)!` where `k` = number of legs.
  - Hexapod (k=6): ~40 million events.
- Advantages: Adaptability, maneuverability on rough terrain, skillful manipulation.
- Disadvantages: Power consumption, mechanical complexity.

---

## Wheeled Mobile Robots

- Most popular locomotion mechanism for human-designed robots.
- Simple, efficient, stable on hard flat surfaces.
- Wheels maintain constant ground contact → constant balance.
- 3 wheels = sufficient for static stability. 2 wheels = possible but harder control.

### Wheel Classes (4 major types)
Differ in kinematics – choice greatly affects overall robot kinematics.

### Suspension Systems
- Needed for all-terrain robots or robots with >3 wheels.
- Simple: deformable soft rubber tires.
- Advanced: dynamic suspension for rough terrain.

---

## Wheeled Geometry

### Automobiles vs. Mobile Robots
- Automobiles designed for standardized roads (Ackerman configuration).
- Ackerman configuration has poor maneuverability for mobile robots (unless robot is designed for road networks).

### Wheel Types (from lecture icons)
| Icon | Description |
|------|-------------|
| ○ | Unpowered omnidirectional (spherical, castor, Swedish) |
| ◉ | Motorized Swedish wheel (Stanford wheel) |
| ○ | Unpowered standard wheel |
| ◉ | Motorized standard wheel |
| ◉ | Motorized and steered castor wheel |
| ○ | Steered standard wheel |
| ◉ | Standard connected wheels |

### Common Configurations

| # Wheels | Arrangement | Examples |
|----------|-------------|----------|
| 2 | Front steering + rear traction | Bicycle, motorcycle, Personal Cye |
| 3 | Two-wheel differential drive + third contact point | smartRob, EPFL, Pygmalion, many indoor robots |

---

## Maneuverability

- **Omnidirectional robots:** Can move in any (x,y) direction regardless of orientation.
  - Use Swedish (Mecanum) or spherical wheels.
  - Example: Uranus (Carnegie Mellon) with Mecanum wheels.
- **Spherical wheels:** Each actuated by one motor, suspended by 3 contact points. Excellent maneuverability but limited to flat surfaces & small loads.
- **4 castor wheels (actively steered & translated):** Truly omnidirectional.
- **Two-wheel differential drive:** Most popular. One or two additional ground contact points for stability.
- **Ackerman steering:** Common in hobby racing cars. Good lateral stability at high speeds, but large turning diameter, cannot move sideways easily.

---

## Controllability

- **Inverse correlation** between maneuverability and controllability.
- Omnidirectional designs require more processing and are often less accurate.
- Ackerman vehicle goes straight easily by locking steerable wheels.
- **No ideal drive configuration** maximizes stability, maneuverability, and controllability simultaneously. Choose based on application.

---

## Case Study: Synchro Drive

- Popular for indoor mobile robots.
- 3 driven & steered wheels, but only **2 motors total**:
  - 1 translation motor → sets speed of all wheels.
  - 1 steering motor → spins all wheels about vertical axes.
- Examples: Nomadics 150, RWI B21r.

### Other Systems

| System | Pros | Cons |
|--------|------|------|
| Tracked slip/skid | Best maneuverability on rough terrain | Inefficient on flat ground, hard to predict rotation center |
| Walking wheels (hybrid) | Combines leg adaptability + wheel efficiency | More complex; can climb objects up to 2× wheel diameter |

---

## Introduction to Kinematics

- Study of how mechanical systems behave.
- In mobile robotics: understand mechanical behavior for design and control software.

### Key Difference: Manipulator vs. Mobile Robot

| Aspect | Manipulator (robot arm) | Mobile Robot |
|--------|------------------------|--------------|
| Position measurement | Direct (from sensors) | No direct method – must integrate motion over time |
| Accuracy | Computable instantly | Affected by slippage & integration errors |
| Workspace | Range of end-effector positions | Range of possible poses in environment |

### Kinematic Models
- Bottom-up process: each wheel contributes motion and imposes constraints (e.g., no lateral skid).
- Constraints combine based on chassis geometry → overall motion constraints.
- Must express forces/constraints in a **consistent reference frame**.
- **Global vs. Local frames mapping** is essential.

### Motion Representation
- Robot as a rigid body on wheels, operating on a horizontal plane.
- Dimensionality: 3 (x, y position + orientation θ about vertical axis).
- Relationship between global frame (XI, YI) and local frame (XR, YR) with angle θ.
