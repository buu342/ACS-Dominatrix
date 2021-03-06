![](https://i.imgur.com/kxijgwR.gif)![](https://i.imgur.com/mancHEJ.png)
---
A highly configurable domination gamemode replacement for Zandronum, ZDaemon, and (G)ZDoom.

This WAD requested by the MDF community.<br/><br/>

### How to place control points on pre-existing maps (AKA make an injection WAD)
  **1)** Write a script to spawn command posts onto the map. Use the format `ACS_NamedExecuteAlways("Dominatrix_AddControlPoint", 0, x, y, z);`, where `x, y, z` are the **FIXED POINT** coordinates to place the command post. Example script:
```c
Script 1 OPEN
{
    ACS_NamedExecuteAlways("Dominatrix_AddControlPoint", 0, 0.0, 0.0, 8.0);
    ACS_NamedExecuteAlways("Dominatrix_AddControlPointBlue", 0, -416.0, -416.0, 8.0);
    ACS_NamedExecuteAlways("Dominatrix_AddControlPointRed", 0, 416.0, -416.0, 8.0);
}
```
  **2)** Put `#library "NAME"` at the top of the ACS script, where NAME is a unique name **less than or equal to 8 characters**<br/>
  **3)** Compile the ACS, placing it between A_START and A_END lumps. Ensure it is the same name as NAME in your library.<br/>
  **4)** Create a new lump called LOADACS, and inside write the name of the compiled ACS file (should be NAME of your library).<br/>
  **5)** Be sure to include the WAD that executes that script along with the server's files.<br/>
Examples are provided in the "Injection WADs" folder within this repository.<br/>
If you prefer, you can use [ZDaemon's Patchinfo method](http://master.zdaemon.org/patchinfo.txt), however this will result in your injection WAD only being compatible in ZDaemon, which defeats the purpose of the multi-sourceport compatibility.<br/><br/>
  
### How to place control points on your custom maps
You can either use the method outlined above OR place the control point entities directly on the map. The following actors are available:
```c
ControlPoint_Grey 10000 (SpawnID 213)
ControlPoint_Blue 10001 (SpawnID 214)
ControlPoint_Red  10002 (SpawnID 215)
```
<br/>

### How to use on a server
  **1)** Include the latest version of the Dominatrix WAD in your server's wad list, as well as the map pack you want to use and the injection script to place CP's in said map pack.<br/>
  **2)** Ensure the server is running "Team Deathmatch" as the selected gamemode.<br/>
  **3)** Ensure the default gamemode's score limit and time limit are both set to 0 to prevent conflicts with Dominatrix. I would also recommend disabling the announcer as this gamemode comes with its own. <br/>
  **4)** If using ZDaemon, include Dominatrix.cfg (or call it in the console via `exec dominatrix.cfg`) in your server so that all Dominatrix related CVars are set. Also, be aware that in ZDaemon, CVars need to have 1/0 as opposed to true/false, and that you **cannot** use decimal numbers!  
<br/><br/>

### How to compile the Dominatrix ACS source
  **1)** Go to your Zandronum ACC folder (For instance, in Doom Builder\Compilers\Zandronum).<br/>
  **2)** Place [zdaemon.acs](http://downloads.zdaemon.org/zdaemon.acs) in that folder.<br/>
  **3)** Edit acc.cfg in the same folder and add `zdaemon = "zdaemon.acs";` to the `zdoom_acc {...}` section.<br/>
  **4)** Modify zspecial.acs to include `-130:SetDeadSpectator(2),` and `-131:SetActivatorToPlayer(1),`<br/>
  **5)** Compile, and place the binary between the A_START and A_END lumps, ensuring the lump itself is called DOMNATRX.
<br/><br/>

### Serverside configuration
```c
dominatrix_compatibility = "Zandronum"; // "Zandronum", "ZDoom, or "ZDaemon"
dominatrix_timemax       = 300;         // How much time for a game to end in seconds? (0 for infinite time)
dominatrix_scoremax      = 250;         // How many points for the game to end? (0 for infinite score)
dominatrix_roundendtime  = 3;           // How many seconds does the game display the winner for?	

dominatrix_caphealth    = 100;   // The maximum health of a control point.
dominatrix_capdistance  = 256;   // How far someone needs to be to capture the control point
dominatrix_capteamregen = false; // If the control point lost some health, can it be recovered by a team member?
dominatrix_capregentime = 0.0;   // How many seconds it takes for a control point to automatically regenerate 1 hp (0 for none)
dominatrix_capmultiple  = false; // Will a control point lose health faster if more people are capturing it?
dominatrix_capbelow     = true;  // Allow capturing if the player is below the control point?
dominatrix_capabove     = true;  // Allow capturing if the player is above the control point?

dominatrix_scorefrag      = false; // Do you get points for fragging players?
dominatrix_scoreperfrag   = 1;     // How many points to you get for fragging players
dominatrix_scoreperfragcp = 1;     // How many points do you get per frag PER control point
dominatrix_scoretime      = 1.0;   // How many seconds for you to gain score for owning control points? (0.0 to not use time based scoring)
dominatrix_scorepercp     = 1;     // How many points per second do you get PER control point

dominatrix_scorelimitpercp     = 0; // Increase the max score by this number multiplied by the number of CPs.
dominatrix_scorelimitperplayer = 0; // Increase the max score by this number multiplied by the number of players.
dominatrix_timelimitpercp      = 0; // Increase the max time by this number multiplied by the number of CPs.
dominatrix_timelimitperplayer  = 0; // Increase the max time by this number multiplied by the number of players.

dominatrix_ddommode         = false; // Use Double Domination mode?
dominatrix_ddomscoretime    = 10;    // How much time do teams need to hold the CP's to score in Double Domination?
dominatrix_ddomresetonscore = true;  // Do all control points reset back to grey when a team scores?

dominatrix_cpsolid       = true;  // Make the Control Points solid
dominatrix_cptranslucent = false; // Make the Control Points slightly translucent

```
<br/>


### Clientside configuration
```c
dominatrix_disableannouncer     = false; // (Don't) Use the announcer?
dominatrix_disablemarkers       = false; // (Don't) Show markers on the CP's?
dominatrix_disableshowallcps    = false; // (Don't) Show all the CP's on the top of the screen?
dominatrix_disablehudscale      = false; // (Don't) Scale the HUD to 640x480?
dominatrix_disablehudwidescreen = false; // (Don't) Use a 16:9 ratio on the HUD?
dominatrix_enablelog            = false; // Log announcements (in text) to the message area?
dominatrix_enablecenterprint    = false; // Show announcements (in text) in the center of the screen?
```
<br/>

### Credits
Credits are provided within the WAD as a special lump.
<br/><br/>

### Changelog
**Version 1.33**
* +[Added dominatrix_capabove CVar](https://github.com/buu342/ACS-Dominatrix/issues/32)
* +[Added CVars to make the CP Solid or translucent](https://github.com/buu342/ACS-Dominatrix/issues/34)
* \*[Fixed how sometimes the capture HUD would show when below a CP](https://github.com/buu342/ACS-Dominatrix/issues/33)
* \*Reduced HUDMessage sending to improve network usage in ZDaemon

**Version 1.3**
* +[Added 2 Clientside console commands to print announcements to the screen in text](https://github.com/buu342/ACS-Dominatrix/issues/30)
* \*[Changed player TID's to start at 1000 instead of 1337](https://github.com/buu342/ACS-Dominatrix/issues/31)
* \*[Made some changes for (G)ZDoom Compatibility](https://github.com/buu342/ACS-Dominatrix/issues/27)
* \*Announcer now takes into account the values of the scorelimitper### CVar(s)
* \*Fixed an issue with announcements repeating themselves or not playing at all
* \*Fixed an issue with the HUD disappearing in Zandronum

**Version 1.2**
* +[Added proper ZDaemon support](https://github.com/buu342/ACS-Dominatrix/issues/1)
* +[Added a Double Domination variant](https://github.com/buu342/ACS-Dominatrix/issues/18)
* +[Made a custom HUD for spectators (Only working in Zandronum)](https://github.com/buu342/ACS-Dominatrix/issues/15)
* +[Implemented an announcement stack](https://github.com/buu342/ACS-Dominatrix/issues/3)
* +[Added a CVar to prevent players from capping a CP from below](https://github.com/buu342/ACS-Dominatrix/issues/28)
* \*[Changed blue team's score to be lighter to improve readability](https://github.com/buu342/ACS-Dominatrix/issues/20)
* \*[Reduced traffic usage by only networking time once](https://github.com/buu342/ACS-Dominatrix/issues/19)
* \*[Reduced traffic usage by separating CP coordinates from __clientsync_cpinfo](https://github.com/buu342/ACS-Dominatrix/issues/21)
* \*[Made a new, custom announcer (Thanks a lot RottKing!)](https://github.com/buu342/ACS-Dominatrix/issues/9)
* \*[Fixed SBARINFO jitter by changing it to ACS](https://github.com/buu342/ACS-Dominatrix/issues/2)
* \*[Made it so that the "official" score gets set at the end of the game](https://github.com/buu342/ACS-Dominatrix/issues/22)
* \*Negated all clientside CVar's by default, in order to allow for ZDaemon compatibility. 

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
