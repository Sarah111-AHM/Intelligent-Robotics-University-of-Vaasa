# Intelligent Robotics – Lecture 5: Perception (ICAT3110)

**Instructor:** Mahmoud Elsanhoury – University of Vaasa

This lecture covers sensors for mobile robots, classification, performance characterization, GPS, active ranging, motion sensors, vision sensors, stereo vision, and feature extraction.

---

## Degree of Mobility Recap

Two methods to compute δₘ (degree of mobility):
1. DDOF (differentiable degrees of freedom) – always equals δₘ.
2. δₘ = 3 – rank(constraint matrix), where 0 ≤ rank ≤ 3.

**Not** by counting the number of wheels.

---

## What is Perception?

For a robot, the world is ambiguous. Perception is the process of acquiring knowledge about the environment using sensors and extracting meaningful information.

---

## Sensor Classification

### Two Functional Axes

| Axis | Description |
|------|-------------|
| Proprioceptive | Measures internal values (motor speed, battery voltage, joint angles) |
| Exteroceptive | Acquires external environmental information (distance, light, sound) |
| Passive | Measures ambient energy (temperature probe, microphone, camera) |
| Active | Emits energy and measures reaction (ultrasonic, laser) – may affect the measured characteristic |

### Sensor Examples (by increasing complexity)

- Tactile sensors (contact switches, bumpers, optical barriers) – exteroceptive, passive/active
- Wheel/motor sensors (encoders, potentiometers, resolvers) – proprioceptive, active
- Heading sensors (compass, gyroscope, inclinometer) – exteroceptive/proprioceptive
- Ground-based beacons (GPS, optical/RF/ultrasonic beacons) – exteroceptive, active
- Active ranging (ultrasonic, laser, structured light) – exteroceptive, active
- Motion/speed sensors (Doppler radar/sound) – exteroceptive, active
- Vision-based sensors (CCD/CMOS cameras, object tracking) – exteroceptive/proprioceptive

---

## Sensor Performance Characteristics

| Term | Definition | Formula/Example |
|------|------------|----------------|
| Dynamic range | Ratio of max to min measurable input | dB = 10 log₁₀(max/min) |
| Resolution | Smallest detectable difference | 8-bit, 0-5V → 20 mV |
| Linearity | Output changes linearly with input | f(ax+by) = af(x)+bf(y) |
| Bandwidth | Measurements per second (Hz) | Limits robot max speed |
| Sensitivity | Output change per input change | May be affected by other environmental parameters |

**Accuracy vs. Precision** – illustrated with target diagrams (drill exercise).

---

## Ground-Based Beacons – GPS

- Requires at least 4 satellites to solve for (x, y, z) + time correction.
- **Advantages:** Easy, 100% Earth coverage, all-weather, low cost.
- **Disadvantages:** High power consumption, does not work indoors or in tunnels.

---

## Active Ranging

- Most popular sensors in mobile robotics.
- Provide direct distance measurements.
- Used for obstacle detection/avoidance, localization, and mapping.

### Time of Flight
\[
d = c \cdot t
\]
- Ultrasonic (3 m): ~10 ms
- Laser (3 m): ~10 ns – more challenging technologically

---

## Motion/Speed Sensors – Doppler Effect

- Measure relative motion between robot and environment.
- **Doppler effect:** Change in frequency due to relative motion.
\[
f_r = f_t \cdot \frac{1}{1 + v/c} \quad \text{(approximate)}
\]
- Example: Siren pitch changes as ambulance approaches and recedes.

---

## Vision-Based Sensors

### CCD (Charged Coupled Device)
- Array of light-sensitive pixels.
- **Disadvantages:** Inconstancy, limited dynamic range.

### CMOS (Complementary Metal Oxide Semiconductor)
- Transistors next to each pixel, parallel readout.
- **Advantages:** 100× less power, simpler circuitry.
- **Disadvantage:** Less sensitive to light (photons hit transistors instead of photodiodes).

---

## Visual Ranging

**Problem:** Camera projects 3D world onto 2D plane → depth information is lost.

### Depth from Focus
- Move image plane (focus) until image sharpness is maximized.
- Range is derived from image plane position.
- Used in autofocus cameras and camcorders.

### Depth from Defocus
- Take two or more images with different camera geometry.
- Very fast, no search algorithms required, no need for different viewpoints.

### Stereo Vision
- Two images from different perspectives.
- **Advantages:** Dense depth, object shape definition, human motion detection.
- **Disadvantages:** Requires pre-calibration, shadows cause errors.

### Color Tracking
- Track a specific color in a single image – no correspondence problem.
- Provides independent environmental cue.

---

## Feature Extraction

Instead of using raw sensor measurements, extract higher-level information (percepts).

### Geometric Features
- Common in structured environments (office buildings: line segments, circles).
- Simple parametric description, closed-form solutions exist.
- **Line detection:** Match noisy range data to a line model using optimization (e.g., least squares).

### Visual Appearance
- Extracting features from real images (e.g., corners, edges, textures) for recognition and navigation.

---

## Key Takeaways

1. Sensors are classified as proprioceptive/exteroceptive and passive/active.
2. Performance metrics (dynamic range, resolution, linearity, bandwidth, sensitivity) help compare sensors.
3. GPS is excellent outdoors but fails indoors.
4. Active ranging (laser, ultrasonic) provides direct distance measurements.
5. Doppler effect measures relative motion.
6. Vision sensors (CCD, CMOS) enable rich perception; stereo vision and focus-based methods recover depth.
7. Feature extraction (geometric or visual) converts raw data into actionable information.

---

**Next:** Localization and mapping.
