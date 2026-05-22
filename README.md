# 🌿 ST dMRV — Ground Breaking
### *Revolutionising IoT in Forest Monitoring*

> **How might we develop an easily deployable dMRV system for carbon credits that is modular, self-healing, and maintenance-free?**

A drone-deployable, solar-powered IoT sensor network for autonomous forest carbon monitoring. Built on a LoRa mesh architecture with self-healing routing, K-Means optimised node placement, and a shock-resistant self-righting capsule designed to survive a 30m drone drop — no human setup required.

Built for **ST Engineering** as a Term 4 EPD Design Thinking Project at **Singapore University of Technology and Design (SUTD) 2025**, Group 7.

---

## 📖 Background

The growing demand for accurate carbon credit verification has exposed critical gaps in existing dMRV (digital Monitoring, Reporting, and Verification) systems deployed in forested environments. Current solutions suffer from:

- **Signal blockage by foliage** — dense canopy disrupts conventional wireless links
- **Laborious manual deployment** — existing systems require hands-on setup deep in forests
- **Expensive proprietary hardware** — solutions like Arable Mark 3, Teralytic, and RFCx Guardian are costly and non-modular

ST dMRV addresses all three with a fully autonomous, drone-deployed mesh sensor network.

---

## ✨ Key Features

### 📡 Seamless LoRa Mesh Network
- **LoRa (923MHz)** — Singapore's assigned frequency band; line-of-sight range up to 10km
- **Self-healing mesh routing** — if a node loses connection due to foliage growth or failure, data is automatically rerouted through neighbouring nodes
- **Meshtastic firmware** — open-source mesh networking stack running on each node
- Root node forwards aggregated data to the cloud via WiFi/Bluetooth

### 🚁 Drone-Automated Deployment
- Sensors are dropped from drone at **20–30m canopy height**
- **K-Means clustering algorithm** optimises node placement for maximum area coverage with minimum signal cost
- Placement simulator models tree obstructions and computes optimal centroid positions using Lloyd's Algorithm
- Zero human entry into the forest required

### ⚡ Dual Energy Source
- **5W monocrystalline solar panel** (100mm × 100mm) — real-world measured output ~3.6W @ 3.8V; MPPT controller maximises harvest
- **Kinetic energy harvester** — hamster-wheel-style generator using a 5V stepper motor as a generator, full-bridge rectified to 6V DC (~240mW output) as a proof of concept for animal-movement energy harvesting
- **Power-sharing circuit** — P-MOSFET automatically switches between solar and battery; protects battery health and restores MPPT functionality

### 🔵 Self-Righting Capsule
- **Outer shell:** Truncated icosahedron in **TPU** — chosen for elasticity and superior impact absorption over aluminium alloy and polycarbonate (validated via FEA simulation)
- **Inner capsule:** PETG plastic with snap-fit joints for easy electronics removal
- **Gimbal mechanism** — inspired by roly-poly toys; passive 2-axis rotation keeps solar panel and antenna pointing upward regardless of landing orientation
- Validated to survive **30m drop** with no plastic deformation

---

## 🔧 Hardware & Electronics

| Component | Specification |
|---|---|
| Microcontroller | ESP32 |
| Communication | LoRa (923MHz, Meshtastic) |
| Solar Panel | 5W monocrystalline, 100×100mm, 5V/1A |
| MPPT Controller | Maximises solar power extraction |
| Battery | LiPo, rechargeable |
| Power Switch | DMP1045U-7 P-MOSFET (Vds=-20V, Id=-4.2A) |
| Rectifier | MBR120ESFT3G Schottky diode (Vf=0.32V @ 1A) |
| Kinetic Generator | 5V stepper motor (reverse-driven), full-bridge rectifier |
| Outer Casing | TPU truncated icosahedron |
| Inner Capsule | PETG with snap-fit joints |

### Power Sharing Circuit Logic
```
When Vg (solar) < 1.7V  → PMOS ON  → Battery powers device (Vout ≈ 3.5V)
When Vg (solar) > 1.7V  → PMOS OFF → Solar powers device  (Vout ≈ 5.68V)
```
Simulated in LTSpice and validated with oscilloscope measurements.

---

## 🗺️ Node Placement Algorithm

Deployment locations are computed using **K-Means clustering**:
1. Target forest area is represented as a set of data points
2. Tree obstructions are modelled as signal-attenuating zones
3. K-Means finds optimal node centroids minimising total signal cost
4. Lloyd's Algorithm iteratively repositions nodes toward cluster centroids

> Node Placement Simulator: https://github.com/minlol1234/Forest-Node-Placement-Simulator

---

## 🔄 Prototyping Journey

| Iteration | Focus | Key Learning |
|---|---|---|
| Circuit v1 | Initial power circuit | Brown-out on long runs; solar/battery conflict; no trickle charge |
| Circuit v2 | Power-sharing PMOS design | Smooth source switching; restored MPPT; protected battery |
| Capsule P1 | Gimbal mechanism proof-of-concept | Passive righting works |
| Capsule P2 | Inner PETG capsule with snap-fit | Electronics fit and removal validated |
| Capsule P3 | Assembled outer TPU shell | Structural integrity tested |
| Capsule P4 | Thickened ring hinges | Resolved weak points at hinge joints |

---

## 🧪 Validation

| Domain | Method | Result |
|---|---|---|
| Power circuit | LTSpice simulation + oscilloscope | PMOS switching confirmed; 250mA peak to ESP32 validated |
| Solar output | Real-world measurement | 3.6W @ 3.8V (72% of rated 5W) |
| Kinetic output | Empirical stepper motor data | ~240mW @ 75 RPM, 6V |
| Node placement | K-Means + Lloyd's Algorithm | Optimal spatial coverage with obstruction modelling |
| Shell impact | FEA stress simulation (30m drop) | TPU sphere: lowest Von Mises stress (5.49 MPa vs 8.6 MPa yield) |
| Self-righting | Centre-of-mass verification | Solar panel and antenna remain upright post-landing |

---

## ⚠️ Known Limitations

- LoRa placement simulator does not yet account for RF signal loss through foliage
- Real solar yield under forest canopy often below 3W (vs 5W rated)
- Hamster wheel contributes only ~240mW intermittently — not sufficient standalone without large buffering
- Outer shell weight (many screws) exceeds ideal; integrated connectors or additive manufacturing would reduce this

---

## 🚀 Future Improvements

- Intuitive GUI for node placement simulation
- Mission-ready drone deployment mechanism integration
- AI-driven cloud computing for carbon data analysis
- Full-scale kinetic energy generator (replacing hamster wheel proof-of-concept)

---

## 👥 Team — CP03 Group 7

Edmund Lim · Gavin Tan · Kwan Jun Jie · Loh Kun Hong · Tan Min

---

## 🏫 Course Info

**Course:** Term 4 EPD Design Thinking Project (Structure & Material, Circuits & Electronics, Computational and Data-Driven Engineering)
**Institution:** Singapore University of Technology and Design (SUTD)
**Industry Partner:** ST Engineering
**Term:** Term 4 | Cohort 2027