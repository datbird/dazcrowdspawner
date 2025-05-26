# DAZ Crowd Spawner

The DAZ Crowd Spawner is a custom DAZ Studio 4.24 scripting system designed for procedurally populating crowd scenes using precise marker/figure logic, a clean locked UI, and reproducible randomness.

This repository serves as the **single source of truth** for all canonical components of the DAZ Crowd Spawner system.

---

## Purpose
This project provides artists and technical directors with a consistent, non-destructive way to spawn randomized, yet controlled, character instances into complex DAZ Studio scenes. It aims to be highly deterministic, lightweight, and simple to use.

---

## Core Principles
- **Locked Logic**: All spawn logic is defined and version-controlled. No implicit rewrites or regenerations are allowed.
- **Locked UI**: The UI is fixed using `DzBasicDialog` with strict geometry-based layout, no frills.
- **Reproducibility**: Seeding is supported to produce identical crowd layouts.
- **Minimal Assumptions**: The spawner infers only what is explicitly defined in the configuration.

---

## Canonical Files
The following files represent the locked system definitions:

- `crowdspawnerui.dsa` – The exact dialog script that collects spawn configuration from the user.
- `crowdspawnerlogic.dsa` – The logic that performs marker-to-figure placement, randomization, and instancing.
- `crowdspawnerdesignguide.md` – The full specification governing the UI layout, behavioral expectations, and design rules.

All changes to these files must be intentional and documented.

---

## Usage
To use the DAZ Crowd Spawner:
1. Open `crowdspawnerui.dsa` in DAZ Studio's script editor.
2. Run the script to configure your crowd settings.
3. Hook the configuration output into `crowdspawnerlogic.dsa` for placement.

---

## License
MIT License unless otherwise specified.

---

## Contributions
This repo is not open to public contributions to ensure the integrity of locked components. Forks are allowed for customization, but must not be represented as canonical.

---

## Status
Actively maintained by the original author. Locked components are stable unless explicitly versioned.
