Background Game Profile Switcher (BGPS)
By David Dahlstrom

Summary
=======
BGPS provides the ability to run game controller configuration software automatically in the background based on what game is being played in emulation, or manually by pressing buttons on a keyboard or game controller. The primary use case for this utility is to facilitate on-the-fly game profile switching when playing emulated MAME games in a VR arcade environment that does not offer the "run before" or "run after" capabilities of conventional front ends where this sort of thing is usually handled. 

Tested Software
===============
BGPS supports and has been tested successfully with the following software:

* Arcade Time Capsule (fantastic MAME-based VR arcade and main tested target client of BGPS)
* Virtual Controller  (software to create virtual XInput controllers)
* Ultimarc UltraMap   (software to modify behavior of Ultimarc's UltraStik 360 joysticks)
* RawAccel            (software to adjust the sensitivity of mouse/trackball controllers)

Command line templates for Virtual Controller and UltraMap are provided as default selections. You may, of course, modify these or add new ones for other software to suit your needs. 

Installation
============
To install BGPS, extract the distribution zip file to a folder on your Windows computer that has read/write access. The folder can be called whatever you want. 

When you run the executable (BGPS.exe), you will see a joystick icon in the Windows tray indicating normal background mode is active. Right clicking on this icon will show a menu of options. When running for the first time you will want to choose the "Settings..." option to configure the application.

Log
===
See the log.txt file in the \log subfolder if needed for troubleshooting. This log is overwritten at the start of every run. Two beeps will be sounded if an error is written to the file. When reporting any issues with BGPS, be sure to include the last log with your description of the problem. 

Configuration
=============
BGPS offers two different modes of operation. The first is a "ROM Monitor" mode that will execute actions whenever specified rom files are accessed. Since this mode provides full automation for game environments like ATC, there's a good chance that "ROM Monitor" mode may be the only mode you need. 

The second mode provides the option to trigger command line actions manually when a game controller button or keyboard key is pressed. Both "ROM Monitor" and keyboard/button actions can be added to the action list in any combination.

ROM Monitor:
------------
To setup a new rom to be monitored, choose "ROM Monitor" from the "Device List" list in the Settings screen, then ensure that the "ROM folder to monitor" field contains the name of the folder containing MAME rom files for your emulator. These must be in *.zip file format. Next, choose a rom from the "Choose ROM" list that you want to trigger an action and then use the "Profile name" and "Command line template" fields to configure the specific command line that should execute when that game is loaded. Finally, press the "Assign ROM" button to add the action to the "Action List". 

**Note** If you choose "[Default]" as the rom, the command line action you define will be executed whenever a rom that was NOT otherwise configured is accessed by the emulator. When you use this option, be aware that BGPS is "smart" enough to not execute the same command line twice in a row. For example, if you switch between two games that use the same profile (such as two default games, or two rotary joystick games that use the same profiles), profile loading will be suppressed for the second since that profile should already be loaded.

Buttons and Key Presses:
------------------------
To setup a manual action that will run upon a particular button or key press, Choose "Keyboard" or one of the game controllers from the Device List  in the Settings screen. Next, use the "Profile name" and "Command line template" fields to configure the command line that will execute when the button or key is pressed. Finally, press the "Assign" button to choose the actual button or key you want to assign to the action and add it to the Actions list.

Voice Annunciation
==================
If you would like BGPS to verbally annunciate an action when it is executed, you may add a phrase to the optional "Voice annunciation phrase" field. You can test the phrase to see what it will sound like by pressing the "Voice Test" button.

How to configure Profiles and Command Line Templates
====================================================
Profiles are files that define specific game controller configurations such as Ikari.vcd for Virtual Controller, or 4-way.ugc for UltraMap. To make command line creation easier, you may specify the profile separately in the "Profile name" field, and then choose a command line template in the "Command line template" field.  This template will typically contain one of the following field tags:

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

* Be aware that BGPS pauses active operation while the Settings screen is open, so be sure to close it when done with configuration.

Understanding the Action List Table
===================================
Each time you use the "Assign" button to create a new action, that action will be added to the Action List table. If you get a warning saying "Duplicate", BGPS will highlight the duplicate action in the list at which point you may keep it or delete it.

When you complete the table, press the "Save list" button to save it.  It will be saved in the \user folder as a *.bgp file having the name specified in the "Activity list name" field above the table. By default this name is "Arcade Controller" (saved as "Arcade Controller.bgp"). If you switch between multiple controllers for use with your emulator, you could save different action lists under different names. These can then be loaded in the future by creating a shortcut that provides the name as a command line parameter when launching BGPS.  For example,

BGPS.exe "Arcade Controller" or
BGPS.exe "Gamepad"

The Action list table contains the following columns:

Device List
-------------
The device or method that was chosen to trigger the action.

Action
------
* For the "ROM Monitor" Device List, this column shows the rom you chose to monitor.
* For the "Keyboard" Device List, it shows the keyboard key or key combo you assigned.
* For a game controller, it shows the button number you assigned.

Sequence
--------
For "Keyboard" and game controller actions, it is possible to assign multiple actions to the same key or button. The effect of this is that when you press that key or button the first time, the action with a sequence number of 1 will be triggered. When you press that same key or button a second time, the action with a sequence number of 2 will be triggered, and so forth (with each action being verbally annunciated if you provided an annunciation phrase with each). This provides a means to manually switch between multiple profiles using a single key or button. 

Sequence numbers are assigned to each action automatically when you add the action. To change the auto-assigned sequence of an action, just use the "Move Up" and "Move Down" buttons and you will see the sequence number for that action adjust according to its position in the list. Note that for "ROM Monitor" actions, the sequence number will always be 1 (since these are fully automated actions that have no need for sequencing).

Annunciation
------------
This is the annunciation phrase you assigned to the action.

Command Line
------------
This is the command line template with field tags replaced (i.e. the actual command line that will be executed).

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
This clears the entire table (if you press this by mistake, just close the screen without saving and re-open it).

Copy action
-----------
Copies fields from the selected row back into the editor fields to ease the creation of similar entries.

Delete action
-------------
Removes the selected row from the table.

Save actions
------------
Saves all actions in the table to the <action list name>.bgp file. 

User Preferences
================
These options allow the user to make a few adjustments to the operation of BGPS.

Operate only when this application is running
---------------------------------------------
This is a recommended setting for most use cases. To configure it, enter the name of the application executable you will be running BGPS with into this field and then check it. For example, if you are using BGPS with Time Capsule Arcade, you will enter "RetroVRArcade.exe" into this field (only enter the executable name, not the path). BGPS will use this information to keep itself paused while it is not actively needed.

Run RawAccel when the application starts
----------------------------------------
RawAccel is a utility that can be found on GitHub at https://github.com/RawAccelOfficial/rawaccel. This software may be needed to tune some trackballs to have additional sensitivity. For example, I need it to make my Ultimarc U-Trak trackball work correctly in Arcade Time Capsule. To integrate RawAccel with BGPS, simply install it to a subfolder of BGPS called ..\RawAccel.

This option is only available when the "Operate only when this application is running" setting is configured. When this option is turned on BGPS will automatically load RawAccel when the application runs, and will close RawAccel when the application closes. It is up to the user to configure RawAccel properly for their trackball before use. 

Always voice annunciate
-----------------------
If you have configured voice annunciation phrases to your actions, then this switch can control when these are heard. This checkbox has three states. When checked (the default), the voice will be heard every time a game in the action table is loaded (including default games). When unchecked, voice annunciation is effectively turned off. Finally, if the checkbox is configured with the minus sign (-), then voice annunciation will only occur if an actual profile switch is conducted (see the **Note** in the ROM Monitor section above).

Beep on profile change
----------------------
This option will sound a beep whenever a profile switch happens. This can be useful as a debugging tool by asserting profile changes independent of the voice option.

Show Tooltips
-------------
In addition to this documentation file, the Settings screen implements tooltips on all controls to explain their operation. If you no longer need the tooltips, you can turn them off by unchecking the "Show Tooltips" checkbox.







  


