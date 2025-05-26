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

## Directives and Constraints

### Required Options

1. **Spawned instance name?** (default: `CrowdMember`)
   *This name will be be used to for each of the spawned character instaces. So expect to see each instance to have a name such as 'CrowdMember', 'Crowdmember (2)' etc etc.*

2. **Prefix?** (default: `CrowdFigure_`)
   *Each of the figures contained in your scene subset are potentially used to import and spawn into the scene. In order for the script to decide which ones to import, it looks at the figure parent object and determines if it's a valid candidate to import based off of the specified prefix. eg 'CrowdFigure\_CrowdMember-variant-suffix' with **CrowdFigure\_** being bold.*

3. **Marker prefix?** (default: `CrowdMarker_`)
   *You are to place objects of your choosing (such as a primitive cube, cylinder, etc) to mark where all you would like crowd members to be spawned. Each of these 'markers' are to have a prefix in their label such as 'CrowdMarker\_seat1' so that the script can identify where to put the newly spawned crowd members.*

4. **Null Parent Name?** (default: `Crowd`)
   *This is the name of the null object that this script will parent all of the spawned crowd members to.*

### Optional Options

5. **Use variant?** (checkbox, default: false)
   *Enables filtering of characters by a "variant" string in addition to the prefix. eg 'CrowdFigure\_CrowdMember-**variant**-suffix'.*

6. **Variant string** (string, default: empty)
   *If variant is enabled, this string is used to match variants. eg 'CrowdFigure\_CrowdMember-**variant**-suffix'.*

7. **Use suffix?** (checkbox, default: false)
   *Enables filtering by a "suffix" in addition to prefix and variant. eg 'CrowdFigure\_CrowdMember-variant-**suffix**'.*

8. **Suffix string** (string, default: empty)
   *Used when suffix is enabled. eg 'CrowdFigure\_CrowdMember-variant-**suffix**'.*

9. **Overall scale offset?** (checkbox, default: false)
   *Maintains aspect ratio of XYZ scaling for imported character.*

10. **Overall scale offset percentage** (`DzIntSlider`, range: -100% to 100%, default: 0%)
    *Adjusts the imported character's overall scale.*

11. **Randomize overall scale?** (checkbox, default: false)
    *Introduces size variance among crowd members.*

12. **Random scale variance percentage** (`DzIntSlider`, range: -100% to 100%, default: 0%)
    *Specifies max percentage range to scale randomly per character.*

### Advanced Options

13. **X position coordinate offset** (`DzIntSlider`, -200 to 200, default: 0)
    *X offset relative to marker.*

14. **Y position coordinate offset** (`DzIntSlider`, -200 to 200, default: 0)
    *Y offset relative to marker.*

15. **Z position coordinate offset** (`DzIntSlider`, -200 to 200, default: 0)
    *Z offset relative to marker.*

16. **X rotation offset** (`DzIntSlider`, -200 to 200, default: 0)
    *X rotation offset relative to marker.*

17. **Y rotation offset** (`DzIntSlider`, -200 to 200, default: 0)
    *Y rotation offset relative to marker.*

18. **Z rotation offset** (`DzIntSlider`, -200 to 200, default: 0)
    *Z rotation offset relative to marker.*

19. **X scale offset** (`DzIntSlider`, -100% to 100%, default: 0)
    *X scale offset relative to imported scale and previous scaling.*

20. **Y scale offset** (`DzIntSlider`, -100% to 100%, default: 0)
    *Y scale offset relative to imported scale and previous scaling.*

21. **Z scale offset** (`DzIntSlider`, -100% to 100%, default: 0)
    *Z scale offset relative to imported scale and previous scaling.*

---

## Logic Rules

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
