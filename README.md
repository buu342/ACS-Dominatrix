# ACS-Dominatrix
A highly configurable domination gamemode replacement for Zandronum, ZDoom, and ZDaemon (coming soon).

This WAD requested by the MDF community.<br/><br/>

### How to use
  **1)** Include this WAD in your server's wad list.<br/>
  **2)** Write a script to spawn command posts onto the map. Example script:
```c
Script 1 OPEN
{
	SpawnForced("ControlPoint_Grey", 0.0, 0.0, 8.0);
	SpawnForced("ControlPoint_Blue", -416.0, -416.0, 8.0);
	SpawnForced("ControlPoint_Red", 416.0, -416.0, 8.0);
}
```
<br/><br/>

### Serverside configuration
```c
dominatrix_compatibility  = "Zandronum"; // "Zandronum", "ZDoom, or "ZDaemon"
dominatrix_timemax        = 300;         // How much time for a game to end in seconds? (0 for infinite time)
dominatrix_scoremax       = 250;         // How many points for the game to end? (0 for infinite score)

dominatrix_capspeed     = 1.0;   // How much health a control point loses per tick of capture
dominatrix_capdistance  = 256.0; // How far someone needs to be to capture the control point
dominatrix_capteamregen = false; // If the control point lost some health, can it be recovered by a team member?
dominatrix_capregentime = 0.0;   // How many seconds it takes for a control point to automatically regenerate 1 hp (0 for none)
dominatrix_capmultiple  = false; // Will a control point lose health faster if more people are capturing it?

dominatrix_scorefrag      = false; // Do you get points for fragging players?
dominatrix_scoreperfrag   = 1;     // How many points to you get for fragging players
dominatrix_scoreperfragcp = 1;     // How many points do you get per frag PER control point
dominatrix_scoretime      = 1.0;   // How many seconds for you to gain score for owning control points? (0.0 to not use time based scoring)
dominatrix_scorepercp     = 1;     // How many points per second do you get PER control point
```
<br/><br/>

### Clientside configuration
```c
dominatrix_announcer     = true; // Use the announcer voice
dominatrix_markers       = true; // Show markers on the control points
dominatrix_showallcps    = true; // Show all CP's below the timelimit
dominatrix_hudscale      = true; // Scale the HUD
dominatrix_hudwidescreen = true; // Use a widescreen HUD
```
<br/><br/>

### Changelog
**Version 1.0**
* Initial release
