#### `Power-On Reset (POR):` It's an essential feature in any digital or mixed-signal chip, especially in system-on-chip (SoC) designs like Caravel, which include a RISC-V CPU, GPIOs, analog blocks, and user defined regions.

#### What is POR (Power-On Reset)?

A Power-On Reset (POR) circuit ensures that the system starts from a known state when power is applied. It generates a reset signal during the power-up sequence of the chip and often holds the reset line active until the supply voltage is stable and meets a specific threshold.

## 🧠 In Caravel, Why POR Is Important?
Caravel is designed to be reusable, with both a "management SoC" and a user project area. The POR block is crucial to:

* Reset the management SoC and user logic properly.
* Ensure reliable startup even if the user design has analog or mixed-signal components.
* Protect against undefined or metastable states on power-up.

## 📐 POR Circuit Characteristics & Specifications

##### In Caravel’s architecture (Sky130 tech), the POR circuit is defined with several key characteristics:

#### ✅ 1. Trigger Voltage (Vtrip):
* The voltage at which the POR triggers a reset signal.
* Usually around 0.6–0.8V for a 1.8V logic supply in Sky130.

#### ✅ 2. Delay Time (tPOR):
* How long the reset signal is held after power reaches a valid level.
* Ensures downstream logic stabilizes.
* Typically a few microseconds to milliseconds.

#### ✅ 3. Hysteresis:
* Prevents reset signal from toggling during noisy or unstable supply conditions.

#### ✅ 4. Output Type:
* Typically a digital signal sent to reset controllers in both management and user areas.

#### ✅ 5. Process-Voltage-Temperature (PVT) Tolerance:
* Must be designed to operate reliably across process corners, supply variations, and temperature ranges.

#### 🛠️ Implementation in Caravel
* In the Caravel SoC, the POR is typically part of the housekeeping block or included in the reset controller logic.

#### Key Signals:

* porb: Power-on reset bar (active-low).
* Drives reset logic in:
      * The RISCV core
      * GPIOs and control blocks
      * SPI flash interface

* User project wrapper

#### Integration Points:
* POR output feeds into reset muxes (hardware vs software-controlled resets).
* Can be monitored or overridden via test modes in simulation.

#### 🧪 Characterization Parameters
* In a silicon test or simulation setup, POR circuits are characterized with these parameters:


#### Parameter	Description	Typical Range:

| Parameter        | Description                             | Typical Range        |
| ---------------- | --------------------------------------- | -------------------- |
| Vtrip            | Threshold voltage for reset deassertion | 0.6V – 0.8V          |
| tPOR             | Reset hold time after Vdd is stable     | 10µs – 1ms           |
| Iq (quiescent)   | Leakage current                         | <1 µA                |
| Output swing     | Reset output voltage                    | Full logic swing     |
| Hysteresis width | Noise immunity range                    | 50–100 mV            |
| PVT variation    | Across process, voltage, temp corners   | Pass/fail thresholds |

#### 🧰 Tools for Simulation and Testing:

* ngspice (for analog behavior)
* Xyce (if detailed electrical modeling is needed)
* Verilog testbenches (for digital integration)
* Caravel’s test harness + OpenLane flow

#### 🔗 Further Reading / References
* Caravel GitHub: https://github.com/efabless/caravel
* Sky130 PDK Docs: https://skywater-pdk.readthedocs.io
* Efabless User Projects: Search for designs that include custom POR logic for reference.

