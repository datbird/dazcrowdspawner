# GPT Session State

## Initialize
- Fetch `alpha/v5/crowdspawnerui.dsa`
- Fetch `alpha/v1/crowdspawnerlogic.dsa`
- Fetch `crowdspawnerdesignguide.md`
- Fetch `gpt_instructions.md`
- Fetch alpha/v4/crowdspawnerui.dsa
- Fetch alpha/v1/crowdspawnerlogic.dsa
- Fetch crowdspawnerdesignguide.md
- Fetch gpt_instructions.md

Current Version Locked: alpha/v5/crowdspawnerui.dsa
Current Version Locked: alpha/v1/crowdspawnerlogic.dsa
---

## Sync Behavior
- Treat `alpha/v5/crowdspawnerui.dsa` as the current editable UI script
- Treat `alpha/v1/crowdspawnerlogic.dsa` as the current editable logic script
- Use `crowdspawnerdesignguide.md` as the definitive source for layout, field order, descriptions, and sectioning
- Enforce all assistant constraints and behaviors from `gpt_instructions.md`
- Recognize all versions in `/alpha`, `/beta`, and `/release`, and ask the user for clarification when ambiguity or updates are detected


## Current Script Version



## Notes
- `DzDialog` successfully implemented with full field layout
- All 21 UI fields visible at once (Required, Optional, Advanced)
- Accept and Cancel buttons functional
- Layout confirmed in DAZ Studio 4.24 Premier
- Vertical divider placeholder removed (styleSheet not supported natively)
- Ready for logic/validation
- **Functionality:** Exports material presets for the selected parent figure and its immediate children (excluding "Hip"), with user-selectable inclusion via checkboxes.
- **Features:**
  - Dynamic parent selection based on current scene selection.
  - Dialog box with checkboxes for each direct child node (excluding "Hip").
  - Suppression of file name prompts during export.
  - Exports material presets to a predefined directory.
- **Known Warnings:** `libpng warning: iCCP: known incorrect sRGB profile` messages may appear during execution; these are harmless and can be safely ignored.

Recent Updates:

UI has been finalized for v5

Required fields validated: accept button only activates if fields filled

Removal of static description labels in favor of tooltips

Bold section dividers

Double-pipe visual column divider added

Adjusted UI layout size (now 1000x552)

Final script tested and committed to repo

Decimator Integration Testing:

Decimator script failed using App.getPlugin and Decimator direct reference

Revised approach assumes plugin is active but script still errors out

Decimator not directly scriptable via standard exposed API

Decimation settings best preserved in full scenes or subsets

Crowd Optimization Guidance:

Target ~20k triangle count per character for reasonable real-time performance

Gen3 figures acceptable for background crowds (wardrobe, hair compatibility discussed)

Mesh-based hair significantly increases decimation load

Strand-based hair preferred for performance

Asset Import and Customization:

Morph Loader (Advanced/Pro) for OBJ import as morphs

Custom sliders and actor properties are script-addressable

No direct detection of applied pose files (transforms only)

Smart Content/Asset DB Handling:

Custom Smart Content filters for Gen3 content

Asset-based scripts cannot trivially detect originating products

Subset/scene .duf files used as scripted triggers for logic

Omni Hair Tool Suite:

Toolset provides procedural SBG generation, grooming, decimation-like optimization

Allows more visually acceptable low-poly hair vs. Decimator

Next Development Goals:

Begin scripting logic components for v5 logic processor

Reuse patterns established in v1 logic (avoid Qt libraries, follow stable Dz functions)

Add functional elements for character spawning, marker detection, asset loading

Design Guide Synced:

Design guide updated to reflect new layout, logic behavior, and UI standards

Notes:

Future UI changes will target v6

All decimation testing should isolate hair/wardrobe geometry from figure mesh

Evaluate lightweight figure variants for efficient crowd simulation


## Dialog Box Function

```javascript
function createChildSelectionDialog(title, message, childLabels) {
    var dialog = new DzDialog();
    dialog.caption = title;
    dialog.setFixedSize(400, 100 + 30 * childLabels.length);

    var label = new DzLabel(dialog);
    label.text = message;
    label.wordWrap = true;
    label.setGeometry(10, 10, 380, 40);

    var checkboxes = [];
    for (var i = 0; i < childLabels.length; i++) {
        var cb = new DzCheckBox(dialog);
        cb.text = childLabels[i];
        cb.checked = true;
        cb.setGeometry(20, 60 + i * 30, 360, 25);
        checkboxes.push(cb);
    }

    var okButton = new DzPushButton(dialog);
    okButton.text = "OK";
    okButton.setGeometry(160, 60 + childLabels.length * 30, 80, 30);
    okButton.clicked.connect(function () {
        dialog.close();
    });

    dialog.setAcceptButton(okButton);
    dialog.exec();

    return checkboxes.filter(function(cb) { return cb.checked; }).map(function(cb) { return cb.text; });
}
