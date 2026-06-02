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

1. **Abstract Specification (M0):** Defines the topological network, physical trains, and the absolute safety property: *No two trains can occupy the same physical space at the same time.*
2. **First Refinement (M1):** Introduces Virtual Sub-Sections (VSS), Radio Block Centre (RBC) position tracking, and basic Movement Authority (MA) allocation.
3. **Second Refinement (M2):** Introduces hybrid train fleets. Differentiates between fully equipped HL3 trains (with TIMS reporting via radio) and unequipped legacy trains (monitored via physical axle counters).
4. **Third Refinement (M3):** Integrates cyber-vulnerabilities, allowing malicious event injections (e.g., spoofed integrity reports, delayed VSS state transitions, and ghost train clearings).

---

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
* `attack_spoofed_integrity.atc`: An attacker spoofs a "Train Integrated" radio message for a split train, causing the RBC to prematurely clear a VSS block.
* `attack_dos_axle_counter.atc`: A Denial-of-Service attack blocks physical track vacancy updates, causing a hazard for unequipped trains.

### How to Import and Replay Traces:
1. In Rodin's *Event-B Explorer*, expand the project and double-click the **M3** machine to open it.
2. Right-click inside the open machine editor and select **Start ProB Animation / Model Checking**.
3. In the ProB Menu (top menu bar), navigate to **File** > **Open Trace...** (or **Load History...** depending on your ProB version).
4. Browse to the `/traces` directory and select one of the attack trace files.
5. Use the **History View** panel to click through the trace step-by-step. 
6. Observe the **State View** to see the exact moment the safety invariant is violated (highlighted in red).

---

## 🤝 Contributing & License
Feel free to fork this repository, add finer-grained attack vectors, or propose optimizations to the mitigation invariants. Distributed under the MIT License.
