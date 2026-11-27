### Wearable Motion Tracker

A compact, battery-powered custom PCB designed in **KiCad** for wearable motion and barometric sensing, built around the **ESP32-C3** wireless microcontroller with integrated USB Type-C Li-Po charging and 3.3V power regulation.

## Visuals


<img width="1916" height="1017" alt="Screenshot 2026-11-26 233524" src="https://github.com/user-attachments/assets/eb396ccf-4c68-4c99-960d-cf063d25f510" />
<img width="1527" height="982" alt="Screenshot 2026-11-26 224522" src="https://github.com/user-attachments/assets/2f0bef45-cb2a-4d03-8e29-301d9b18600d" />
<img width="1917" height="1023" alt="Screenshot 2026-11-26 233503" src="https://github.com/user-attachments/assets/99919c50-1a4b-4af4-b7a5-7649ee241192" />


## Hardware Architecture

* **Microcontroller & RF Link (`U1` — ESP32-C3):** Handles wireless telemetry and sensor processing with a cleared antenna keep-out zone along the board edge.
* **6-Axis Inertial Sensing (`U2` — MPU-6050):** Measures 3-axis acceleration and 3-axis angular velocity over the shared I2C bus (`SDA`, `SCL` with `4.7k` pull-up resistors).
* **Barometric & Environmental Sensing (`U3` — BMP280):** Provides barometric pressure, altitude estimation, and ambient temperature over I2C.
* **Battery & Charging Management (`J1`, `U4`, `BT1`, `SW1`):**
  * USB Type-C receptacle (`J1`) with `5.1k` CC configuration resistors (`R1`, `R2`)
  * `TP4056` (`U4`) single-cell Li-Po battery charger IC
  * Onboard battery cell connector (`BT1`) and physical power switch (`SW1`)
* **Voltage Regulation (`U5` — ME6211C33M5):** Steps down battery/input voltage to a regulated `3.3V` rail for the MCU and sensors with local decoupling capacitors (`C2`, `C3`, `C4`, `C6`).

## Repository Contents

* `Wearable_Motion_Tracker.kicad_pro` & `Wearable_Motion_Tracker.kicad_prl` — KiCad project and local workspace configuration
* `Wearable_Motion_Tracker.kicad_sch` — Schematic design
* `Wearable_Motion_Tracker.kicad_pcb` — 2D PCB layout and routing
* `Wearable_Motion_Tracker-NPTH.drl` & `Wearable_Motion_Tracker-PTH.drl` — Non-plated and plated through-hole drill files
* `Wearable_Motion_Tracker.dsn` & `Wearable_Motion_Tracker.cmp` — Design and component files

## Hardware Bring-Up Checklist

* [ ] Resolve all remaining unrouted ratsnest airwires (`Unrouted: 0`) and run DRC/ERC in KiCad with zero errors
* [ ] Verify USB Type-C charging current and `TP4056` status behavior on a single-cell Li-Po battery
* [ ] Confirm stable `3.3V` output from the `ME6211C33M5` regulator before powering the sensors
* [ ] Scan the I2C bus in firmware to verify `MPU-6050` and `BMP280` communication
