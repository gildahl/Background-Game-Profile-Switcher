Background Game Profile Switcher (BGPS)
By David Dahlstrom

Summary
=======
BGPS provides the ability to switch game controller profiles automatically in the background based on what game is being played, or manually by pressing buttons on a keyboard or game controller. The primary use case for this utility is to more conveniently facilitate game profile switching when playing emulated MAME games in a VR environment using arcade controllers whose mappings and behaviors need to be customized beyond what can be achieved using in-game settings alone.

Tested Software
===============
BGPS has been tested successfully with the following software.

* Arcade Time Capsule (fantastic MAME-based VR arcade)
* Virtual Controller  (software to create virtual XInput controllers)
* Ultimarc UltraMap   (software to modify behavior of Ultimarc's UltraStik 360 joysticks)

Command line templates for Virtual Controller and UltraMap are pre-installed in BGPS with default paths. You may, of course, modify these to match the paths on your own machine, or add new ones for other software to suit your needs. 

Installation
============
To install BGPS, extract the distribution zip file to a folder on your Windows computer that has read/write access. When you run the executable (BGPS.exe), you will see a joystick icon in the Windows tray and normal background mode is active. Right clicking on this icon will show a menu of options. You will want to choose the "Settings..." option to configure the application.

Tooltips
========
In addition to this documentation file, the Settings screen implements tooltips on all controls to explain their operation. If you no longer need the tooltips, you can turn them off by unchecking the "Show Tooltips" checkbox.

Normal Operation
================
After BGPS has been configured (see next item), anytime you start the application it will be in its normal background operation mode. In this mode it will monitor your computer for any specified rom activity, keypresses, and or game controller button presses. When such an activity is detected, the appropriate configured profile loading command line will be executed.

It is recommended that one you are done with your gaming session, that you exit BGPS to avoid possible side-effects. However, it is also possible to deactivate keyboard and button triggers while BGPS is still running by right-clicking the tray icon and left-clicking on the "Active" option. Clicking on "Active" a second time will turn monitoring back on.

Configuration
=============
BGPS offers two different modes of operation. The first is a "ROM Monitor" mode that will execute a user defined command line action whenever rom files are loaded by MAME. The second mode provides the ability to trigger command line actions manually when a game controller button or keyboard key is pressed. These two modes can operate simultaneously. 

ROM Monitor:
------------
To setup a rom to be monitored, choose "ROM Monitor" from the device list in the Settings screen. Ensure that the "ROM folder to monitor" field contains the name of a valid folder containing MAME rom *.zip files. Next, choose the rom that you want to trigger an action from the "Choose ROM" list and use the "Profile name" and "Command line template" fields to configure the specific command line that should execute when that game is loaded. Finally, press the "Assign" button to add the action to the "Action List". 

**Note** If you choose "[Default]" as the rom, the command line action you define will be executed whenever a rom that was NOT configured is loaded by the emulator. Be aware, however, that BGPS is "smart" enough to not execute the same command line twice in a row. For example, if you switch between two games that use the same profile (such as two default games), profile loading will be suppressed for the second since that profile should already be loaded.

Buttons and Key Presses:
------------------------
To setup an action that will run upon a particular button or key press, Choose "Keyboard" or one of the game controller devices from the Device list in the Settings screen. Next, use the "Profile name" and "Command line template" fields to configure the command line that will execute when the button or key is pressed. Finally, press the "Assign" button to choose the button or key you want to assign to the action and add it to the Actions list.

Voice Annunciation
==================
If you would like BGPS to verbally annunciate an action when it is executed, you may add a phrase to the optional "Voice annunciation phrase" field. You can test the phrase to see what it will sound like by pressing the "Voice Test" button.

How to configure Profiles and Command Line Templates
====================================================
Profiles are files such as myprofile.vcd for Virtual Controller, or myprofile.ugc for UltraMap. To make command line creation easier, you may specify the profile separately in the "Profile name" field, and then choose a command line template in the "Command line template" field.  This template will typically contain one of the following tag fields:

[profile_name]        - will be replaced by the filename or contents of "Profile name" field
[profile_full_name]   - will be replaced by the full path/file or contents of "Profile name" field

For example, if the profile is "C:\Ultrastik\Profiles\qbert.ugc" and the command line template is "C:\UltraMap\UltraMap.exe [profile_name]", then upon pressing the "Assign" button, the command line that will be assigned to the action will be "C:\UltraMap\UltraMap.exe qbert.ugc". If the full path to the profile is needed, then the command line template should be changed to "C:\UltraMap\UltraMap.exe [profile_full_name]. If the command line template has no tags, then the command line will be used verbatim with no insertions. 

Additional Notes:
-----------------
* To test a command line while still in the Settings screen, press the "Test" button next to the Command Line Template field. Hovering over the "Test" button with the Show Tooltips option turned on, will show the actual command line that will be executed.

* If your profile filename needs quotes around it, then simply add quotes around the tag in the template, such as "[profile_name]" or "[profile_full_name]".
 
* If you wish to trigger two command lines in a single action, click on the checkbox next to "Profile name 2" and you can configure a second command line using a completely different profile and command line template. There will be a one second delay between the execution of the first and second action.

* If you want to add new templates to BGPS that will persist across sessions, you can edit any of the built-in ones and then use the Add button. You may also delete any templates you no longer want to see in the list.  Note that whenever you do this both the "Command line Template" and "Command Line Template 2" lists will be synchronized to contain the same list of templates.

* As an FYI, these templates are saved in a file called templates.json in the root BGPS folder. You may delete this file to restore the original shipping defaults.

Understanding the Action List Table
===================================
Each time you use the "Assign" button to create a new action, that action will be added to the Action List table. This table contains all of the actions which will become actively monitored once you save and exit the Settings screen, or when you initially load BGPS.

The Action list table contains the following columns:

Device
------
This is the device you chose from the Device list to create the action.

Action
------
* For the "ROM Monitor" device, this column shows the rom you chose.
* For the "Keyboard" device, it will show the keyboard key or key combo you pressed.
* For a game controller, it will show the button number you pressed.

Sequence
--------
For "Keyboard" and game controller actions, it is possible to assign multiple actions to the same key or button. The effect of this is that when you press that key or button the first time, the action with a sequence number of 1 will be triggered. When you press that same key or button a second time, the action with a sequence number of 2 will be triggered, and so forth (with each action being verbally annunciated if you provided an annunciation phrase with each). This provides a means to manually switch between multiple profiles using a single key or button. 

Sequence numbers are assigned to each action automatically when you add the action. To change the auto-assigned sequence of an action, just use the "Move Up" and "Move Down" buttons and you will see the sequence number for that action adjust according to its position in the list. Note that for "ROM Monitor" actions, the sequence number will always be 1 (since these are fully automated actions).

Annunciation
------------
This is the annunciation phrase you assigned to the action.

Profile
-------
This is the name of the profile you specified.

Command Line
------------
This is the command line template with tags replaced (i.e. the actual command line that will be executed).

Profile 2
---------
This is the name of any second (optional) profile that you specified.

Command Line 2
--------------
This is the second command line template with tags replaced (i.e. the actual command line that will be executed).


Managing the Action table
=========================
Below the Action List table are several additional buttons with the following functions:

Move Up / Move Down
-------------------
These buttons are intended for use in changing the sequence order of actions assigned to a single button or key press as described above under "Sequence".

Clear All
---------
This clears the entire table.

Edit Action
-----------
Copies fields from the selected row back into the editor fields.

Delete Action
-------------
Removes the selected row from the table.

Save
----
Save all actions in the table to the bgps.json file. This is the configuration file that will be used in normal background operation mode once the Settings screen is closed, or when BGPS is started the next time. 

License
=======
This software is distributed freely on GitHub for hobbyist users, and may be used and modified freely for personal, non-commercial use. It may not be sold or packaged with any other product or software without permission.





  


