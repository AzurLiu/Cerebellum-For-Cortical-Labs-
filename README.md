<p align="center">
  <h1 align="center">Senxe Cerebellum v4.0 (Pure Wetware)</h1>
  <p align="center">
    <strong>100% Biologically-Grounded Motor Control for Industrial Robotics</strong><br>
    Interfacing Cortical Labs CL1 Biological Neurons with Robotic Arms
  </p>
</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> •
  <a href="#core-philosophy">Core Philosophy</a> •
  <a href="#architecture">Architecture</a> •
  <a href="LICENSE">MIT License</a>
</p>

---

> *"What if we stopped training artificial networks to mimic biology — and just used the biology itself?"*

**Senxe Cerebellum** is a 100% Pure Wetware control framework that directly interfaces **Cortical Labs CL1** biological neurons with the Franka Panda 7-DoF robotic arm. 

In v4.0, we have violently purged all Reinforcement Learning (PPO) baselines, `MockNeurons`, and software fallbacks. The system enforces a strict biological hardware dependency to solve the industrial **RoboSuite NutAssembly** task. It relies purely on physical force/torque sensors mapped to a 64-channel MEA (Microelectrode Array).

---

## Core Philosophy

### 1. Zero Software Fallbacks (Pure Biology)
We do not simulate biology. The codebase strictly requires the Cortical Labs `cl-sdk`. If it is not a real biological organoid, the code will refuse to execute. We have eliminated all Deep Learning training wheels.

### 2. Neuromorphic Event-Driven Sparse Coding (VIE)
The **Virtual Interference Encoding (VIE)** module translates continuous RoboSuite force/torque sensory data into event-driven Delta Tracking. The culture only fires when physical parameters *change*, drastically improving SNR and completely preventing global overstimulation seizures.

### 3. Closed-Loop Homeostasis
Biological tissue exhausts if constantly stimulated. Channel adaptation (`channel_gain`) is physically hooked into the stimulation amplitude and burst frequency, dynamically preventing cellular fatigue while preserving sensitive pathways.

### 4. Antagonistic Decoding
Motor output follows the biological **flexor/extensor antagonistic** principle. 
The 64 channels are perfectly balanced and mapped across the 7-DoF spatial and gripper dimensions, eliminating dimensional dominance. 

---

## Quick Start

### Hardware Requirements
You **MUST** have access to Cortical Labs CL1 biological hardware.

```bash
# Clone and install
git clone https://github.com/AzurLiu/Senxe-Cerebellum.git
cd Senxe-Cerebellum
pip install -r requirements.txt
pip install cl-sdk

# Set MuJoCo renderer (macOS)
export MUJOCO_GL=glfw

# Run the biological assembly benchmark
python senxe_demo_robosuite.py
```

---

## Output Artifacts

| File | Description |
|:---:|:---|
| `cl1_nutassembly.mp4` | CL1 bio-agent execution video with Cyberpunk F/T Bloom HUD overlay. |

*(Note: Generating this video requires a successful run on the physical CL1 hardware).*

---

## Architecture

### Project Structure

```text
senxe-cerebellum/
├── senxe_demo_robosuite.py    # Main: RoboSuite NutAssembly (native F/T sensors)
├── core/
│   ├── neurons.py             # CL1 neural interface (Strict Hardware Enforced)
│   ├── decoder.py             # Antagonistic motor decoding (flexor/extensor)
│   ├── pdi.py                 # Physical Disturbance Index (FEP explore/exploit)
│   ├── curiosity.py           # Neural intrinsic curiosity (firing-pattern novelty)
│   ├── vie.py                 # Virtual Interference Encoding module
│   ├── hud.py                 # HUD rendering and Bloom pipeline
│   └── video.py               # Video generation utilities
├── tests/
│   └── test_core.py           # Unit tests
└── README.md
```

### Biological Control Pipeline

```text
┌─────────────────────────────────────────────────────────────────┐
│                    SENXE CONTROL LOOP                            │
│                                                                 │
│  ┌──────────┐    ┌─────────┐    ┌──────────────┐    ┌────────┐ │
│  │ RoboSuite│───▶│   VIE   │───▶│  64-ch MEA   │───▶│Antagon.│ │
│  │  Sensors │    │ Encoder │    │ (Real CL1)   │    │Decoder │ │
│  │ F/T, Pos │    │(Sparse) │    │              │    │        │ │
│  └──────────┘    └─────────┘    └──────┬───────┘    └───┬────┘ │
│       ▲                                │                │      │
│       │                          ┌─────▼─────┐    ┌─────▼────┐ │
│       │                          │ Predictable / │    │  Action  │ │
│       └──────────────────────────│ Unpredictable Stimulus │◀───│  Output  │ │
│              (env.step)          │ Injection  │    │ (7D OSC) │ │
│                                  └─────┬─────┘    └──────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

---

## Author

**Azur (Jiahao)** — 18-year-old independent developer, incoming University of Alberta student.

Built from scratch as an exploration into biological computation and neural motor control for industrial robotics. This project represents a first-principles approach to neuromorphic engineering: rather than training artificial networks to approximate biological dynamics, Cerebellum interfaces directly with living biological neural tissue to solve real-world motor control problems.

---

Copyright © 2026 Azur (Jiahao). Licensed under the MIT License.
