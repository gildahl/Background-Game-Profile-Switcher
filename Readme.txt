Background Game Profile Switcher (BGPS)
By David Dahlstrom

Summary
=======
BGPS provides the ability to run game controller configuration software automatically in the background based on what game is being played by a MAME emulator, or manually by pressing buttons on a keyboard or game controller. The primary use case for this utility is to better facilitate on-the-fly game profile switching or virtual game controller creation when playing emulated MAME games in a VR arcade environment that does not offer the "run before" or "run after" capabilities of conventional front ends where this sort of thing is usually handled. 

Tested Software
===============
BGPS has been tested successfully with the following software:

* Arcade Time Capsule (fantastic MAME-based VR arcade and main tested target client of BGPS)
* Virtual Controller  (software to create virtual XInput controllers)
* Ultimarc UltraMap   (software to modify behavior of Ultimarc's UltraStik 360 joysticks)

Command line templates for Virtual Controller and UltraMap are provided as default selections. You may, of course, modify these or add new ones for other software to suit your needs. 

Installation
============
To install BGPS, extract the distribution zip file to a folder on your Windows computer that has read/write access. The folder can be called whatever you want. When you run the executable (BGPS.exe), you will see a joystick icon in the Windows tray indicating normal background mode is active. Right clicking on this icon will show a menu of options. When running for the first time you will want to choose the "Settings..." option to configure the application.

User Preferences: Tooltips
==========================
In addition to this documentation file, the Settings screen implements tooltips on all controls to explain their operation. If you no longer need the tooltips, you can turn them off by unchecking the "Show Tooltips" checkbox.

User Preferences: Operate only when this application is running
===============================================================
It is recommended to enter the name of the executable that you will be running BGPS in the field called, "Operate only when this application is running". For example, if you are using BGPS with Time Capsule Arcade, you would enter RetroVRArcade.exe in this field (only enter the executable name, not the path). This is to avoid possible side effects caused by BGPS trying to monitor for rom file access when the target application is not running.

Configuration
=============
BGPS offers two different modes of operation. The first is a "ROM Monitor" mode that will execute user defined command line actions whenever rom files are loaded by MAME. Since this mode provides full automation, there's a good chance that "ROM Monitor" mode is the only mode you will ever need. 

The second mode provides the option to trigger command line actions manually when a game controller button or keyboard key is pressed. Both "ROM Monitor" and keyboard/button mode can be active simultaneously.

ROM Monitor:
------------
To setup a rom to be monitored, choose "ROM Monitor" from the "Device List" list in the Settings screen. Ensure that the "ROM folder to monitor" field contains the name of the folder containing MAME rom files for your emulator. These must be in *.zip file format. Next, choose a rom from the "Choose ROM" list that you want to trigger an action and use the "Profile name" and "Command line template" fields to configure the specific command line that should execute when that game is loaded. Finally, press the "Assign" button to add the action to the "Action List". 

**Note** If you choose "[Default]" as the rom, the command line action you define will be executed whenever a rom that was NOT configured is loaded by the emulator. When you use this option, be aware that BGPS is "smart" enough to not execute the same command line twice in a row. For example, if you switch between two games that use the same profile (such as two default games), profile loading will be suppressed for the second since that profile should already be loaded.

Buttons and Key Presses:
------------------------
To setup an action that will run upon a particular button or key press, Choose "Keyboard" or one of the game controllers from the Device List  in the Settings screen. Next, use the "Profile name" and "Command line template" fields to configure the command line that will execute when the button or key is pressed. Finally, press the "Assign" button to choose the actual button or key you want to assign to the action and add it to the Actions list.

Voice Annunciation
==================
If you would like BGPS to verbally annunciate an action when it is executed, you may add a phrase to the optional "Voice annunciation phrase" field. You can test the phrase to see what it will sound like by pressing the "Voice Test" button.

How to configure Profiles and Command Line Templates
====================================================
Profiles are files such as MyProfile.vcd for Virtual Controller, or MyProfile.ugc for UltraMap. To make command line creation easier, you may specify the profile separately in the "Profile name" field, and then choose a command line template in the "Command line template" field.  This template will typically contain one of the following field tags:

[profile_name]        - will be replaced by the filename or contents of "Profile name" field
[profile_full_name]   - will be replaced by the full path/file or contents of "Profile name" field

For example, if the profile is "C:\Ultrastik\Profiles\qbert.ugc" and the command line template is "C:\UltraMap\UltraMap.exe [profile_name]", then upon pressing the "Assign" button, the command line that will be assigned to the action will be "C:\UltraMap\UltraMap.exe qbert.ugc". If the full path to the profile is needed, then the command line template should be changed to "C:\UltraMap\UltraMap.exe [profile_full_name]. If the command line template has no field tags, then the command line will be used verbatim with no insertions. 

Additional Notes:
-----------------
* To test a command line while still in the Settings screen, press the "Test" button next to the Command Line Template field. Hovering over the "Test" button with the Show Tooltips option turned on, will show the actual command line that will be executed.

* If your profile filename needs quotes around it, then simply add quotes around the field tag in the template, such as "[profile_name]" or "[profile_full_name]".
 
* If you wish to trigger two command lines in a single action, click on the checkbox next to "Profile name 2" and you can configure a second command line using a completely different profile and command line template. There will be a one second delay between the execution of the first and second action.

* If you want to add a new template to BGPS that will persist across sessions, you can edit any of the built-in ones and then use the Add button. You may also delete any template you no longer want to see in the list.  Note that whenever you do this both the "Command line Template" and "Command Line Template 2" lists will be synchronized to contain the same list of templates.

* As an FYI, these templates are saved in a file called templates.json in the root BGPS folder. You may delete this file to restore the original shipping defaults.

Understanding the Action List Table
===================================
Each time you use the "Assign" button to create a new action, that action will be added to the Action List table. This table contains all of the actions which will become the active set once you save and close the Settings screen.

The Action list table contains the following columns:

Device List
-------------
Choose the device or method that will trigger the action.

Action
------
* For the "ROM Monitor" Device List, this column shows the rom you chose to monitor.
* For the "Keyboard" Device List, it will show the keyboard key or key combo you assigned.
* For a game controller, it will show the button number you assigned.

Sequence
--------
For "Keyboard" and game controller actions, it is possible to assign multiple actions to the same key or button. The effect of this is that when you press that key or button the first time, the action with a sequence number of 1 will be triggered. When you press that same key or button a second time, the action with a sequence number of 2 will be triggered, and so forth (with each action being verbally annunciated if you provided an annunciation phrase with each). This provides a means to manually switch between multiple profiles using a single key or button. 

Sequence numbers are assigned to each action automatically when you add the action. To change the auto-assigned sequence of an action, just use the "Move Up" and "Move Down" buttons and you will see the sequence number for that action adjust according to its position in the list. Note that for "ROM Monitor" actions, the sequence number will always be 1 (since these are fully automated actions that have no need for sequencing).

Annunciation
------------
This is the annunciation phrase you assigned to the action.

Profile
-------
This is the name of the profile you specified.

Command Line
------------
This is the command line template with field tags replaced (i.e. the actual command line that will be executed).

Profile 2
---------
This is the name of any second (optional) profile that you specified.

Command Line 2
--------------
This is the second command line template with field tags replaced (i.e. the actual command line that will be executed).


Managing the Action List table
==============================
Below the Action List table are several additional buttons with the following functions:

Move Up / Move Down
-------------------
These buttons are intended for use in changing the sequence order of actions assigned to a single button or key press as described above under "Sequence".

Clear all
---------
This clears the entire table.

Edit action
-----------
Copies fields from the selected row back into the editor fields.

Delete action
-------------
Removes the selected row from the table.

Save actions
------------
Save all actions in the table to the bgps.json file. This is the configuration file that will then be used in normal background operation mode once the Settings screen is closed. 

License
=======
This software is distributed freely on GitHub for hobbyist users, and may be used and modified freely for personal, non-commercial use. It may not be sold or distributed with any other product or software without permission. Some included source code files by myself or third parties may provide more permissive or public domain licenses. See the individual source code files for details.





  


