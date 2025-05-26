# 🧭 Crowd Spawner Design Guide (Updated)

## Overview

This guide defines the UI and behavior for the DAZ Crowd Spawner system, ensuring consistency, usability, and adherence to DAZ Studio scripting standards. It incorporates user-defined specifications and maintains existing design principles.

---

## 📐 UI Layout & Structure

- **Dialog Type**: `DzBasicDialog`
- **Fixed Size**: Width: 500px; Height: 620px (adjustable as needed)
- **Layout Method**: All widgets are positioned using `.setGeometry(x, y, width, height)`
- **Widget Types**:
  - `DzLabel` for text labels and section headers
  - `DzLineEdit` for text input fields
  - `DzCheckBox` for boolean options
  - `DzIntSlider` for numerical input sliders

---

## 🧩 Section Dividers

Sections are visually separated using centered `DzLabel` elements with bold text:

- **Required Options**
- **Optional Options**
- **Advanced Options**

These dividers help organize the UI into logical groups.

---

## 🛠️ Required Options

1. **Spawned Instance Name**
   - **Type**: `DzLineEdit`
   - **Default**: `"CrowdMember"`
   - **Description**: This name will be used for each of the spawned character instances. Expect to see names like 'CrowdMember', 'CrowdMember (2)', etc.

2. **Prefix**
   - **Type**: `DzLineEdit`
   - **Default**: `"CrowdFigure_"`
   - **Description**: Each figure in your scene subset is potentially used for spawning. The script identifies valid candidates based on this prefix. For example, 'CrowdFigure_CrowdMember-variant-suffix' with **CrowdFigure_** as the prefix.

3. **Marker Prefix**
   - **Type**: `DzLineEdit`
   - **Default**: `"CrowdMarker_"`
   - **Description**: Place objects (e.g., cubes, cylinders) as markers where you want crowd members to spawn. Each marker should have a label starting with **CrowdMarker_**, such as 'CrowdMarker_seat1'.

4. **Null Parent Name**
   - **Type**: `DzLineEdit`
   - **Default**: `"Crowd"`
   - **Description**: Name of the null object to which all spawned crowd members will be parented.

---

## ⚙️ Optional Options

5. **Use Variant**
   - **Type**: `DzCheckBox`
   - **Default**: `false`
   - **Description**: If enabled, only figures with both the specified prefix and variant string in their name (e.g., 'CrowdFigure_CrowdMember-**variant**-suffix') will be used.

6. **Variant String**
   - **Type**: `DzLineEdit`
   - **Default**: `""` (empty)
   - **Description**: Specify the variant string to match in figure names (e.g., 'CrowdFigure_CrowdMember-**variant**-suffix').

7. **Use Suffix**
   - **Type**: `DzCheckBox`
   - **Default**: `false`
   - **Description**: If enabled, only figures with the specified prefix, variant (if used), and suffix string in their name (e.g., 'CrowdFigure_CrowdMember-variant-**suffix**') will be used.

8. **Suffix String**
   - **Type**: `DzLineEdit`
   - **Default**: `""` (empty)
   - **Description**: Specify the suffix string to match in figure names (e.g., 'CrowdFigure_CrowdMember-variant-**suffix**').

9. **Overall Scale Offset**
   - **Type**: `DzCheckBox`
   - **Default**: `false`
   - **Description**: Enables uniform scaling of imported characters, maintaining aspect ratios across X, Y, and Z axes.

10. **Overall Scale Offset Percentage**
    - **Type**: `DzIntSlider`
    - **Range**: `-100%` to `100%`
    - **Default**: `0%`
    - **Description**: Specifies the percentage to uniformly scale imported characters if Overall Scale Offset is enabled.

11. **Randomize Overall Scale**
    - **Type**: `DzCheckBox`
    - **Default**: `false`
    - **Description**: Introduces size variance among imported crowd members.

12. **Randomize Overall Scale Variance Percentage**
    - **Type**: `DzIntSlider`
    - **Range**: `-100%` to `100%`
    - **Default**: `0%`
    - **Description**: Specifies the range of scale variance applied randomly to each crowd member if Randomize Overall Scale is enabled.

---

## 🧪 Advanced Options

13. **X Position Coordinate Offset**
    - **Type**: `DzIntSlider`
    - **Range**: `-200` to `200`
    - **Default**: `0`
    - **Description**: Adds an X-axis offset relative to the marker position.

14. **Y Position Coordinate Offset**
    - **Type**: `DzIntSlider`
    - **Range**: `-200` to `200`
    - **Default**: `0`
    - **Description**: Adds a Y-axis offset relative to the marker position.

15. **Z Position Coordinate Offset**
    - **Type**: `DzIntSlider`
    - **Range**: `-200` to `200`
    - **Default**: `0`
    - **Description**: Adds a Z-axis offset relative to the marker position.

16. **X Rotation Offset**
    - **Type**: `DzIntSlider`
    - **Range**: `-200` to `200`
    - **Default**: `0`
    - **Description**: Adds an X-axis rotation offset relative to the marker orientation.

17. **Y Rotation Offset**
    - **Type**: `DzIntSlider`
    - **Range**: `-200` to `200`
    - **Default**: `0`
    - **Description**: Adds a Y-axis rotation offset relative to the marker orientation.

18. **Z Rotation Offset**
    - **Type**: `DzIntSlider`
    - **Range**: `-200` to `200`
    - **Default**: `0`
    - **Description**: Adds a Z-axis rotation offset relative to the marker orientation.

19. **X Scale Offset**
    - **Type**: `DzIntSlider`
    - **Range**: `-100%` to `100%`
    - **Default**: `0%`
    - **Description**: Adds an X-axis scale offset relative to the imported scale and any previously specified overall and randomized scale.

20. **Y Scale Offset**
    - **Type**: `DzIntSlider`
    - **Range**: `-100%` to `100%`
    - **Default**: `0%`
    - **Description**: Adds a Y-axis scale offset relative to the imported scale and any previously specified overall and randomized scale.

21. **Z Scale Offset**
    - **Type**: `DzIntSlider`
    - **Range**: `-100%` to `100%`
    - **Default**: `0%`
    - **Description**: Adds a Z-axis scale offset relative to the imported scale and any previously specified overall and randomized scale.

---

## 🧭 Additional Guidelines

- **Tooltips**: Each field should have a tooltip displaying its description for user guidance.
- **Validation**: Input fields should include validation to ensure correct data types and ranges.
- **Defaults**: All fields should be initialized with their specified default values.
- **Layout Consistency**: Maintain consistent spacing and alignment across all UI elements for a clean and user-friendly interface.
