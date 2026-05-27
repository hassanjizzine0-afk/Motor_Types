
## Implementation Example: S_17HS4401S + A4988

### Motor
- **Model**: Songaine S_17HS4401S
- **Type**: Hybrid, bipolar, 2-phase
- **Step angle**: 1.8° (200 steps/rev)
- **Current**: 1.7A per phase
- **Wires**: 4 (A1, A2, B1, B2)

### Driver: A4988
![image_alt](https://github.com/hassanjizzine0-afk/Motor_Types/blob/main/stepper_motor/examples/ex%201/A4988%20(1).jpg.jpeg?raw=true)



The A4988 is a **microstepping driver** with internal chopper circuit. It converts STEP/DIR logic signals into the correct phase sequence for a 2-phase bipolar motor.

| Function | Pin | Connection |
|----------|-----|------------|
| Step input | STEP | Pulse per step (rising edge triggered) |
| Direction | DIR | HIGH = CW, LOW = CCW |
| Enable | ENABLE | LOW = outputs active |
| Motor A | 1A, 1B | Coil A wires |
| Motor B | 2A, 2B | Coil B wires |
| Power | VMOT | 8V - 35V DC |
| Logic | VDD | 3V - 5V |

### Current Limit

A4988 regulates current via PWM chopping. Set with potentiometer (Vref):

```
I_max = Vref / (8 × Rsense)
Vref = I_max × 8 × Rsense

For 1.7A and Rsense = 0.1Ω:
Vref = 1.7 × 8 × 0.1 = 1.36V
```

### Microstepping Resolution

| MS1 | MS2 | MS3 | Microsteps | Steps/Rev (1.8° motor) |
|-----|-----|-----|------------|------------------------|
| LOW | LOW | LOW | 1 (full) | 200 |
| HIGH | LOW | LOW | 1/2 | 400 |
| LOW | HIGH | LOW | 1/4 | 800 |
| HIGH | HIGH | LOW | 1/8 | 1600 |
| HIGH | HIGH | HIGH | 1/16 | 3200 |

### Wiring Diagram

![image_alt](https://github.com/hassanjizzine0-afk/Motor_Types/blob/main/stepper_motor/examples/ex%201/A4988.jpg?raw=true)





```
A4988                   42 Carrier Board               NEMA 17
┌─────────┐             ┌──────────────┐              ┌─────────┐
│ 1A ─────┼─────────────┤ A1          │──────────────┤ Coil A  │
│ 1B ─────┼─────────────┤ A2          │──────────────┤  wire 1 │
│ 2A ─────┼─────────────┤ B1          │──────────────┤ Coil B  │
│ 2B ─────┼─────────────┤ B2          │──────────────┤  wire 1 │
│ STEP ───┼─────────────┤ PUL+        │              └─────────┘
│ DIR ────┼─────────────┤ DIR+        │
│ GND ────┼─────────────┤ GND         │
│ VMOT ───┼─────────────┤ 12-24V      │
└─────────┘             └──────────────┘
                              │
                        12V Power Supply
```

### Critical Notes

- **Never disconnect motor while powered** — destroys driver
- **Heatsink required** on A4988 above ~1A
- **Decoupling capacitor** (100µF) near VMOT prevents voltage spikes
```

---

This focuses only on your specific motor and driver with no Arduino or beginner explanations.
