# GPT Session File

## Session Metadata
- **Session Date**: 2025-05-30
- **DAZ Studio Version**: 4.24
- **Active Folder**: `/beta/`
- **CrowdSpawnerUI Version**: `alpha/v5/crowdspawnerui.dsa`
- **CrowdSpawnerLogic Version**: `alpha/v1/crowdspawnerlogic.dsa`
- **Repository**: [dazcrowdspawner GitHub](https://github.com/datbird/dazcrowdspawner)


## Initialize
- Fetch `alpha/v5/crowdspawnerui.dsa`
- Fetch `alpha/v1/crowdspawnerlogic.dsa`
- Fetch `crowdspawnerdesignguide.md`
- Fetch 'gpt_instructions.md'


## Current Script Version
- Current Version Locked: alpha/v5/crowdspawnerui.dsa
- Current Version Locked: alpha/v1/crowdspawnerlogic.dsa
- Current Version Locked: alpha/v1/surfaceDazFigtoImportedFig.dsa


## Canonical Files

- `crowdspawnerdesignguide.md`
- `gpt_instructions.md`
- `gpt_session.md`

## Sync Behavior
- Treat `alpha/v5/crowdspawnerui.dsa` as the current editable UI script
- Treat `alpha/v1/crowdspawnerlogic.dsa` as the current editable logic script
- Use `crowdspawnerdesignguide.md` as the definitive source for layout, field order, descriptions, and sectioning
- Enforce all assistant constraints and behaviors from `gpt_instructions.md`
- Recognize all versions in `/alpha`, `/beta`, and `/release`, and ask the user for clarification when ambiguity or updates are detected

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
- UI has been finalized for v5
- Required fields validated: accept button only activates if fields filled
- Removal of static description labels in favor of tooltips
- Bold section dividers
- Double-pipe visual column divider added
- Adjusted UI layout size (now 1000x552)
- Final script tested and committed to repo
- Use only DzDialog, DzPushButton, DzComboBox, DzLineEdit, DzCheckBox, DzLabel per verified working files.
- Do not introduce QWidget, layouts, or addWidget patterns.
- Future UI changes will target v6
- Future Logic changs will target V2
- Surface Match Prototype now fully matches and transfers shaders with summary output.
- UI test confirmed compatibility for all interactive types.



## Crowd Optimization Guidance:
Target ~20k triangle count per character for reasonable real-time performance
Gen3 figures acceptable for background crowds (wardrobe, hair compatibility discussed)
Mesh-based hair significantly increases decimation load
Strand-based hair preferred for performance

## Asset Import and Customization:
Morph Loader (Advanced/Pro) for OBJ import as morphs
Custom sliders and actor properties are script-addressable
No direct detection of applied pose files (transforms only)

## Smart Content/Asset DB Handling:
Custom Smart Content filters for Gen3 content
Asset-based scripts cannot trivially detect originating products
Subset/scene .duf files used as scripted triggers for logic


## Next Development Goals:
Begin scripting logic components for v5 logic processor
Reuse patterns established in v1 logic (avoid Qt libraries, follow stable Dz functions)
Add functional elements for character spawning, marker detection, asset loading


## Design Guide Synced:
Design guide updated to reflect new layout, logic behavior, and UI standards

## Verified Dialog Components

### `createChildSelectionDialog`

```javascript
function createChildSelectionDialog(title, message, options) {
    var dialog = new DzDialog();
    dialog.caption = title;
    dialog.setFixedSize(400, 160);

    var lbl = new DzLabel(dialog);
    lbl.text = message;
    lbl.setGeometry(10, 10, 380, 20);

    var combo = new DzComboBox(dialog);
    combo.setGeometry(10, 40, 380, 25);
    for (var i = 0; i < options.length; i++) {
        combo.addItem(options[i].getLabel ? options[i].getLabel() : options[i]);
    }

    var btnAccept = new DzPushButton(dialog);
    btnAccept.text = "OK";
    btnAccept.setGeometry(220, 110, 80, 30);

    var btnCancel = new DzPushButton(dialog);
    btnCancel.text = "Cancel";
    btnCancel.setGeometry(310, 110, 80, 30);
    btnCancel.clicked.connect(function () {
        dialog.close();
    });

    dialog.setAcceptButton(btnAccept);

    var selectedIndex = -1;
    btnAccept.clicked.connect(function () {
        selectedIndex = combo.currentItem;
        dialog.close();
    });

    dialog.exec();

    if (selectedIndex < 0 || selectedIndex >= options.length) {
        return null;
    }

    return options[selectedIndex];
}
```

### `test_child_selection_ui_full.dsa` 
```javascript


// Use this to test the previously referenced "createChildSelectionDialog" function.
// Comprehensive UI test for combo, checkboxes, and line edits

var testDialog = new DzDialog();
testDialog.caption = "UI Element Test";
testDialog.setFixedSize(400, 300);

var lblCombo = new DzLabel(testDialog);
lblCombo.text = "Choose an option:";
lblCombo.setGeometry(10, 10, 200, 20);

var cmbOptions = new DzComboBox(testDialog);
cmbOptions.setGeometry(10, 35, 200, 20);
cmbOptions.addItem("Option A");
cmbOptions.addItem("Option B");
cmbOptions.addItem("Option C");

var chkSample = new DzCheckBox(testDialog);
chkSample.text = "Enable feature";
chkSample.setGeometry(10, 70, 200, 20);
chkSample.checked = true;

var lblInput = new DzLabel(testDialog);
lblInput.text = "Enter label:";
lblInput.setGeometry(10, 100, 200, 20);

var txtInput = new DzLineEdit(testDialog);
txtInput.setGeometry(10, 125, 200, 20);
txtInput.text = "Default Text";

var btnOK = new DzPushButton(testDialog);
btnOK.text = "OK";
btnOK.setGeometry(100, 200, 80, 30);

btnOK.clicked.connect(function() {
    var result = "Combo Selection: " + cmbOptions.currentText + "\n";
    result += "Checkbox is " + (chkSample.checked ? "checked" : "unchecked") + "\n";
    result += "Text Input: " + txtInput.text;
    print(result);
    testDialog.close();
});

testDialog.setAcceptButton(btnOK);
testDialog.exec();
```
