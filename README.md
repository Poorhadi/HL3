# Event-B Modeling of ERTMS/ETCS Hybrid Level 3 (HL3) Signaling System

This repository contains the formal Event-B specification, refinement chain, and ProB validation artifacts for the ERTMS/ETCS Hybrid Level 3 (HL3) railway signaling system. It models the core safety properties of HL3 and evaluates system resilience against targeted cyberattacks.

## 📌 Project Overview
The model formally verifies the interaction between the Radio Block Centre (RBC), Virtual Sub-Sections (VSS), Train Integrity Monitoring Systems (TIMS), and legacy trackside detection (axle counters). 

### Repository Structure
* **`/HL3`**: Contains the Rodin project archive (`.zip`) with the Event-B contexts and machines.
* **`/traces`**: Contains `.trace` execution trace files demonstrating system safety violations under specific cyberattack scenarios.

---

## 🏗️ Model Architecture & Refinement Chain

The system is developed using a stepwise refinement strategy to manage complexity and guarantee correctness-by-construction:

1. **Abstract Specification (M0):** ControlLoop
2. **First Refinement (M1):** ENV
3. **Second Refinement (M2):** Interlocking
4. **Third Refinement (M3):**  TrainController
5. **Forth Refinement (M3):**  Train
6. **Fifth Refinement (M3):**  TrainPositioEstimator
7. **Sixth Refinement (M3):**  VSScontrollers
---
Note: the current model only supports tampering and deletion attack scenarios. 
## 🛠️ Prerequisites & Setup

To explore, prove, and animate this model, you need the **Rodin Platform** and the **ProB** plugin.

### 1. Download Rodin
* Download **Rodin v3.x** for your operating system from SourceForge.
* Extract and launch the application.

### 2. Install ProB in Rodin
1. Open Rodin and navigate to **Help** > **Install New Software...**
2. In the "Work with" dropdown, select the pre-configured Rodin update site (or add `http://ccetb-st-provers.org` if not listed).
3. Expand the **ProB** category and check **ProB for Rodin**.
4. Click **Next**, accept the license agreement, and click **Finish**.
5. Restart Rodin when prompted.

---

## 🚀 Getting Started

### How to Import the Model
1. Clone this repository to your local machine.
2. Open Rodin and select **File** > **Import...**
3. Select **General** > **Existing Projects into Workspace** and click **Next**.
4. Choose **Select archive file**, browse to `/model/HL3_Signaling.zip`, and click **Finish**.
5. The project will appear in your *Event-B Explorer*. Rodin will automatically run the proof obligations in the background.

---

## 🕹️ Animation & Cyberattack Simulation (ProB Traces)

The `/traces` folder contains specific execution paths where the system transitions from a safe operational state to a collision state due to modeled cyber-exploits.

### Cyberattack Scenarios Modeled:
* `InjectionAttack.trace`: An attacker injects a "Position Report" radio message
* `Tameringattack.atc`: An attacker tampers with a "Position Report" radio message
---

## 🤝 Contributing & License
Feel free to fork this repository, add finer-grained attack vectors, or propose optimizations to the mitigation invariants. Distributed under the MIT License.
