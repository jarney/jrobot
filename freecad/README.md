# CAD Design Introduction

The JRobot design is broken into a number of different FreeCAD files linked together.
This approach was taken for a few different reasons:

* By breaking the design into multiple files, it increases the likelihood that
  it can be run on low-spec machines because each individual file is responsible for
  only a few parts.
* By breaking up the design into subsystems, the overall design is easier for a human
  to understand each subsystem without having to understand the whole design at once,
  thereby reducing cognitive overhead when making design changes.
* By separating the design, a separate consideration can be made for the individual components,
  the assembly, and the print orientation (or manufacture process) without having them dependent 
  on one another.

The design approach is to keep as much of the design parametric as possible.  In most cases, this means
driving the design based on "Master Sketches".  These master sketches are not rendered directly into parts,
but keep constraints for various parameters like "X Axis outer diameter" shared across all of the components
that need to be driven by that parameter.  This means that many practical changes to the design can be done
by chaging these key driving constraints and recalculating the downstream parts.

## Dependencies

* FreeCAD 0.21+
* Assembly4 workbench
* Parts workbench

## Restrictions

Note that each part must have a single body.  This restriction is imposed by the "BOM" feature of Assembly4 and this is
used to generate the bill-of-materials and other things.

## Object naming conventions

Objects in the CAD files follow a strict naming convention.  This was adopted to keep the files
readable and help manage the complexity of the models.  The convention is that the prefix of the name
indicates what type of thing it is:
* P_ : Parts
* B_ : Bodies (within parts)
* S_ : Sketches
* PAD_ : Padding (extrusions) of sketches.
* POCKET_ : Pockets cut out with sketches.
* HOLE_ : Holes cut with standard profiles.
* PAT_ : Patterns duplicating objects (linear, polar, mirror, etc).

The next part of the name indicates the part it belongs to.  For example, the X Axis Top part is named 'P_X_Axis_Top' and the
corresponding body is called 'B_X_Axis_Top'.

The final part of the name indicates the specific feature inside the part (for example, holes, mount points, bearing slots, etc).

## File Naming Conventions

The files are also named with a particular convention 'jrobot-[subsystem]-[purpose].FCStd'.  For example,
the x-axis parts are called 'jrobot-x-axis-parts.FCStd' and the x-axis assembly (using the parts) is 'jrobot-x-axis-assembly.FCStd'
and similarly for other subsystems.

The 'purpose' should be one of these:
* -parts : Parts, individually manufacturable units.
* -assembly : Assembled parts to form a complete subsystem
* -print-orientations : Parts aligned to the correct print orientation and ready for STL export.

## Color/Material codes

TODO: Color code materials for:
* 3d printed parts : Burgandy
* Fasteners, bearings, etc. : Grey, Dark Gray
* PC Boards : Green
* Off the shelf components: Close to their actual color
* DuPont Connectors: Black

# Files

## jrobot-x-axis-parts.FCStd
This contains the x-axis parts including:
* X-axis Base (bolt mounted to substrate)
* X-axis Top (mounted on top of base)
* X-axis Motor Mount (mounted to top and is the mount point for the belt tensioner and motor)
* X-axis Tensioner (belt tensioner)
* X-axis Bearing Base

TODO
* Add 'part information' to all parts.
* Hide LCS axes from view.
* Export STL of each part

## jrobot-x-axis-print-orientations.FCStd
This contains the parts with their correct print orientations ready for export to STL for printing.

TODO:
* Create this and establish the pattern

## jrobot-x-axis-assembly.FCStd
This contains the assembly for the X axis showing how the parts fit together.

TODO:
* Finish with all of the fasteners

## jrobot-pcb-assembly.FCStd
This contains the assembly for the custom PCB used in the instruction manuals and the electronics assembly.

## jrobot-cnc-assembly.FCStd
This contains the assembly for the CNC boards mainly for generating the build guide and instruction videos.

## jrobot-electronics-parts.FCStd
This contains the electronics enclosure
* Add 'part information' to all parts.
* Electronics box base
* Electronics box lid

## jrobot-electronics-print-orientations
This contains the electronics parts laid out in their print orientations.

## jrobot-electronics-assembly
This is the animated assembly for the electronics enclosure with Arduino, bolts, and fans.

TODO:
* Output the BOM

## StandardParts-3-2.FCStd
This contains the 'standard' off the shelf parts needed for the assembly including:
* Standard ISO4762 metric bolts and nuts
* Belt sprockets and idlers
* Limit switch
* Cooling fan
* Bearings

TODO:
* Arduino Mega
* Arduino CNC Shield
* Arduino stepper drivers
* Add 'part information' to all parts.

# FreeCAD bugs to fix:
* Assemblies with other assemblies don't work because part loading isn't correct.  Sub-dependencies don't load their dependencies correctly and can break either the top level or sub-assemblies.
* Topology naming problem:  This can be fixed with an n^2 algorithm in terms of the number of features on the part.  Approach:
  ** Start with the list of features.  For each feature, iterate it and capture some "metrics" like "normal", "area", "length", etc.
  ** Recompute object
  ** Re-build this list of features.
  ** For each feature (in order of feature 'importance')
     *** Sort the "old" features by metrics that would give the "best match" to this feature.
     *** Take the best match for that feature and re-use the name.
     *** Remove this feature from the list for next iteration.
     *** If no 'old' features are left to match, assign a new name to this feature.
  ** Continue this process until all new features have names and hopefully the "important" features will not change names.
  ** To avoid this making models 'slow', only do this if there is a 'meaningful' change in the features (i.e. new features or 'major' changes which is probably O(1) detectable).

# Macros

There are a number of helper macros for managing the BOM and assembly animation exports.

* jrobot-write-bom.FCMacro : Macro to write BOM for a sub-assembly
* jrobot-export-assembly.FCMacro : Macro to write Assembly parts as .stl so they can be used in Blender animations.
* jrobot-export-print-orientations.FCMacro : Macro to write parts as .stl for 3d printing.


