# Intelligent Robotics – Lecture 4: Kinematics (ICAT3110)

**Instructor:** Mahmoud Elsanhoury – University of Vaasa

This lecture covers motion representation, forward kinematics, wheel constraints, robot kinematic constraints, maneuverability, holonomic vs. nonholonomic systems, and kinematic control.

---

## Motion Representation

- Robot as rigid body on wheels, operating on horizontal plane.
- Dimensionality: 3 (x, y position + orientation θ about vertical axis).
- Need relationship between **global reference frame** (XI, YI) and **local reference frame** (XR, YR).

### Rotation Matrix
Maps motion from global to local frame:

\[
R(\theta) = \begin{bmatrix} \cos\theta & \sin\theta & 0 \\ -\sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix}
\]

\[
\dot{\xi}_R = R(\theta) \dot{\xi}_I
\]

---

## Forward Kinematics (Differential Drive Robot)

**Parameters:**
- Wheel radius: r
- Distance from center P to each wheel: L
- Wheel spin speeds: φ₁, φ₂

**Local frame velocities:**
- x-direction (forward): \(\dot{x}_R = 0.5r\dot{\phi}_1 + 0.5r\dot{\phi}_2\)
- y-direction (sideways): \(\dot{y}_R = 0\) (no lateral motion)
- Rotation: \(\dot{\theta} = \frac{r\dot{\phi}_1}{2L} - \frac{r\dot{\phi}_2}{2L}\)

**Global frame velocity:**
\[
\dot{\xi}_I = R(\theta)^{-1} \dot{\xi}_R
\]

### Example
If θ = π/2, r = 1, L = 1, φ₁ = 4, φ₂ = 2:
- Robot moves at 3 units/sec along YI (global y-axis)
- Rotates at 1 unit/sec

### Drill (Bonus)
If θ = π, r = 2, L = 3, φ₁ = 6, φ₂ = 5:
- Robot moves at 11 units/sec in negative XI direction
- Rotates at 0.333 units/sec

---

## Wheel Constraints

Each wheel imposes two constraints:
1. **Rolling constraint:** Pure rolling along wheel plane
2. **No lateral slippage:** Zero motion orthogonal to wheel plane

### Wheel Types

| Wheel Type | Steering | DOF | Kinematic Constraints? | Omnidirectional? |
|------------|----------|-----|----------------------|------------------|
| Fixed Standard | Fixed β | 1 (spin) | Yes (2 constraints) | No |
| Steered Standard | Variable β(t) | 2 (spin + steer) | Yes (2 constraints) | No |
| Castor | Vertical axis offset | 2 | No | Yes |
| Swedish | Rollers at angle γ | 2 | No | Yes |
| Spherical | Free rotation | 3 | No | Yes |

### Key Equations

**Fixed Standard Wheel:**
- Rolling: \([\sin(\alpha+\beta), -\cos(\alpha+\beta), (-l)\cos\beta] R(\theta)\dot{\xi}_I - r\dot{\phi} = 0\)
- Sliding: \([\cos(\alpha+\beta), \sin(\alpha+\beta), l\sin\beta] R(\theta)\dot{\xi}_I = 0\)

**Swedish Wheel:** Similar to fixed but with γ (roller angle)
- When γ = 0: behaves like fixed standard wheel
- When γ = π/2: degenerate form

**Castor & Spherical wheels:** Impose no kinematic constraints → omnidirectional

---

## Robot Kinematic Constraints

Only fixed and steered standard wheels affect chassis kinematics.

**Rolling constraints (all standard wheels):**
\[
J_1(\beta_s)R(\theta)\dot{\xi}_I - J_2\dot{\phi} = 0
\]

**Sliding constraints (all standard wheels):**
\[
C_1(\beta_s)R(\theta)\dot{\xi}_I = 0
\]

Where:
- \(J_1(\beta_s)\): projection matrix for wheel plane motions
- \(J_2\): diagonal matrix of wheel radii
- \(C_1(\beta_s)\): projection matrix for lateral constraints

---

## Maneuverability

### Degree of Mobility (δₘ)
\[
\delta_m = \dim N[C_1(\beta_s)] = 3 - \text{rank}[C_1(\beta_s)]
\]
- Measures directly controllable DOF via wheel velocities
- Range: 0 to 3

### Degree of Steerability (δₛ)
- Number of independently controllable steerable wheels
- Each steerable wheel adds δₛ = 1 (if independently steerable)

### Overall Maneuverability (δₘ)
\[
\delta_M = \delta_m + \delta_s
\]

### Five Basic 3-Wheel Configurations

| Configuration | δₘ | δₛ | δₘ | Holonomic? |
|---------------|----|----|----|------------|
| Omnidirectional | 3 | 0 | 3 | Yes |
| Differential | 2 | 0 | 2 | No |
| Omni-Steer | 2 | 1 | 3 | No |
| Tricycle | 1 | 1 | 2 | No |
| Two-Steer | 1 | 2 | 3 | No |

**Note:** Spherical wheels can be replaced by castor or Swedish wheels without affecting maneuverability.

---

## Holonomic vs. Nonholonomic Robots

| Property | Holonomic | Nonholonomic |
|----------|-----------|---------------|
| Constraints | All integrable into positional constraints | Non-integrable (involve velocities) |
| Motion ability | Can move in any direction in configuration space | Velocities (magnitude/direction) are constrained |
| Examples | Omnidirectional robots (Swedish, castor, spherical) | Differential drive, tricycle, Ackerman |

**Key insight:** A robot with δₘ = 3 can follow any **path** in its workspace, but may not be able to follow arbitrary **trajectories** (due to steering dynamics).

---

## Path vs. Trajectory

| Path | Trajectory |
|------|-------------|
| Geometric characteristics only (start to end) | Geometry + Dynamics + Time |
| No time component | Time-parameterized |

**Example:** A two-steer robot (δₘ = 3) can follow any path, but may need time to change steering angles before changing orientation.

---

## Kinematic Control

### Open-Loop Control
- Precompute smooth trajectory (lines and circle segments)
- **Disadvantages:**
  - Difficult to account for all velocity/acceleration constraints
  - No adaptation to environmental changes
  - Non-smooth transitions between segments

### Feedback Control
- Use real-time state feedback
- Set intermediate positions (subgoals) along desired path
- Control law: 
  \[
  \begin{bmatrix} v(t) \\ \omega(t) \end{bmatrix} = K \cdot e
  \]
  where \(e = [x, y, \theta]^T\) is the error vector

---

## Key Takeaways

1. **Kinematics** is fundamental for understanding robot motion and designing controllers.
2. **Wheel constraints** determine what motions are possible.
3. **Maneuverability** = mobility (direct control) + steerability (indirect control).
4. **Holonomic** robots can move in any direction; **nonholonomic** have velocity constraints.
5. **Paths** (geometry) vs. **trajectories** (time + dynamics) – important distinction.
6. **Feedback control** is preferred over open-loop for real-world robotics.

---

## Beyond Basic Kinematics

- **Dynamics** needed for high-speed robots (forces, friction)
- **Slip/skid systems** (tank treads) require dynamic modeling
- **Motorization** analysis ensures actuators can realize kinematic DOF

---

**Next:** Kinematic control and trajectory following in more depth.
