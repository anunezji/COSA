# COSA: Community Solar Adoption Model

<p align="center">
  <img src="https://img.shields.io/badge/python-3.8+-blue.svg" alt="Python 3.8+">
  <img src="https://img.shields.io/badge/mesa-ABM-green.svg" alt="Mesa ABM">
  <img src="https://img.shields.io/badge/license-MIT-lightgrey.svg" alt="License">
  <a href="https://doi.org/10.1016/j.enpol.2023.113477"><img src="https://img.shields.io/badge/DOI-10.1016/j.enpol.2023.113477-blue" alt="DOI"></a>
</p>

**COSA** is an agent-based model (ABM) for simulating the adoption of rooftop photovoltaic (PV) systems in urban environments, with a focus on **community solar installations**. The model captures how building owners decide whether to install PV individually or jointly in a community PV installation based on economic, social, and attitudinal factors.

---

## Overview

Community solar enables multiple electricity users to share PV systems across buildings, unlocking economies of scale and higher self-consumption rates. COSA simulates the decision-making of building owners to evaluate how different policy designs influence PV adoption in cities.

COSA uses input from the open-source urban building energy model City Energy Analyst [(CEA)](https://github.com/architecture-building-systems/CityEnergyAnalyst), as well as socio-economic and geographical information system (GIS) data.

![Workflow of CEA+COSA models](https://ars.els-cdn.com/content/image/1-s2.0-S0301421523000629-gr1.jpg)

### Key Features

- **Theory of Planned Behavior** framework for adoption decisions
- **Adoption mode choice** compares individual and community adoption options
- **Community formation dynamics** including new communities and community growth over time
- **Policy scenario analysis** for evaluating the design of eligibility rules for community solar

For the case of the Alt-Wiedikon neighborhood in Zurich, Switzerland:
- **Nearly 5,000 heterogeneous agents** representing building owners with unique electricity demand and solar generation profiles
- **12 building use categories**: residential (single/multi-family), retail, office, industrial, hotel, school, hospital, and more
- **Hourly energy balances** from the City Energy Analyst (CEA) model
- **Calibrated and validated** against historical PV adoption data from Zurich, Switzerland

---

## Model Structure

COSA takes inputs from the CEA model, socio-economic and GIS data, and runs simulations based on policy scenairos following three main processes executed each time step (year):

![COSA overview](https://ars.els-cdn.com/content/image/1-s2.0-S0301421523000629-gr3.jpg)

### Agent States

| State | Description |
|-------|-------------|
| **Grid Consumer** | No PV installed |
| **Grid Prosumer** | Individual PV installation |
| **Community Prosumer** | Member of a community PV installation |

---

## Installation

### Prerequisites

- Python 3.8+
- [Mesa](https://mesa.readthedocs.io/) (agent-based modeling framework)

### Configuration

Simulations are configured through JSON experiment files containing:

- **Scenario parameters**: Policy design, eligibility rules
- **Calibration parameters**: Ideation variable weights
- **Economic parameters**: PV prices, electricity tariffs, subsidies

### Key Terminology

| Term | Description |
|------|-------------|
| **Experiment** | Simulation inputs defined in JSON file |
| **Scenario** | Unique combination of simulation parameters |
| **Batch** | Set of simulation runs for one scenario |
| **Run** | Single deterministic simulation |
| **Timestep** | One year in the simulation |

---

## Policy Scenarios

COSA was designed to evaluate community solar policy designs. The published study analyzed three scenarios:

| Scenario | Community Solar | Eligibility Rule |
|----------|-----------------|------------------|
| **IND** | Not allowed | — |
| **ZCS** | Allowed | Buildings in same zone (no street crossing) |
| **RCS** | Allowed | Buildings within 100-meter radius |

### Key Findings of Published Study

- Permissive community solar policy (RCS) increases PV adoption by **21%** compared to no community solar
- Investment subsidy efficiency improves by **~5%** with community solar
- Community growth over time is critical for realizing the full potential of community solar

---

## Repository Structure

```
COSA/
├── main.py              # Main entry point
├── COSA_Model.py        # SolarAdoptionModel class
├── COSA_Agent.py        # BuildingAgent class
├── COSA_Tools.py        # Economic evaluation, data collection, utilities
├── COSA_Data/           # Input data (building profiles, prices, etc.)
└── COSA_Outputs/        # Simulation results
```

---

## Data Requirements

COSA requires the following input data:

- **Building data**: Location, use category, ownership
- **Hourly electricity demand profiles** per building (from CEA or similar)
- **Hourly solar generation profiles** per building
- **Solar PV and electricity prices**
- **Policy parameters** (subsidies, feed-in tariffs, eligibility rules)

> **Note**: The model was applied to Alt-Wiedikon district in Zurich, Switzerland. Large input files are not included in the repository.

---

## Citing COSA

If you use COSA in your research, please cite the following paper:

```bibtex
@article{NunezJimenez2023,
  author  = {Nuñez-Jimenez, Alejandro and Mehta, Prakhar and Griego, Danielle},
  title   = {Let it grow: How community solar policy can increase PV adoption in cities},
  journal = {Energy Policy},
  volume  = {175},
  pages   = {113477},
  year    = {2023},
  doi     = {10.1016/j.enpol.2023.113477}
}
```

📄 **Paper**: [Energy Policy (2023)](https://doi.org/10.1016/j.enpol.2023.113477)

---

## Related Tools

- **[City Energy Analyst (CEA)](https://cityenergyanalyst.com/)**: Used to generate hourly electricity demand and solar generation profiles
- **[Mesa](https://mesa.readthedocs.io/)**: Python framework for agent-based modeling

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## Contact

For questions or collaboration inquiries, please open an issue or contact the authors through the corresponding author information in the [published paper](https://doi.org/10.1016/j.enpol.2023.113477).
