# Intelligent Robotics – Lecture 6: Perception II (ICAT3110-3011)

**Instructor:** Mahmoud Elsanhoury – University of Vaasa

This lecture continues the discussion on perception, covering sensor performance details, wheel/motor sensors, heading sensors (compasses, gyroscopes), and introduces mobile robot localization challenges.

---

## Sensor Performance – Advanced Concepts

### Cross-sensitivity
- Sensitivity to environmental parameters **orthogonal** to the target parameter.
- Example: Flux-gate compass sensitive to magnetic north **and** ferrous building materials → may become useless indoors.

### Systematic vs. Random Errors

| Error Type | Description | Examples |
|------------|-------------|----------|
| **Systematic** | Deterministic, can be modeled | Poor calibration, unmodeled floor slope, bent stereo head |
| **Random** | Stochastic, cannot be modeled precisely | Hue instability, spurious range errors, black level noise |

### Accuracy vs. Precision

- **Accuracy:** Closeness to true value.
- **Precision:** Reproducibility (low scatter). Defined as:  
  \[
  \text{Precision} = \frac{\text{range}}{\sigma}
  \]
  - Only σ (standard deviation) affects precision.
  - μ (mean) affects total error and is inversely related to accuracy.

| | Accurate | Inaccurate |
|--|----------|------------|
| **Precise** | Ideal (A) | Systematic error (B) |
| **Imprecise** | (rare) | Random error (C) |

---

## Challenges Specific to Mobile Robots

### Blurring of Systematic and Random Errors
- When robot is **stationary**, a sensor may produce the same incorrect reading repeatedly → appears systematic.
- When **moving**, the same mechanism may appear random due to changing pose/environment.
- Example: Sonar specular reflections from smooth walls → consistent overestimation of range.

### Multimodal Error Distributions
- Probability distribution with two or more modes (peaks).
- Example: Sonar facing certain materials → bimodal distribution (correct range + overestimated range).

---

## Wheel/Motor Sensors

### Optical Encoders
- Mechanical light chopper: light source, fixed grating, rotating disc with optical grid, detectors.
- Produces sine/square waves per revolution.
- Converted to square wave via threshold.
- Resolution measured in **CPR** (cycles per revolution).

---

## Heading Sensors

### Compasses

| Type | Principle | Pros | Cons |
|------|-----------|------|------|
| Hall effect | Voltage difference in semiconductor due to magnetic field | Inexpensive | Poor resolution, nonlinearity, bias errors |
| Flux gate | Two perpendicular coils on ferrite cores | More accurate | Requires power; if power off → no function |

### Gyroscopes

**Mechanical Gyroscope:**
- Fast-spinning rotor, uses **gyroscopic precession**.
- Reactive torque: \(\tau = I \omega \Omega\)
  - \(I\) = moment of inertia
  - \(\omega\) = spin speed
  - \(\Omega\) = precession speed
- Maintains inertial stability.

**Optical Gyroscope:**
- Uses two laser beams from same source (clockwise and counterclockwise).
- No moving parts.
- Based on Sagnac effect: rotation causes path length difference → frequency shift.
- Used in aircraft since early 1980s.

---

## Mobile Robot Localization

### Navigation's Four Building Blocks
1. **Perception** – interpret sensor data
2. **Localization** – determine position in environment
3. **Cognition** – decide actions to achieve goals
4. **Motion control** – execute desired trajectory

> Localization has received the most research attention in the past decade.

### Navigation vs. Localization
- **Navigation:** Complete process of getting from A to B (path planning, obstacle avoidance).
- **Localization:** Answering "Where am I?" (absolute or relative).

### Why GPS is not a complete solution
- Accuracy: several meters (insufficient for indoor/delicate tasks)
- Does not work indoors or in obstructed areas
- Localization also requires **relative position** to objects/people, and often a **map** for path planning.

---

## Localization Challenges

### 1. Sensor Noise
- Reduces consistency and information content.
- Solutions:
  - **Temporal fusion** – combine multiple readings over time.
  - **Multi-sensor fusion** – combine different sensor types.

### 2. Sensor Aliasing
- **Definition:** Non-unique sensor readings from different locations (same percept from different places).
- Humans rarely experience aliasing (visual system is highly discriminating).
- For robots, aliasing is the **norm**, not the exception.
- Example: Sonar cannot distinguish between a human and a chair in an indoor setting.

### Aliasing in Signal Processing (context)
- Occurs when sampling frequency \(F_s\) is less than twice the maximum signal frequency (Nyquist criterion).
- Results in low-frequency artifacts (alias frequencies \(F - F_s\)).

**Consequence for navigation:** Even with noise-free sensors, a single percept usually provides insufficient information to uniquely identify robot position. Must use **sequences of readings** over time.

---

## Key Takeaways

1. **Cross-sensitivity** can render a sensor useless in certain environments.
2. **Systematic errors** are predictable; **random errors** are stochastic.
3. **Precision ≠ accuracy** – precision measures reproducibility, accuracy measures closeness to true value.
4. Mobile robots blur the line between systematic and random errors due to motion.
5. **Optical encoders** are common for wheel/motor sensing.
6. **Compasses** (Hall effect, flux gate) and **gyroscopes** (mechanical, optical) provide heading.
7. **Localization** is a core component of navigation, but GPS has limitations.
8. **Sensor noise** and **sensor aliasing** are major challenges – overcome via temporal/multi-sensor fusion and sequential readings.

---

**Next:** Localization techniques (probabilistic methods, Kalman filters, particle filters).
