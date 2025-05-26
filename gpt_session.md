# DAZ Crowd Spawner GPT Session State

This file is used to initialize a new session for the DAZ Crowd Spawner GPT Assistant. Upon loading this file, the assistant should sync with all relevant files and enforce behavior based on the design guide and locked instruction set.

---

## Initialize
- Fetch `alpha/v1/crowdspawnerui.dsa`
- Fetch `alpha/v1/crowdspawnerlogic.dsa`
- Fetch `crowdspawnerdesignguide.md`
- Fetch `gpt_instructions.md`
- Fetch alpha/v4/crowdspawnerui.dsa
- Fetch alpha/v1/crowdspawnerlogic.dsa
- Fetch crowdspawnerdesignguide.md
- Fetch gpt_instructions.md


---

## Sync Behavior
- Treat `alpha/v1/crowdspawnerui.dsa` as the current editable UI script
- Treat `alpha/v1/crowdspawnerlogic.dsa` as the current editable logic script
- Use `crowdspawnerdesignguide.md` as the definitive source for layout, field order, descriptions, and sectioning
- Enforce all assistant constraints and behaviors from `gpt_instructions.md`
- Recognize all versions in `/alpha`, `/beta`, and `/release`, and ask the user for clarification when ambiguity or updates are detected

---

## Session Notes

## Notes
- `DzDialog` successfully implemented with full field layout
- All 21 UI fields visible at once (Required, Optional, Advanced)
- Accept and Cancel buttons functional
- Layout confirmed in DAZ Studio 4.24 Premier
- Vertical divider placeholder removed (styleSheet not supported natively)
- Ready for logic/validation in alpha v5

TODO
- [ ] Validate implementation of all 21 fields and their descriptions per the design guide
- [ ] Confirm variant/suffix matching logic functions as described
- [ ] Ensure all scaling logic uses `DzIntSlider` and is clamped properly
- [ ] Await next edits to determine when to advance to `beta/v1/`
- [ ] Encourage saving session state after key updates to retain continuity
