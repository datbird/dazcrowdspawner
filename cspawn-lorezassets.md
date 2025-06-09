Crowd Spawner Logic Outline Using Lorenzo and Loretta JSON Configs

This document defines the full logic tree and data flow for generating crowd characters using the lorenzo.json and loretta.json configurations. It encapsulates all parameters and decisions defined in the spreadsheet and previous session notes.

Step 0: Determine Gender

Randomly choose between "Lorenzo" and "Loretta" with a 50/50 probability.

Step 1: Determine Ethnicity

For the selected gender, randomly pick an ethnicity from the config-defined list:

ethnicities[]

Step 2: Load Base Actor

Lorenzo:

Randomly select one .cr2 from:

BusinessSuit.cr2

Hoodie.cr2

T-Shirt.cr2

Located at:

Runtime/Libraries/Character/P3DA_LorenzoLorez

Loretta:

Always use:

!!LorettaLorez.cr2

Located at:

Runtime/Libraries/Character/P3DA_LorettaLorez

Step 3: Apply Skin MAT

From ethnicity-specific subdirectory:

materialPaths.skin, with ethnicity substituted in placeholder

Use skinFiles[ethnicity]

Step 4: Apply Hair and Face MAT (Lorenzo only)

From same materialPaths.skin subfolder:

Randomly select one of the MAT files from list of exact .pz2 files provided for that ethnicity (hair, beard, tash, etc.)

Step 5: Face Morphs

Randomly select 3 entries from namedFaceMorphs[]:

Assign each a random weight

Normalize the weights so their sum is 1.0

Apply morphs accordingly

Step 6: Apply Eye MAT

Randomly select one from:

eyeMats[]

Located in: materialPaths.eyes

Step 7: Apply Clothing MAT

Randomly select one from:

clothingMats[]

Located in: materialPaths.clothes

Step 8: Hair Prop (Loretta only)

Randomly select one hairstyle category:

Afro, BackTied, Pony, Hairband, Standard, Pigtails, Bob

If Afro is selected:

Only allow if ethnicity is African

Apply Afro morph value 1.0

Hair prop loaded from:

materialPaths.hairProps

Additional Options (TBD for Logic Integration)

Scale variance

Pose application

Face rotation/yaw

Figure parenting to null

Final Notes

File names must match spreadsheet exactly

No guesses: all asset names come directly from config

Logic is gender-, ethnicity-, and outfit-sensitive

Each marker spawns exactly one configured figure
