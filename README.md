![](https://i.imgur.com/kxijgwR.gif)![](https://i.imgur.com/mancHEJ.png)
---
A highly configurable domination gamemode replacement for Zandronum, ZDoom, and ZDaemon. ZDaemon compatiblity is not yet finished, as the DECORATE assets need to be converted to DeHackEd.

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
  **3)** Ensure the server is running "Team Deathmatch" as the selected gamemode. <br/>
  **4)** Ensure the score limit and time limit is both set to 0 to prevent conflicts with Dominatrix. I would also recommend disabling the announcer as this gamemode comes with its own. 
<br/><br/>

### How to compile the ACS
  **1)** Go to your Zandronum ACC folder (For instance, in Doom Builder\Compilers\Zandronum).<br/>
  **2)** Place [zdaemon.acs](http://downloads.zdaemon.org/zdaemon.acs) in that folder.<br/>
  **3)** Edit acc.cfg in the same folder and add `zdaemon = "zdaemon.acs";` to the `zdoom_acc {...}` section.<br/>
  **4)** Compile, and place the binary between the A_START and A_END lumps, ensuring the lump itself is called DOMNATRX.
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

dominatrix_scorelimitpercp     = 0; // Increase the max score by this number multiplied by the number of CPs.
dominatrix_scorelimitperplayer = 0; // Increase the max score by this number multiplied by the number of players.
dominatrix_timelimitpercp      = 0; // Increase the max time by this number multiplied by the number of CPs.
dominatrix_timelimitperplayer  = 0; // Increase the max time by this number multiplied by the number of players.
```
<br/>


### Clientside configuration
```c
dominatrix_announcer     = true; // Use the announcer voice
dominatrix_markers       = true; // Show markers on the control points
dominatrix_showallcps    = true; // Show all CP's below the timelimit
dominatrix_hudscale      = true; // Scale the HUD
dominatrix_hudwidescreen = true; // Use a widescreen HUD
```
<br/>


### Changelog
**Version 1.1**
* +[Game now shows why it ended](https://github.com/buu342/ACS-Dominatrix/issues/14)
* +[Created a credits lump](https://github.com/buu342/ACS-Dominatrix/issues/6)
* +[Added a CVar for game freeze time duration when the round ends](https://github.com/buu342/ACS-Dominatrix/issues/5)
* +[Added CVars for dynamic score/time](https://github.com/buu342/ACS-Dominatrix/issues/10)
* \*[Fixed an issue regarding team health regen](https://github.com/buu342/ACS-Dominatrix/issues/13)
* \*[Fixed an issue in the HUD shoiwng health regen incorrectly](https://github.com/buu342/ACS-Dominatrix/issues/12)
* \*[Made some networking opimizations by making CP XYZ values static](https://github.com/buu342/ACS-Dominatrix/issues/11)
* \*[Made it so CP's can take a new line in player HUDs](https://github.com/buu342/ACS-Dominatrix/issues/8)
* \*[Moved the timer to show below the CP's](https://github.com/buu342/ACS-Dominatrix/issues/7)
* \*[Made it so CP's cant be modified when a game ends](https://github.com/buu342/ACS-Dominatrix/issues/4)

**Version 1.0**
* Initial release
