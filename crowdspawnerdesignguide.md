# Crowd Spawner UI Design Guide (v5)

## File Structure

* **UI Script**: `/alpha/v5/crowdspawnerui.dsa`
* **Logic Script**: (still using v1 for now)

## General Layout

* **Dialog Type**: `DzDialog`
* **Fixed Dimensions**: `1000 x 552`
* **Grid Layout**: Two-column arrangement
* **Visual Divider**: Vertical ASCII divider (`||`) between columns

## Section Organization

* **Left Column**:

  * Required Options (Top)
  * Optional Options (Middle)
* **Right Column**:

  * Advanced Options

### Section Headers

* Section headers use bold ASCII divider labels:

  * `====== Required Options ======`
  * `====== Optional Options ======`
  * `====== Advanced Options ======`

## Field Types

* **Labels**: `DzLabel`
* **Text Inputs**: `DzLineEdit`
* **Check Boxes**: `DzCheckBox`
* **Sliders**: `DzIntSlider`

## Field Formatting Rules

* Fields placed with fixed `.setGeometry(x, y, w, h)` values
* Descriptions **replaced** with `toolTip` for each interactive field
* Tooltips mirror original descriptions as closely as possible
* Labels/inputs grouped in pairs (label above, input below)

## Validation Behavior

* **Required Fields**:

  * Spawned Instance Name
  * Prefix
  * Marker Prefix
  * Null Parent Name
* **Validation Logic**:

  * If any required field is empty, **Accept button is disabled**
  * Validation triggers on `textChanged` signals from these fields
* **No red border** or visual warning — just disables Accept

### Code Sample: Validation Logic

```javascript
function validateForm() {
    var filled = inputInstanceName.text.trim() !== "" &&
                 inputPrefix.text.trim() !== "" &&
                 inputMarkerPrefix.text.trim() !== "" &&
                 inputNullParent.text.trim() !== "";
    btnAccept.enabled = filled;
}

inputInstanceName.textChanged.connect(validateForm);
inputPrefix.textChanged.connect(validateForm);
inputMarkerPrefix.textChanged.connect(validateForm);
inputNullParent.textChanged.connect(validateForm);

validateForm();
```

## Buttons

* **Accept**:

  * Created with `DzPushButton`
  * Accept behavior handled via `CrowdSpawnerDialog.setAcceptButton(btnAccept);`
  * No custom handler; closure managed by DAZ after validation passes
* **Cancel**:

  * Triggers `CrowdSpawnerDialog.close();`

## Style & Convention

* Field order and section grouping must follow this guide
* All tooltips must reflect the latest specification content
* No experimental DAZ UI APIs or alternate widget types may be used

## Explicitly Out of Scope (v5)

* Preset save/load system
* In-place red-border visual validation
* Any Qt or stylesheet-based formatting
* External image use for dividers or layout

---

This guide defines the authoritative specification for all UI work under v5. All script updates must strictly comply with this design structure.
