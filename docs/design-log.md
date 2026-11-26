# Design log

[← Back to README](../README.md#test-results)

The prototype was developed in short **design → print → assemble → test** cycles (the development and evaluation stages of Design Science Research). This page summarises the problems that showed up on the physical robot, their root causes and the fixes. Most failures did not come from the concepts but from details that only appear in the real object.

## Architecture decisions

| Initial proposal | What was built | Why |
|---|---|---|
| Articulated arm with several servos | Vertical lead-screw elevator + simple gripper | Decoupled, simpler kinematics; fewer actuators to control. |
| Images sent to an external computer, ESP32 as a bridge | Raspberry Pi 4 on board (edge) + Arduino over USB | The Pi already has Wi-Fi and USB 3.0 for the Kinect v2; one cable replaces the bridge. |
| L298N motor drivers | BTS7960 (43 A) | Current margin for the motors; the same driver for tracks and elevator. |
| Several batteries | One LiPo 3S with isolated branches | Less weight. Two step-down converters keep the logic rail free of servo and motor current peaks. |
| Rope and pulley elevator | Lead screw | Precision and holding the position with the motor off. |
| Gripper with a stem cutter | Cage gripper, detachment by pulling | Simpler and printable. Cutting and twisting moved to the roadmap. |

## Chassis and locomotion

| Problem observed | Root cause | Fix |
|---|---|---|
| The wheel did not fit the motor shaft as designed. | Shaft size was taken from a generic JGY370 datasheet (Ø6.4 mm), which described another variant. | Tested the real shaft in the printed wheel and trusted the measurement. Later the motors were replaced by a version with an M6 threaded shaft, removing the coupler entirely (parts 11, 12 and 14 discontinued). |
| The wheel spun inside the track without pulling it. Changing the track length between 89 % and 100 % did not help. | In the CAD script the teeth were generated on the **outer** face of the ring (ground side) instead of the inner face (wheel side). Earlier "successful" tests only checked that the track **fitted**, not that it was **driven**. | Teeth moved to the inner face. Lesson: test function under load, not only fit. |
| The front wheel slipped on its shaft under track tension. | The wheel was held by nut friction only. | Nyloc nuts + threadlocker; the radial locking screw was added to part 07 as a further option. |
| The track kept failing at 92 % length and the wheels looked tilted. | One rear bearing bracket was mounted on the wrong side: the off-centre axle sat **13 mm higher**. | Brackets swapped and mounted upright. **First successful run on 7 Oct 2026** with the 92 % track. |
| Battery and charger boxes printed badly. | Overhangs and side features that needed supports. | v2 boxes: lids screwed through vertical fins, everything prints without support, fixed only to existing holes. |
| The screw heads under the bottom plate scraped the floor. | Only ~3 mm between the plate and the ground; the 17 M5 pan heads (~Ø10 × 3.5 mm) stick out below it. A thin TPU sheet with pockets, taped under the whole plate, was modelled first. | Replaced by individual TPU caps (less material, each one replaceable), press-fitted with a drop of superglue: 9 single (38a) and 4 double (38b) for the corner pairs, 12.2 mm apart. Bore found by test: the double cap holds at Ø9.8, the single needed Ø9.4 (9.8 and 9.6 fell off). Superglue alone was not relied on, since it cracks on flexible TPU. |

## Elevator

| Problem observed | Root cause | Fix |
|---|---|---|
| The tower's top lugs needed 245 mm-tall supports. | 8 mm overhangs at the top. | Tried a "grow from the base" version without lugs; it was reverted for appearance and the original lug design was kept. |
| The lead screw printed lying down had a rough thread. | Flat face on the bed and irregular lower flanks. | Printed upright instead, first in four pieces. |
| With four pieces, the joints slipped against each other when the motor overran the end of travel. | Torque between pieces was transmitted only by friction. | **One-piece screw** (215.5 mm, fits the 256 mm build height). Parts 28a/28b/29a/29b discontinued. |
| The screw would not enter the first carriage. | The boolean cut of the helical thread **failed silently** in the CAD, leaving a smooth bore. | v2: the thread is cut in a simple tube that is then fused to the carriage, with 0.5 mm radial clearance. Lesson: check helical geometry with section cuts, not only "is valid". |
| The pinion ended up lower than designed. | Assembly tolerance on the motor shelf. | Gear v2 with 16 mm wide teeth: meshes at any height between 2 and 18 mm. |
| The carriage jams at the ends if the motor overruns. | No end-of-travel sensing yet. | Pending: limit switches (roadmap). |

## Kinect v2 mount

| Problem observed | Root cause | Fix |
|---|---|---|
| The cradles printed with a poor surface. | Printed upside down: a 66 mm unsupported bridge. | v2: walls extended and cradles printed lying on their side, without support. |
| The pivot bolt did not go through 35e. | A central rib sat on the pivot axis. | 35e v3: two side ribs with a 16 mm gap for the nut. |
| No room for the servo tab nuts on 35d. | Side walls only 1.25 mm from the holes. | 35d v2 without side walls (bending stress ~0.6 MPa, far below the limit). Lesson: check head, nut and wrench clearance on every hole. |

## Gripper

| Generation | What happened |
|---|---|
| 1. Cage gripper adapted from an open model + stem cutter driven by a second servo | Stringing under overhangs, and a wall of less than 0.4 mm between the horn screw holes and the gear's tooth root. Hanging below the tool plate, it would hit the chassis when the elevator went down. |
| 2. Same gripper without the cutter | Detachment changed to pulling (elevator down or robot reversing); cutting and twisting moved to future work. |
| 3. New gripper, two parts (36A + 36B) | Designed from scratch and kept entirely above the tool plate's lower edge. On assembly, the moving jaw sat **~8 mm above** the fixed jaw: the real DS3218MG is ~8 mm shorter (tabs to shaft tip) than its catalogue drawing. **36A v2** raised the fixed jaw by 8 mm, and the jaws now align. The gripper opens, closes and holds the fruit on the bench. |

## Hopper

Version 3 was printed, installed on the robot and works: the lock fits the tunnel, and the latch holds the door shut and releases it when retracted. In CAD, the door swings 0–90° without collision and the body holds two oranges. It uses only existing holes, so it can be added without changing any other part.

| Version | Problem | Fix |
|---|---|---|
| 1 | The solenoid pocket (55 × 26 × 20.5 mm) was sized from the TAU-S0837DL catalogue. On the printed part the body width and height fit, but the length did not: the 54 mm body plus the latch, which still sticks out 15 mm when retracted, did not fit, and the 10 × 8 mm pin hole was smaller than the 10 × 10 mm latch. The pocket also needed tree supports. | — |
| 2 | Printed and tried: the 24 × 18 mm tunnel was the size of the lock, not big enough to take it. The real section needs at least 23 mm of width and 26 mm of height (the frame and screw heads add to the 21 × 15 mm first measured). | Measured lock: body 54 × 21 × 15 mm, latch 25 mm out and 15 mm retracted (10 mm stroke). Closed 24 × 18 × 59 mm tunnel loaded from the back and closed by a separate back cap 37d (Ø12 mm wire hole, 2 × M3); door fin moved and thickened to 6 mm with a latch window. A web under the ramp removed every support. |
| 3 | — | Tunnel 29 × 30 × 59 mm inside (≈ 3 mm clearance per side over the 23 × 26 mm minimum, 2 mm in length for the ~80 mm / < 70 mm lock). Two M3 × 10 side screws clamp the lock against the left wall so the latch always lines up with the 17.5 × 20 mm windows in the front wall and the door fin; the door locks within 2–4° whether the body is 21 or 25 mm wide. Fin lowered to z −65 and widened; web, wedge and a 45° bevel under the tunnel keep it support-free (only bridges ≤ 30 mm and 45° chamfers). |

Physical test pending. Lesson 1 again: the lock was modelled from the catalogue before it was measured.

## Recurring lessons

1. **Catalogue vs. real part.** Measure purchased components before designing the parts that hold them (motor shaft, servo).
2. **Silent CAD failures.** Verify critical geometry (threads, teeth) with section cuts and point sampling.
3. **Fit is not function.** A part that fits can still fail under load; test with the actuator running.
4. **Design for FDM.** Avoid supports, keep loads parallel to the layers, and check wall thickness near holes and gear roots.
5. **Modularity pays off.** The fixed hole grids let the gripper be replaced twice and the hopper be added without reprinting anything else.
