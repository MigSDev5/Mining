Mining 1.2 
credits : Vindomire

Link original post:
 https://epochmod.com/forum/topic/15055-release-mining-12-updated-08062014/

What this does:

If you have a Toolbox and a Sledge, you go to where the nodes are and if your 15m from the activiation object you get a start mining option. The script will then loop on a 10 second timer collecting iron ore, silver ore, gold ore, and rarely gems. Since my server uses gems as a higher currency this would be the draw to these sites. It will loop until your inventory is full then you start it all over again.
 
Installation:
 
1) place the mining folder into your mission pbo/custom directory
 
2) Add to init.sqf:     [] execVM 'custom\mining\init.sqf';﻿     //Added for Mining in the if (!isDedicated) then { section
 
3) OPTIONAL to add map markers
    Add to class markers in mission.sqm and replace # with proper incremented number and increase the items=# by 2:

		class Item#
		{
			position[]={ 3893.9448, 0, 11426.449};
                        name="Mine1";
                        text="Mining Node";
                        type="mil_dot";
                        colorName="ColorBlack";
		};
		class Item#
		{
			position[]={ 13273.093, 0, 6099.0747};
                        name="Mine2";
                        text="Mining Node";
                        type="mil_dot";
                        colorName="ColorBlack";
		};
4) Place mining.sqf  in whatever folder you put your custom map additions in the server pbo
 
5) add to the end of init\server_functions in server pbo:

	//Mining Nodes
	[] execVM "z\addons\dayz_server\<CUSTOM FOLDER NAME>\mining.sqf";﻿
6) to stop undefined variable errors in the RPT add to your custom variables.sqf inside dayz_resetSelfActions = {:

	s_player_mining = -1;</br>
	s_player_mine = -1;</br>
DONE!
 
From that point you should just have to go to the giant rock tower and mine. The rock tower is just for looks since i didnt want people to be able to mine at them all i put an object(BeltBuckle_DZE) in the middle to trigger the start mining scroll option. So to add more just put the belt buckle somewhere and drop a rock tower over top of it.
 
This is the first script i have made for release so hopefully the install instructions are good. :)
 
Version 1.1 Uploaded 08/04/2014 (download and replace your mining\init.sqf and mining\start.sqf):

New requirement to have sledgehammer as primary weapon
animation changed to swinging animation
Moving cancels mining as well as the stop mining option (now properly removes the stop mining option and readds start mining)
Notification when you enter mining range with instructions on how to mine added
inventory max changed to 20 (hopefully it is more accurate)
ore percentages changed and where gems are calculated moved. Less gems then before but more consistant numbers.
small code optimizations
Version 1.2 Uploaded 08/06/2014 (download and replace your mining\init.sqf and mining\start.sqf):

Proper inventory full check, no more overflow
Various notification handling changes
Ability to get the start mining with a sledge in inventory but you are told it must be equipped to mine
Check to make sure the sledge is the current weapon selected
check to make sure your looking at the rockwall. Cancels mining if you look away
closes inventory if opened
minor little formatting and undefined variable fixes
*** Special Thanks to hogscraper for the animation change, sledge as primary(including fix), movement cancellation, proper inventory handling, close inventory and change to the notification handling.

Known Issue (removed for all new downloads):

Sometimes it wont let you mine when looking at the rock (works for me on my server after about 3 mining tries then isnt a problem everr again). To disable the rockwall cursor check delete from start.init:

if (!(_cursorTarget isKindOf "MAP_R2_RockTower")) exitWith {
isMining = false;
systemChat("Must look at what your Mining.");
};
 
