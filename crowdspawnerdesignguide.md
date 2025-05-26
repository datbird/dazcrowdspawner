# DAZ Crowd Spawner Design Guide

This design guide defines the core principles, rules, and constraints for the DAZ Crowd Spawner system. It serves as the blueprint for UI construction, spawn logic, versioning, and assistant behavior.

---

## Purpose

The DAZ Crowd Spawner is intended to populate 3D scenes with randomized, reusable figures using DAZ Studio 4.24. It must be reliable, controllable, and predictable across scenes and projects.

---

## Design Rules

### UI Rules

* Must use `DzBasicDialog` only.
* Use **absolute geometry placement** — no layout managers.
* All controls must match those defined in `crowdspawnerui.dsa`.
* **No DzSlider** — only `DzIntSlider` for numeric ranges.
* Use built-in Accept/Cancel buttons, no custom dialog controls.

### UI Sections

Include the following visual dividers:

* `Required Options`
* `Optional Options`
* `Advanced Options`

Labels must use asterisks (`**`) to simulate bolding:

```
**Figure Group Node:**
```

---

### Logic Rules

* Each marker must spawn **one** randomly selected figure from the provided pool.
* Figures must be instanced as children of the defined parent node.
* Random Y rotation and scale variance are optional.
* Use a seed value to ensure deterministic output if provided.
* Spawner must never alter existing scene data not under its assigned parent node.

---

## File Structure

```
dazcrowdspawner/
├── alpha/v1/
│   ├── crowdspawnerui.dsa
│   └── crowdspawnerlogic.dsa
├── release/v1/
│   ├── crowdspawnerui.dsa
│   └── crowdspawnerlogic.dsa
├── crowdspawnerdesignguide.md
└── README.md
```

---

## Assistant Behavior

When referencing or regenerating scripts:

* Do **not** rewrite or improve locked files unless explicitly instructed.
* Always pull scripts from the canonical GitHub path if given.
* Use current session file versions unless otherwise specified.

---

## Versioning

* All in-development scripts live in `/alpha`.
* Experimental or review-ready scripts go to `/beta`.
* Final locked scripts go to `/release`.
* Version folders (`v1`, `v2`, etc.) must not be overwritten without explicit version bump.

---

## Notes

This design guide is versioned and tracked like any other canonical file. All assistants and users must comply with its rules to ensure system integrity.
