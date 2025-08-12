arcadeVFE for ATC
A Virtual Front End for Arcade Time Capsule
By David Dahlstrom

Summary
=======
Virtual Reality arcades based on MAME, such as ATC, don't need traditional front ends since the player walks the floors of the virtual arcade, choosing games just as in a real arcade. So there's no need for game selection menus, pictures and videos of machines and screens, or background ambiance sounds since all of that is already right in front of you. However, there are still a few key technical benefits, ancillary to game selection, that I felt could be addressed through the use of a specialized front-end designed specifically for the virtual reality arcade.

The most important of these is to provide the "run before" function of most traditional front ends, allowing players to run external game controller configuration software for game-specific customization of controllers. This is to permit programmable joysticks and servo sticks to alter their configuration based on the specific game being played; or to do on-the-fly remapping of buttons for say, creating more comfortable layouts or left vs. right hand operation; or for combining game controllers into a single integrated control panel through the use of command-line driven software like "Virtual Controller" that enables multiple input devices to be combined and recognized as single XInput device, a necessity for ATC (see link to the "ATC Monster Control Panel Guide" link below).

Thus, a complete list of arcadeVFE's *current* feature set includes:

* Automatic execution of custom command-line driven software whenever a new game is started. 
* Manual execution of custom command-line driven software whenever a particular keyboard key or game controller button is pressed.
* Customizable voice annunciation of controller layouts when they are loaded if desired or deemed helpful.
* Mapping of keyboard keys such as Tab and Enter to controller buttons to (for example) better facilitate access to the MAME Tab configuration menus.
* And for data nerds like me, a highly detailed game information overlay on the desktop that can be viewed and navigated in VR using one's favorite desktop viewport. This information comes from integrating traditional MAME gameinfo.dat and history.xml files, and can also include pictures of your choice--for example, flyers, pcbs, or pictures of real cab control panels (which can be very handy as a reference in the Candy Cab rooms of ATC).

Resources
=========
GitHub:  https://github.com/gildahl/Background-Game-Profile-Switcher
Discord: https://discord.gg/yQ7THG6d2u
ATC Monster Control Panel Guide:   https://docs.google.com/document/d/1_UpA_Fa-1jQdQMLDDSFTut15gjGnhjljFkd_raw9Ox4/edit?tab=t.0

Tested Software
===============
arcadeVFE has been tested successfully with the following software:

* Arcade Time Capsule (fantastic MAME-based VR arcade and main tested target of arcadeVFE)
* Virtual Controller  (software to create virtual XInput controllers)
* Ultimarc UltraMap   (software to modify behavior of Ultimarc's UltraStik 360 joysticks)
* Ultimarc JoyTray    (software to control ServoStik sticks, including U360 with ServoStik upgrade)
* RawAccel            (software to adjust sensitivity of mouse/trackball controllers)

Installation
============
To install arcadeVFE, extract the distribution zip file to an empty folder on your Windows computer that has read/write access. The folder can be called whatever you want. Importantly, after installation, right-click on each *.dll and *.exe file, choose Properties, check the "Unblock" checkbox at the bottom and click apply.

When you first run the executable (vfe.exe), it will create a few subfolders and extract some additional files into them. You will then see a joystick icon in the Windows tray indicating normal background mode is active. Right clicking on this icon will show a menu of options. When running for the first time you will want to choose the "Settings..." option to configure the application.

Log
===
See the log.txt file in the \log subfolder if needed for troubleshooting. This log is overwritten at the start of every run. Two beeps will be sounded if an error is written to the file. When reporting any issues with arcadeVFE, be sure to include the last log with your description of the problem. You may report errors on the Discord.

Configuration
=============
arcadeVFE offers two different modes of operation. The first is a "ROM Monitor" mode that can execute game-specific actions whenever a MAME rom file is accessed. This mode provides full automated game controller configuration in MAME emulation environments like ATC. 

The second mode provides the option to trigger actions manually when a game controller button or keyboard key is pressed. Both "ROM Monitor" and keyboard/button actions can be added to the action list in any combination and are supported simultaneously with ROM Monitor mode.

ROM Monitor:
------------
To setup a new rom to be monitored, choose "ROM Monitor" from the "Device List" list in the Settings screen, then ensure that the "ROM folder to monitor" field contains the name of the folder containing MAME rom files for your emulator. These must be in *.zip file format. Next, choose a rom from the "Choose ROM" list that you want to trigger an action and use the "Profile name" and "Command line template" fields to configure the specific command line that should execute when that game is loaded. Finally, press the "Assign ROM" button to add the action to the "Action List". 

**Note** If you choose "[Default]" as the rom, the command line action you define will be executed whenever a rom that was NOT otherwise configured is accessed by the emulator. When you use this option, be aware that arcadeVFE is "smart" enough to not execute the same command lines twice in a row. For example, if you switch between two games that use the same profile (such as two default games, or two rotary joystick games that use the same profiles), or exit a game and then restart it, profile loading will be suppressed since that configuration should still be loaded.

Buttons and Key Presses:
------------------------
To setup a manual action that will run upon a particular button or key press, Choose "Keyboard" or one of the game controllers from the Device List in the Settings screen. Next, use the "Profile name" and "Command line template" fields to configure the command line that will execute when the button or key is pressed. Finally, press the "Assign" button to choose the actual button or key you want to assign to the action and add it to the Actions list.

**Note** In addition to command line actions, game controller buttons can also be configured to act send virtual keyboard key presses or perform game information screen navigation actions. These options can be configured by choosing the appropriate radio button at the top of the screen whenever a game controller is selected in the "Devices" list.

Voice Annunciation
==================
If you would like arcadeVFE to verbally annunciate an action when it is executed, you may add a phrase to the optional "Voice annunciation phrase" field. You can test the phrase to see what it will sound like by pressing the "Voice Test" button. These phrases can provide reminders about how a game is configured. Some example might be:

* "Use left joystick"
* "Use right 4 way joystick"
* "Use trackball with buttons on left"

How to Configure Command-Line Actions
=====================================
"Profiles" are the files containing specific game controller configurations created by game controller configuration software such as Ikari.vcd for Virtual Controller, or 4-way.ugc for UltraMap. To make command line creation easier, you may specify the name of a profile separately in the "Profile name" field, and then choose a command line template in the "Command line template" field, which will get filled in with the profile when the "Assign" button is pressed.  This template will typically contain one of the following field tags:

[profile_name]        - will be replaced by the filename or contents of "Profile name" field
[profile_full_name]   - will be replaced by the full path/file or contents of "Profile name" field

For example, if the profile is "C:\Ultrastik\Profiles\qbert.ugc" and the command line template is "C:\UltraMap\UltraMap.exe [profile_name]", then upon pressing the "Assign" button, the command line that will be assigned to the action will be "C:\UltraMap\UltraMap.exe qbert.ugc". If the full path to the profile is needed, then the command line template should be changed to "C:\UltraMap\UltraMap.exe [profile_full_name]. If the command line template has no field tags, then the command line will be used verbatim with no insertions. 

Additional Notes:
-----------------
* To test a command line while still in the Settings screen, press the "Test" button next to the Command Line Template field. Hovering over the "Test" button with the Show Tooltips option turned on, will show the actual command line that will be executed.

* If your profile filename needs quotes around it, then simply add quotes around the field tag in the template, such as "[profile_name]" or "[profile_full_name]".
 
* If you wish to trigger two command lines in a single action, click on the checkbox next to "Profile name 2" and you can configure a second command line using a completely different profile and command line template. There will be a one second delay between the execution of the first and second action.

* If you want to add a new template to VFE that will persist across sessions, you can edit any of the built-in ones and then use the Add button. You may also delete any template you no longer want to see in the list.  Note that whenever you do this both the "Command line Template" and "Command Line Template 2" lists will be synchronized to contain the same list of templates.

* As an FYI, these templates are saved in a file called templates.json in the root VFE folder. You may delete this file to restore the original shipping defaults.

* Be aware that VFE pauses active operation while the Settings screen is open, so be sure to close it when done with configuration.

Understanding the Action List Table
===================================
Each time you use the "Assign" button to create a new action, that action will be added to the Action List table. If you get a warning saying "Duplicate", arcadeVFE will highlight the duplicate action in the list at which point you may keep it or delete it.

When you complete the table, press the "Save list" button to save it.  It will be saved in the \user folder as a *.vfe file having the name specified in the "Activity list name" field above the table. By default this name is "Arcade Controller" (saved as "Arcade Controller.vfe"). If you switch between multiple controllers for use with your emulator, you could save different action lists under different names. These can then be loaded in the future by creating a shortcut that provides the name as a command line parameter when launching VFE.  For example,

vfe.exe "Arcade Controller" or
vfe.exe "Gamepad"

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

Command
-------
This is the command line template with field tags replaced (i.e. the actual command line that will be executed).

Command 2 and Command 3
-----------------------
These are the second and third optional command line templates with field tags replaced (i.e. the actual command lines that will be executed).


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
Saves all actions in the table to the <action list name>.vfe file. 

User Preferences
================
These options allow the user to make a few adjustments to the operation of arcadeVFE.

Operate only when this application is running
---------------------------------------------
This is a recommended setting for most use cases (and required for the RawAccel and Game Information Display options). To configure it, enter the name of the virtual arcade executable you will be running arcadeVFE with into this field and then check it. For example, for Time Capsule Arcade, you will enter "RetroVRArcade.exe" into this field (only enter the executable name, not the path). arcadeVFE will use this information to keep itself paused while it is not actively needed.

Run RawAccel when the application starts
----------------------------------------
RawAccel is a utility that can be found on GitHub at https://github.com/RawAccelOfficial/rawaccel. This software may be needed to tune some trackballs to have additional sensitivity. For example, I need it to make my Ultimarc U-Trak trackball work correctly in Arcade Time Capsule. To integrate RawAccel with arcadeVFE, simply install it to a subfolder of VFE called ..\RawAccel.

This option is only available when the "Operate only when this application is running" setting is configured. When this option is turned on VFE will automatically load RawAccel when the application runs, and will close RawAccel when the application closes. It is up to the user to configure RawAccel properly for their trackball before use. 

Show Game Information
---------------------
This feature will produce a desktop overlay on the primary monitor showing detailed text information, and possibly pictures, pertaining to the game currently running in the emulator. This information may be easily viewed while you are in VR by using your favorite desktop viewport (third party, or probably more typically the one provided with your headset). The text information comes from the mameinfo.dat and history.xml files in the arcadeVFE root folder. This display will automatically unload when the emulator is closed (which is why this feature is also only available when the "Operate only when this application is running" setting is configured).

To navigate through the Game Info screens, you will want to assign at least the move "Right" action in the game controller button configuration (and optionally, the "Left", "Start", and "Exit" options), using the "Game Info Navigation" radio switch at the top of the screen. If you would like pictures to be displayed along with the text information, just create a folder within the ..\assets subfolder of arcadeVFE, and fill it with *.jpg or *.png files having root names that are the same as the roms you would like to associate them with. Examples are provided in the ..\assets\cpanels and ..\assets\flyers folders. Feel free to add additional folders as you like.

Always voice annunciate
-----------------------
If you have configured voice annunciation phrases to your actions, then this switch can control when these are heard. This checkbox has three states. When checked (the default), the voice will be heard every time a game in the action table is loaded (including default games). When unchecked, voice annunciation is effectively turned off. Finally, if the checkbox is configured with the minus sign (-), then voice annunciation will only occur if an actual profile switch is conducted (see the **Note** in the ROM Monitor section above).

Beep on profile change
----------------------
This option will sound a beep whenever a profile switch happens. This can be useful as a debugging tool by asserting profile changes independent of the voice option.

Show Tooltips
-------------
In addition to this documentation file, the Settings screen implements tooltips on all controls to explain their operation. If you no longer need the tooltips, you can turn them off by unchecking the "Show Tooltips" checkbox.







  


