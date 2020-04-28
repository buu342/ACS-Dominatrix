In this folder is a set of tools that you can use to help with modding Dominatrix.

### dominatrix_tool1.wad
A tool designed to allow you to place CP's ingame and to auto-generate the ACS code for the CP placement. Created by [Krawa](https://forums.zdaemon.org/profile.php?mode=viewprofile&u=45796).
```
Tool wad to generate code for Dominatrix.
- Pistol shot logs code with player coordinates for LOADACS.
- Coordinates are rounded to 16 pixels.
- An arrow will be placed to show the coordinates.
- First shot also prints map number as script number with leading 1,
  so map scripts should not be overridden. (map01 -> script 101)

Usage:
- Enable logfile for Single Player in ZLauncher.
  (e.g. Extra params: +logfile "%BASE%\%DATE%_%TIME%_patchinfo.txt")
- Shoot Pistol to get coordinates.
- Copy code from logfile and put to LOADACS.


Example for LOADACS library:
********************************************************************************
#library "DOM"
#include "zcommon.acs"

script "AddControlPoint_open" OPEN
{
 	ACS_Execute(GetLevelInfo(LEVELINFO_LEVELNUM) + 100, 0);
}

script 101 (void)
{
	// put generated code here
}
********************************************************************************

Changelog:
1: Initial version


2020-04-27 Krawa
```