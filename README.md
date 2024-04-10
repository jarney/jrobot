# JRobot Introduction


This project aims to make available a high quality, low cost robot arm for the home hobbyist.

## Quality
* Repeatable: gear mechanisms with small backlash and repeatable moves.
* Safe: Limit switches all around to ensure within tolerances.
* Callibration: Custom callibration cycle similar to Prusa mesh leveling procedure to ensure repeatable moves and measured tolerances.
* Feedback: Closed-loop encoders where possible (but not required)
* Reliable: Be aware of vibration-sensitive connections and try to reduce the vibrarion or otherwise prevent loosening during operation.

## [Getting parts](bill-of-materials/README.md)

There is a bill of materials for the build.  The parts are a combination of commonly available bolts, bearings, motors, and switches as well as 
3d-printed and other custom parts.

## [Build Guide](build-guide/README.md)
The assembly can be done using the build instructions.  The instructions include written instructions as well as
a number of videos showing the assembly.

## [CAD](freecad/README.md)

The CAD is done using FreeCad.  There is a guide to the [CAD files](FreeCAD/README.md) if you would like to modify the design.

## [3d Printing of parts](3d-printing/README.md)

Some of the parts are 3d-printed.  The STL files are available with a printing guide.

## Design Goals:

This section describes some of the design goals of the project.  This is mainly to keep the team honest
when making design choices and specifically to differentiate from other similar robot arm projects
which have slightly different design goals.

### Inexpensive:

In order to keep the project inexpensive, it is important for the off-the-shelf components
used be commonly available and inexpensive.  In addition, many of the off-the-shelf components
are less expensive per unit when purchased in bulk.  For example, ISO M3 screws are less expensive
in a box of 100 than they are for individual purchase of screws.  From a design perspective, this means
that it is more desirable to have a small variety of fasteners to increase the likihood that they can be
aquired in bulk.

It should also go without saying that less is more.  Reducing the number of bearings and variety
of 'uncommon' or 'large' bearings is important because bearings and other precision parts can sometimes
be expensive.  Also, substituting 3d-printed bearings in some places may be a more accessible option,
especially when the tolerance or wear characteristics of the bearings are not critical.

### Reliability

Continuous operation should be possible for hundreds of hours without a breakdown.  Experience with similar
projects indicates that the two major areas where this can be problematic from a design perspective
are the wiring and vibration.

For wiring, the most common area is cable fatigue from repeated movement.  Good cable management
and isolating the areas of cable motion are critical for improving the reliability.  The design
should ensure that moving cables be kept to a short length and well protected from abrasion.

For vibration, the most common issue is fasteners loosening with nuts falling off.  Wherever possible,
it should be ensured that fasteners can be tightened strongly and where possible, caps added to prevent
nuts from rotating under vibration.  Radial loads on fasteners should also be avoided and
instead, axial loads preferred because this prevents the fasteners from experiencing loads that are
likely to loosen them.

### Fast construction

It is also a design goal to ensure that the project is easy to assemble.  Specificlaly,
special-purpose tools and tight squeezes for inserting fasteners should be avoided.

The only equipment required should be restricted to things commonly available in a home shop.
* 3d Printer (for producing the special-purpose parts).
* Metric hex wrenches
* Soldering iron and crimp tool for building electrical systems.

It may be desirable, if the popularity of the project grows, to custom-build a 
PCB for system control in order to prevent the need to custom solder a breakout board
for the arduino.

### Open-source

The last design goal is for the entire project from CAD to construction be open-source.
This means using tools and techniques that are accessible and open-source with a permissive
license allowing modification at all levels of the project.


