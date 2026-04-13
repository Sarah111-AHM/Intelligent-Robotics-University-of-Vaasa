# Intelligent Robotics – Lecture 2: Locomotion (ICAT3110-3112)

**Instructor:** Mahmoud Elsanhoury – University of Vaasa

This lecture covers legged and wheeled locomotion mechanisms for mobile robots.

---

## Key Concepts

### Locomotion Definition
- Enables a robot to move unbounded in its environment.
- Inspired by biology (mammals, insects, fish) except for the powered wheel (human invention).

### Wheeled vs. Legged Locomotion

| Feature | Wheeled | Legged |
|---------|---------|--------|
| Complexity | Simple | High (more DOF) |
| Best surface | Hard, flat | Soft, rough |
| Friction on soft ground | High (bad) | Low (good) |
| Static stability | Easy (3+ wheels) | Needs 6 legs |
| Maneuverability | Limited on rough terrain | High |

> **Conclusion:** Nature favors legged locomotion. Humans flatten surfaces for wheels. Hybrid solutions are emerging.

---

## Key Issues in Locomotion & Manipulation
- **Locomotion:** Environment fixed, robot moves by applying force.
- **Manipulation:** Robot arm fixed, moves objects.
- Shared concerns: stability, contact characteristics, friction, center of gravity (COG), terrain inclination.

---

## Legged Mobile Robots

### Advantages
- Adaptability to rough terrain
- Skillful object manipulation

### Disadvantages
- Power consumption & mechanical complexity

### Stability & Leg Configuration
- **Static stability:** Needs at least 3 legs (tripod). For static *walking*, minimum 6 legs.
- Number of possible gait events: `N = (2k – 1)!` where `k` = number of legs.
  - Biped (k=2): 6 events
  - Hexapod (k=6): ~40 million events

### Examples

| Type | Example | Key Feature |
|------|---------|--------------|
| 1-leg | Raibert Hopper (MIT, 1983) | Dynamic stability only, hops, 85% energy return via springs |
| 2-leg | Sony SDR-4X, HONDA Asimo | Anthropomorphic, dances, climbs stairs, needs active balance |
| 4-leg | Sony AIBO | Passively stable when still, chases colored balls |
| 6-leg | Genghis (hobby robot) | Statically stable, less maneuverable than real insects |

> Insects outperform robots due to passive structures (barbs, pads) – not just DOF.

---

## Wheeled Mobile Robots

### Advantages
- Simple, efficient, stable on flat hard surfaces.
- Minimum 3 wheels for static stability (2 wheels possible but harder control).

### Wheel Types
1. Unpowered standard wheel
2. Motorized standard wheel
3. Motorized & steered caster wheel
4. Omnidirectional wheels (Swedish, spherical)

### Suspension
- Needed for all-terrain robots (>3 wheels).
- Simple: deformable soft rubber tires.
- Advanced: dynamic suspension for rough terrain.

### Wheel Geometry
- Automobiles use Ackerman configuration – poor maneuverability for robots.
- For robots: 2-wheel differential drive, 3-wheel centered drive, etc.

### Static Stability Condition
> **COG must lie inside the triangle formed by ground contact points.**

More wheels = more stability, but also more complexity.

---

## Summary Table

| Aspect | Legged | Wheeled |
|--------|--------|---------|
| Best terrain | Soft, uneven | Hard, flat |
| Static stability | Needs 6 legs for walking | 3 wheels enough |
| Control complexity | High | Moderate |
| Energy efficiency | Lower | Higher (on flat) |
| Biological inspiration | Yes | No (human invention) |

---

## References
- Siegwart, Nourbkhsh, Scaramuzza – *Introduction to Autonomous Mobile Robots*, MIT Press.
- Bristol Robotics Laboratory, MIT, SONY, HONDA.

---

**Next:** Wheeled robot kinematics and control.
