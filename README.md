# 4-Servo-Motor-Control-Arduino
This project demonstrates how to control four servo motors using an Arduino. The program runs a sweeping motion for each servo for 2 seconds, then locks all servos at 90 degrees.

# Features
- Controls 4 servo motors simultaneously.
- Simulates sweep motion for 2 seconds (like the built-in Servo example).
- Holds all motors at 90 degrees afterward.

# Tools uesd 
| Tool                        | Purpose                    |
| --------------------------- | -------------------------- |
| Arduino IDE                 | Writing and uploading code |
| Servo.h                     | Servo control library      |
| Arduino Uno (or compatible) | Microcontroller            |

# How It Works
All four servos sweep from 0° to 180° and back for 2 seconds.

After sweeping, the servos are set and held at a fixed angle of 90°.

# Circuit Design
This project was designed and simulated using Tinkercad Circuits.

Image of the Circuit Setup:

<img width="804" height="461" alt="pic" src="https://github.com/user-attachments/assets/7a1bd2be-9b24-47b2-9f98-0220f60b36f4" />


Video Demonstration:

https://github.com/user-attachments/assets/2d157df9-abd0-4c40-99fe-1c1b4646a792


# An algorithm for how the walking motion will be executed in the humanoid robot.

Servo Configuration

| Servo # | Joint | Leg Side | Function                          | Approximate Range (Degrees) |
| ------- | ----- | -------- | --------------------------------- | --------------------------- |
| S1      | Hip   | Left     | Moves entire leg forward/backward | 60° – 120°                  |
| S2      | Knee  | Left     | Bends/straightens the leg         | 60° – 120°                  |
| S3      | Hip   | Right    | Moves entire leg forward/backward | 60° – 120°                  |
| S4      | Knee  | Right    | Bends/straightens the leg         | 60° – 120°                  |

Walking Strategy (Cycle-Based)
We simulate a walking cycle in alternating leg steps, where one leg steps forward while the other supports balance. Each leg has:
- 1 hip (leg swing)
- 1 knee (lift & land)

Complete Walking Cycle (4 Phases)
Phase 1: Neutral Standing (Initial Position), Robot stands upright. Both legs straight, feet flat.

| Servo | Angle | Description                   |
| ----- | ----- | ----------------------------- |
| S1    | 90°   | Left hip in neutral position  |
| S2    | 90°   | Left knee straight            |
| S3    | 90°   | Right hip in neutral position |
| S4    | 90°   | Right knee straight           |

Phase 2: Lift Left Leg, Step Forward. Shift imaginary weight to right leg (balance passively). Swing left leg forward.
| Servo | Angle | Description                 |
| ----- | ----- | --------------------------- |
| S1    | 60°   | Left hip moves leg forward  |
| S2    | 120°  | Left knee bends (lift foot) |
| S3    | 90°   | Right hip stays neutral     |
| S4    | 90°   | Right knee remains straight |

Wait ~200–400 ms for motion

Phase 3: Place Left Foot, Shift Forward. Straighten left leg to touch ground.
| Servo | Angle | Description            |
| ----- | ----- | ---------------------- |
| S1    | 60°   | Left leg still forward |
| S2    | 90°   | Left knee straightens  |
| S3    | 90°   | Right hip neutral      |
| S4    | 90°   | Right knee straight    |

Wait ~200 ms

Phase 4: Lift Right Leg, Step Forward. Shift weight to left leg (new support), Move right leg forward.
| Servo | Angle | Description                  |
| ----- | ----- | ---------------------------- |
| S1    | 60°   | Left leg holds ground        |
| S2    | 90°   | Left knee straight           |
| S3    | 120°  | Right hip swings leg forward |
| S4    | 120°  | Right knee bends             |

Wait ~200–400 ms

Loop Back to Phase 1 Repeat the cycle:
Phase 1 → Phase 2 → Phase 3 → Phase 4 → Phase 1...


! Limitations of 4 Servo Setup:
Less smooth walking
Harder to balance
No dynamic foot control (no ankle)
Best for slow walking or controlled surfaces






