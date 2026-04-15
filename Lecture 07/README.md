# Intelligent Robotics – Lecture 7: Localization I (GPS, IPS, and Map-Based Navigation)

**Instructor:** Mahmoud Elsanhoury – University of Vaasa

This lecture covers satellite positioning (GPS), indoor positioning systems (IPS), localization challenges (effector noise), behavior-based vs. map-based navigation, and representations for belief and maps.

---

## GNSS (Global Navigation Satellite Systems)

### GPS Basics
- Started by U.S. Department of Defense in 1973.
- First prototype (NAVSTAR) launched 1978.
- Full constellation of 24 satellites operational in 1993.
- Civilian use allowed since 1980s.

### GPS Segments
| Segment | Function |
|---------|----------|
| Space | Satellites (≥24 in orbit) |
| Control | Ground stations for monitoring and correction |
| User | GPS receivers |

### Positioning Principle
- Need **at least 4 satellites** to solve 4 unknowns: (x, y, z) + time correction.
- More than 4 signals → optimization problem (least squares, Kalman filters).
- Each satellite transmits: ID, orbital info (XYZ), timing info (T).

**Space graveyard:** Old satellites moved to higher orbits or directed to Point Nemo (Pacific Ocean).

---

## Why Not Use GPS Indoors?
- GPS signals are very weak and cannot penetrate buildings (concrete roofs/walls).
- Requires direct line-of-sight to satellites.

---

## Indoor Positioning Systems (IPS)

**Definition:** Real-time system that calculates the location of a person or object (moving or stationary) inside buildings.

**Applications:** Visitor tracking in crowded venues (airports, malls), indoor navigation.

### Common IPS Technologies

| Technology | Typical Accuracy | Range | Method |
|------------|------------------|-------|--------|
| UWB | 2–50 cm | 15–50 m | TOA/TDOA trilateration |
| Wi-Fi RSSI | <10 m | 35 m | Fingerprinting |
| Wi-Fi CSI | <5 m | 35 m | Fingerprinting, AoA |
| Bluetooth RSSI | <5 m | <50 m | Fingerprinting |
| Bluetooth DF | <1 m | <50 m | AoA, AoD |
| 5G sub-6 GHz | 3–10 m | 0.5–2 km | TDOA, TW-TOA, AoA, AoD |
| 5G mmWave | 0.2–0.5 m | 200 m | TDOA, TW-TOA, AoA, AoD |

### UWB (Ultra-Wideband)
- Low power transmission, wide bandwidth, high data rate.
- Requires **≥4 anchors** + at least 1 tag.
- Uses **Double-Sided Two-Way Ranging (DS-TW)** to cancel clock offset and drift.

### IPS Performance Metrics
- Accuracy, Availability, Coverage, Scalability, Cost, Privacy.

### NLOS (Non-Line-of-Sight) Challenge
- Occurs in dense environments (mines, heavy concrete/metal structures).
- Mitigated via sensor fusion and algorithmic remedies.

---

## Localization Challenges – Effector Noise

- Effectors (wheels, motors) also introduce noise, not just sensors.
- Movement generally **increases uncertainty**.
- Sources of odometric errors:
  - Limited integration resolution (time increments, measurement resolution)
  - Wheel misalignment (deterministic)
  - Uncertainty in wheel diameter (especially unequal diameters)
  - Wheel slip or non-planar floor
- **Odometry + Dead Reckoning:** Position update using only proprioceptive sensors (wheel encoders, heading sensors). Errors accumulate over time → need periodic correction from other localization mechanisms.

---

## Behavior-Based Navigation

- Instead of geometric map, design **sets of behaviors** that together produce desired motion.
- Avoids explicit reasoning about localization and path planning.
- **Drawback:** Multiple active behaviors can interfere; adding a new behavior often requires retuning all existing ones.

---

## Map-Based Navigation

- Includes explicit localization and cognition modules.
- Robot collects sensor data and updates belief about its position relative to a map.
- **Advantage:** Belief transparent to human operators; human can give robot a new map when entering a new environment.

---

## Belief Representation

### Two Main Branches

| Type | Description | Advantage | Disadvantage |
|------|-------------|-----------|---------------|
| Single-hypothesis | Unique point on map | No ambiguity | Cannot handle uncertainty |
| Multiple-hypothesis | Set of possible positions (possibly infinite) with ordering (e.g., probability distribution) | Explicitly maintains uncertainty; can update with partial info | More complex |

---

## Map Representation

### Three Fundamental Relationships
1. Map precision must match goal precision.
2. Map precision and feature types must match sensor precision and data types.
3. Map complexity directly impacts computational complexity of mapping, localization, and navigation.

### Continuous-Valued Maps
- Exact decomposition of environment in continuous space.
- Most implementations use **2D** only (higher dimensions cause computational explosion).
- Often combined with **closed-world assumption**: all environmental objects are specified in the map; empty areas truly have no objects.

### Decomposition and Abstraction
- Keep only relevant features → compact representation.
- Can be hierarchical (pyramid) → computationally efficient planning.
- **Disadvantage:** Loss of fidelity between map and real world (both qualitative and quantitative).

---

## Summary

| Concept | Key Points |
|---------|-------------|
| GPS | 4+ satellites, trilateration, fails indoors |
| IPS | UWB, Wi-Fi, Bluetooth, 5G; NLOS is major challenge |
| Effector noise | Odometry errors accumulate; need periodic corrections |
| Behavior-based | No explicit map; multiple behaviors may conflict |
| Map-based | Uses explicit map and belief; transparent to humans |
| Belief | Single or multiple hypotheses; probability distributions |
| Map | Continuous or decomposed; trade-off fidelity vs. complexity |

---

**Next:** Localization algorithms (Kalman filters, particle filters, SLAM).
