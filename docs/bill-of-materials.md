# Bill of materials

[← Back to README](../README.md#bill-of-materials)

Printed parts are listed in the [README](../README.md#printed-parts). This page lists everything else. Fastener counts marked "~" depend on how many grid holes you use.

## Electronics and actuators

| Component | Qty | Notes |
|---|:-:|---|
| Raspberry Pi 4 Model B, 8 GB + case, fan, 128 GB microSD | 1 | Ubuntu Server 24.04 LTS (64-bit), headless, SSH over Wi-Fi. USB 3.0 is required by the Kinect v2. |
| Arduino Mega 2560 | 1 | Connected to the Pi by a USB A–B cable (appears as `/dev/ttyACM0`). 8 of its 15 PWM outputs are used. |
| Microsoft Kinect v2 (Xbox One) + PC/USB adapter | 1 | RGB camera + time-of-flight depth sensor. |
| JGY370 12 V **130 RPM** worm-gear motor, M6 threaded output shaft | 2 | Tracks. The worm gear is self-locking. |
| JGY370 12 V **40 RPM** worm-gear motor, M6 threaded output shaft | 1 | Elevator. |
| BTS7960 / IBT-2 43 A H-bridge module | 3 | 2 tracks + 1 elevator (2 PWM pins each). |
| DS3218MG 20 kg·cm digital servo | 2 | Gripper and Kinect tilt. **Measure your servo**: the tab-to-shaft-tip distance of ours was ~8 mm shorter than the catalogue value. |
| TAU-S0837DL 12 V fail-secure solenoid lock | 1 | Hopper door. |
| 1-channel 5 V relay module | 1 | Drives the solenoid from an Arduino pin. |
| LiPo 3S 11.1 V 5000 mAh, XT90 (147 × 51 × 27 mm) | 1 | ~1 to 1.5 h of operation (estimate). |
| iMAX B3 Pro 2S/3S balance charger | 1 | Fits the charger enclosure (18/19). |
| XL4015 5 A step-down converter | 2 | One fixed at 5.0 V (Pi + Arduino), one at 5–6 V (servos). |
| 60 A terminal blocks | 2 | Separate positive and negative distribution. |
| XT90 male/female pigtails, 14 AWG | 1 set | Main plug and switch. |
| Jumper wires, heat-shrink tubing, cable ties, velcro strap | — | Wiring. |

## Bearings and shafts

| Item | Qty | Where |
|---|:-:|---|
| 6000ZZ bearing (10 × 26 × 8 mm) | 2 | Rear bearing brackets (05/06) |
| MR126ZZ bearing (6 × 12 × 4 mm) | 2 | Motor brackets (03/04) |
| 608ZZ bearing (8 × 22 × 7 mm) | 2 | Elevator tower floor and top plate |
| M10 threaded rod, cut to length | 2 | Rear axles (one per side) |
| M8 threaded rod, 255 mm | 1 | Lead-screw core |

## Fasteners by subsystem

| Subsystem | Fasteners |
|---|---|
| Chassis | M5 bolts + nuts for the brackets and plates (~); motor screws M2.5 × 16 + nuts; 4 × M4 bolts + nuts per wheel (16 total); front axles: 4 × M6 washers + 2 × M6 nyloc; rear axles: 4 × M10 washers + 2 × M10 thin nuts + 2 × M10 nyloc + threadlocker; optional 4 × M3 × 16 self-tapping pan-head screws to lock the front wheels |
| Power enclosures | 7 × M5 × 20 + nuts and washers (4 battery, 3 charger); 7 × M3 × 20 + nuts (5 lids, 2 plug holder) |
| Elevator | 6 × M5 × 20, 4 × M5 × 25 + nuts; 2 × M8 nuts; 1 × M6 nut + 1 × M6 nyloc; 8 × M3 × 20 (4 motor, 4 tool plate + nuts) |
| Kinect mount | 16 × M3 × 20 + nuts; 1 × M5 × 20 hex-head bolt + M5 nyloc + washer |
| Gripper | 4 × M3 × 15 + nuts (flange); 4 × M3 + nuts (servo tabs); servo horn kit screws |
| Hopper | 2 × M5 + nuts (bracket to plate); 3 × M3 × 15 + nuts (bracket to body); 2 × M3 × 15 (door hinge); 4 × M3 + nuts (solenoid cover) |

## Filament

| Material | Used for |
|---|---|
| PETG (black) | All structural parts |
| TPU 95A (black) | Tracks 09 and 10 |
