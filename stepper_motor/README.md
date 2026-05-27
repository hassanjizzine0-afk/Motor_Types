Understood. Here is a concise, no-Arduino, technical README focused solely on the stepper motor itself.

---

# Stepper Motor Fundamentals

## What is a Stepper Motor?

A **stepper motor** is an electromechanical actuator that converts electrical pulses into discrete mechanical angular displacements (steps). It operates open-loop—position is determined by counting pulses, not by feedback.

## Operating Principle

The motor consists of:
- **Stator**: Electromagnets arranged in phases (2 or 3)
- **Rotor**: Permanent magnet with toothed structure (hybrid type)

When a phase is energized, the rotor aligns with the resulting magnetic field. Sequentially switching phases rotates the rotor by a fixed angle.

### Step Generation (2-Phase Motor)

| Phase Sequence | Rotor Position |
|---------------|----------------|
| A+ B+         | 0°             |
| A- B+         | 1.8°           |
| A- B-         | 3.6°           |
| A+ B-         | 5.4°           |

Each transition = one step. Reversing sequence reverses rotation.

## Stepper Motor Types

| Type | Rotor Construction | Step Angle | Torque @ Low Speed | Cost |
|------|-------------------|------------|--------------------|------|
| **Permanent Magnet (PM)** | Smooth permanent magnet | 7.5° - 15° | Low | Low |
| **Variable Reluctance (VR)** | Toothed soft iron (no magnet) | 7.5° - 15° | Very Low | Low |
| **Hybrid (HB)** | Toothed permanent magnet + toothed stator | 0.9° - 3.6° | High | Medium |
| **Linear Stepper** | Integrated threaded nut | N/A | N/A | High |

### Winding Configurations

| Configuration | Wires | Phase Count | Driver Type |
|---------------|-------|-------------|--------------|
| Bipolar | 4 | 2 | H-bridge (current reversal) |
| Unipolar | 5 or 6 | 2 | Center-tapped (single direction) |
| 3-Phase | 3 or 5 | 3 | 3-phase bridge |

## Key Characteristics

- **Holding torque**: Torque when energized but stationary
- **Detent torque**: Residual torque when de-energized (present in PM/HB)
- **Step accuracy**: ±5% non-cumulative (error does not add across steps)
- **Resonance**: Natural frequency exists at certain step rates
- **Microstepping**: Partial energization of both phases creates intermediate positions (reduces resonance, increases resolution)

## Physical Construction (Hybrid Type)

Stator and rotor both have precision teeth. Number of teeth determines step angle:

```
Steps per revolution = (Rotor teeth × 2) / Phase count
200 steps/rev = 50 rotor teeth × 2 / 2 phases → 1.8° per step
```

Stator teeth are offset between phases to create the stepping sequence without requiring the rotor to physically "jump" between discrete magnet positions.

## Common Applications by Type

| Application | Motor Type | Rationale |
|-------------|------------|-----------|
| 3D printers, CNC | Hybrid 2-phase | Precision + cost |
| Industrial robotics | Hybrid 3-phase | Higher torque, smoother |
| Automotive gauges | PM | Low cost, acceptable accuracy |
| Linear actuators | Linear stepper | No external screw mechanism |

## Limitations

- Open-loop: No position verification (stall = lost steps)
- Torque drops significantly at high speeds
- Consumes current even when stationary (holding torque)
- Requires driver with current limiting (coils cannot connect directly to supply)
```

---

This covers the motor theory, types, and construction without microcontroller references.
