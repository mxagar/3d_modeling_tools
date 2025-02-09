# PrusaMINI+: A Guide

## Table of Contents

- [PrusaMINI+: A Guide](#prusamini-a-guide)
  - [Table of Contents](#table-of-contents)
  - [Printer Guide](#printer-guide)
    - [Setup](#setup)
    - [My Experience](#my-experience)
    - [Summary of Usual Workflow](#summary-of-usual-workflow)
    - [Helpful 3D Printer Tools](#helpful-3d-printer-tools)
  - [Slicer Guide](#slicer-guide)
    - [Beginner Guide](#beginner-guide)
      - [Platter Tab: Tools (Icons)](#platter-tab-tools-icons)
      - [Printer Settings Tab](#printer-settings-tab)
      - [Filaments Tab](#filaments-tab)
      - [Printer Settings Tab](#printer-settings-tab-1)
      - [Slice Now](#slice-now)
    - [Advanced Guide](#advanced-guide)
    - [Modifiers: Specific Parts with Specific Print Configurations](#modifiers-specific-parts-with-specific-print-configurations)

## Printer Guide

### Setup

Initial setup links:

- [MANUAL: 3D Printing Handbook](https://cdn.prusa3d.com/downloads/manual/prusa3d_manual_mini_en.pdf)
- [Start here: Software, firmware, material and articles (Prusa MINI+)](https://help.prusa3d.com/tag/mini-2)
- [Firmware updating (MINI/MINI+): Old Firmware Versions](https://help.prusa3d.com/article/firmware-updating-mini-mini_124784)
- [Original Prusa MINI - Calibration and First Print](https://www.youtube.com/watch?v=6Nip9EnSz7Q)

Issues:

- [Prusa3D Forum: The first layer taken off while printing  ](https://forum.prusa3d.com/forum/general-discussion-announcements-and-releases/the-first-layer-taken-off-while-printing/)
- [Prusa3D Forum: Life adjust Z - my way](https://forum.prusa3d.com/forum/original-prusa-i3-mk3s-mk3-assembly-and-first-prints-troubleshooting/life-adjust-z-my-way/)
- [r/prusa: How to prevent print from detaching mid-print](https://www.reddit.com/r/prusa/comments/10qvpaw/how_to_prevent_print_from_detaching_midprint/)
- [Prusa3D: First layer issues](https://help.prusa3d.com/article/first-layer-issues_1804)

Filaments:

- [Prusament: Filaments](https://prusament.com/materials/)

### My Experience

- I followed the official PDF guide for the setup.
- I had an old firmware which required to be updated in 2 steps.
  - First, an intermediate version
  - Then, the latest version
  - For more details: google Prusa MINI+ update firmware
- I has issues with the Z level calibration and the first print
  - I did not understand which was a good printing adhesion
  - Finally, I downloaded the model [`./models/calibration_utils/Life Adjust Z Mini PLA.gcode`](./models/calibration_utils/Life%20Adjust%20Z%20Mini%20PLA.gcode) and I printed it using the live Z adjustment (Control, Live Z).
  - I decided the Y value (close to `-1460`) and it worked.
  - Then, I printed some models (among others, the ship benchmark) to check everything was fine.

### Summary of Usual Workflow

- Get an STL
- Open the STL in the PrusaSlicer
- Set the properties of the slicing
- Slice Now
- Take the BGCODE file and copy it to the USB drive
- Plug it the USB drive into the Prusa
- Switch on Prusa
- Select print > Select file

### Helpful 3D Printer Tools

- Bar glue
- Wet towels
- Magnifying glass

## Slicer Guide

### Beginner Guide

Source: [PrusaSlicer Beginner Tutorial: Learn the basics](https://www.youtube.com/watch?v=_kIqMPNQNSw)

The first time we open the Prusa Slicer, the **installation wizard** is launched:

- Installation wizard: select printer, config, etc.
- Also other printers than Prusa supported!

Then, the home screen appears:

![Prusa Slicer Home Screen](./assets/slicer_home_screen.png)

In the upper right corner we can choose 3 modes:

- Beginner
- Normal: beginner settings + new ones
- Advanced: normal settings + new ones

The home screen has 4 tabs (and their tools vary depending on beginner/normal/... mode):

- Platter: 3D editor
- Printer: Choose a printer system preset
  - Layers and perimeter
  - Infill
  - Skirt and brim
  - Support material
- Filaments: Choose filament type and characteristics
  - PLA, etc.
  - Vendor: Prusament, generic, etc.
  - Diameter, density, cost, etc.
  - Cooling
  - Overrides
- Printers: we should have our printer selected; here we configure its parameters
  - Extruder:
    - Nozzle diameter: 0.4 mm
    - Travel lift height
    - Retraction length
- Printables: online store with free models

In the following, some notes on the tabs.

#### Platter Tab: Tools (Icons)

- In **Beginner Mode** (mode can be chosen in upper right corner, beside the login)
  - 3D view editor / Preview
    - In preview we can see the slices
  - Add model, remove
    - We can add several models
    - Formats: STL, 3MF, STEP, OBJ, AMF, SVG
      - Not GCODE!
  - Arrange: make models disjoint
  - Copy and Paste
  - Move
  - Scale
  - Rotate
  - Place on face
  - Measure
  - Variable layer height: we can add detail (thinner slices) depending on height
- In **Normal Mode**:
  - Cut: if the height of our model is too much, we can piece it into two objects!
  - ...

#### Printer Settings Tab

The printer settings appear in the right panel in the platter tab, but we can access to more printer features/settings if we open the specific tab.

Note that we choose a system preset, e.g.: `0.20mm SPEED @MINIIS 0.4`

- 0.2mm: layer height; the smaller, the more detail and thinner layers
- SPEED: whether speed of structure is favored
- @MINIIS: printer name
- 0.4: nozzle size

Depending on the preset, the settings change.
We have these settings:

- Layers and perimeters
  - Layer height
    - 0.2 mm is common; 0.1 is for very detailed, 0.5 for faster drafts
  - First layer height
    - 0.2 mm is common
    - Maybe it's a good idea to have a slightly thicker first layer to improve adhesion, if we have issues
  - Perimeter: the number of shell layers (stacked walls) the infilled body will have
    - 2 to 3 is normal
  - Horizontal shells: they refer to the top and bottom horizontal walls
    - 5 and 4 are common values
  - Seam: Determines the start point of each perimeter loop, it looks like a tiny zit on the model surface. We can choose a strategy depending on our need:
    - Random, aligned (arranged into lines), etc. 
- Infill: how strong structures are created by filling shells with structured matrices
  - Density: percentage of solid material vs. air
    - 15%-20% is common; choose higher if the piece needs to be strong.
  - Pattern: the filling pattern
    - Common: grid, gyroid
    - For thin objects: rectilinear
  - Top and bottom fill patterns
    - Common: monotonic
- Skirt and brim: the initial layer/lines/curves before the model is printed
  - Skirt: initial outer line
  - Brim: inner layer attached to the model, often left to 0 mm
- Support material: scaffolding in case we have horizontal hanging parts
  - If we need the scaffolding, we need to click/select *Generate support material*
  - Support material can be easily removed or snapped off from the model

Note: we can check the infill stiles in the platter tab, choosing the preview tool/view.

#### Filaments Tab

As in the printer settings, we can choose a preset, e.g., `Prusament PLA @MINIIS`.

- Filament
  - Color
  - Diameter: most are 1.75mm thick, but if we use other vendors we might need to change this value after measuring with a caliper.
  - The rest of the variables depend on the vendor and product
  - Temperature: these variables should be provided by the vendor
    - Bed temperature (initial layer and rest)
    - Nozzle temperature (initial layer and rest)
    - Usually, these values are provided in the filament roll
- Cooling: usually always on, unless we want to try expert stuff
- Filament overrides: retraction settings; we can leave them

#### Printer Settings Tab

Usually, we don't need to change anything here if the preset is correct; we can see the configuration of the extruder:

- Nozzle diameter
- Color
- Retraction travel lift and length
- ...

#### Slice Now

In the platter tab when the model is set as we want and all the configuration parameters have been correctly set in the other tabs, we can click on the **`Slice Now`** button (bottom left).

- Sliding the vertical control on the scene we can see the layers
- Sliding the horizontal control on the scene we can see the nozzle printing the layer
  - The GCode commands appear on a box
- We get different print statistic in a box overlaid on the scene:
  - Perimeter, infill, etc.
  - We can hide/visualize many things: travel, retractions, seams, etc.
  - Note that we can change the view mode (in the box) and the shown features are different
    - Feature type (default)
    - Speed
    - ...
- Bottom left panel: time and cost are displayed, among others

Finally, if we're happy with everything, we can click on **`Export G-code`** (bottom left).
The `.BGCODE` file will be exported; we need to copy it to the USB and then print it!

### Advanced Guide

Source: [PrusaSlicer Advanced & Expert Features Tutorial](https://www.youtube.com/watch?v=auWNk8jHc3E)

### Modifiers: Specific Parts with Specific Print Configurations

Source: [PrusaSlicer Modifiers Tutorial](https://www.youtube.com/watch?v=X2oZKiUS7bk)
