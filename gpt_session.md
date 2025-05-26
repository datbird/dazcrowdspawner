DAZ Crowd Spawner GPT Session State

This file is used to initialize a new session for the DAZ Crowd Spawner GPT Assistant. Upon loading this file, the assistant should sync with all current alpha files and enforce behavior based on the design guide and locked instruction set.

Initialize

Fetch alpha/v1/crowdspawnerui.dsa

Fetch alpha/v1/crowdspawnerlogic.dsa

Fetch crowdspawnerdesignguide.md

Fetch gpt_instructions.md

Sync Behavior

Enforce all UI layout, naming, and behavior rules from crowdspawnerdesignguide.md

Use alpha/v1/crowdspawnerui.dsa as the active configuration UI script

Use alpha/v1/crowdspawnerlogic.dsa as the active spawn logic script

Treat gpt_instructions.md as the canonical instruction set for assistant behavior

Session Notes

These items summarize context or tasks from the previous session. Use this section to retain progress between assistant sessions.


- [ ] Update current UI script to match requested features from the design guide.
- [ ] Update current Logic script to match UI inputs. Bolt the two scripts onto each other.
