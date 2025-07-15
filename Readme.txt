Background Game Profile Switcher (BGPS)
By David Dahlstrom

Summary
=======
BGPS provides the ability to switch game controller profiles automatically in the background based on what game is being played, or manually by pressing buttons on a keyboard or game controller. The primary use case for this utility is to more conveniently facilitate game profile switching when playing emulated MAME games in a VR environment using authentic arcade controllers whose mappings and behaviors need to be customized beyond what can be achieved using in-game settings alone.  

Tested Software
===============
BGPS has been tested for use with the following software.

* Arcade Time Capsule (a MAME-based VR arcade)
* Virtual Controller  (software to create virtual XInput controllers)
* Ultimarc UltraMap   (software to modify behavior of Ultimarc's UltraStik 360 joysticks)

Feel free to experiment with other software.

Installation
============
To install, extract the distribution zip file to a folder on your Windows computer that has read/write access. When you run the executable (BGPS.exe), you will see a joystick icon in the Windows tray and normal background mode is active. Right clicking on this icon will show a menu of options.

Configuration
=============
BGPS offers two different modes of operation. The first is a "ROM Monitor" mode which executes command line actions whenever a rom file is accessed by a game engine. The second mode provides the ability to execute command line actions by pressing a game controller button or keyboard key. 

ROM Monitor:
------------
To setup a rom to be monitored, choose "ROM Monitor" from the device list in the Settings screen. Ensure that the "ROM folder to monitor" field is filled in with the name of a valid folder containing MAME rom *.zip files. Next, choose the rom that will trigger the action and use the "Profile name" and "Command line template" fields to configure the command line that will execute when that game is loaded. Finally, press the "Assign" button to add the action to the list.

Note that if you choose "[Default]" as the rom, the profile you configure and assign to this action will be loaded whenever a rom having no specific configuration is loaded. Be aware that BGPS is "smart" about not reloading a profile that is already loaded. So if you switch between games that use the same profile (such as two default games), profile loading will be suppressed for the second since it is already loaded.

Buttons and Key presses:
------------------------
To setup a command line that will run upon a button or key press, Choose "Keyboard" or one of the game controller devices from the device list in the Settings screen. Next, use the "Profile name" and "Command line template" fields to configure the command line that will execute when the button or key is pressed. Finally, press the "Assign" button to assign the button or key you would like to use to the list.

Voice Annunciation
==================
If you would like BGPS to verbally annunciate the configuration that is being loaded, just add a phrase to the optional "Voice annunciation phrase" field. You can test the phrase to see what it will sound like by pressing the "Voice Test" button.

How to configure Profiles and Command Line Templates
====================================================
Profiles are files such as myprofile.vcd for Virtual Controller or myprofile.ugc for UltraMap. You may specify the profile in the "Profile name" field, and then choose or type a command line template in the "Command line template" field.  This template me be configured with one of the following field code:

[profile_name]        - will be replaced by the filename or contents of "Profile name" field
[profile_full_name]   - will be replaced by the full path/file or contents of "Profile name" field

For example, if the profile is "C:\Ultrastik\Profiles\qbert.ugc" and the command line template is "C:\UltraMap\UltraMap.exe [profile_name]", then upon pressing the "Assign" button, the final command line to be executed when the action is triggered is "C:\UltraMap\UltraMap.exe qbert.ugc". If the full path to the profile is needed, then the command line template could be changed to "C:\UltraMap\UltraMap.exe [profile_full_name]. If the command line template has no field code, then the command line will be used verbatim. 

If you wish to trigger two command lines in a single action, click on the checkbox next to "Profile name 2" and you can configure a second command line using a completely different profile and command line template.

If you want BGPS to remember certain command line templates, you can use the Add and Remove buttons next to the "Command line template" field to add or remove favorite templates to the list.  When you do this, both of the "Command line template" lists will be synchronized to contain the same list of templates (these will be saved across sessions).

Understanding the Action table
==============================
Each time you use the "Assign" button to create a new action, that action will be added to the actions table, and the following columns will be populated.

Device
This is the device you chose from the device list.

Action
This is the game rom if you chose the "ROM Monitor" device, or a keyboard key if you chose the "Keyboard" device, or a button number if you chose a game controller.

Sequence
For "Keyboard" and game controller actions, it is possible to assign multiple different actions to the same key or button. The effect of this is that when you press that key or button once, the action with a sequence number of 1 will be triggered. When you press that same key or button a second time, the action with a sequence number of 2 will be triggered, and so forth (with each action being verbally annunciated if you provided an annunciation phrase with each). This provides the means to manually switch between multiple profiles using a single key or button. To change the sequence of an action, just use the "Move Up" and "Move Down" buttons and you will see the sequence number for that action adjust according to its position in the list.

Annunciation
This is the annunciation phrase you assigned to the action.

Profile
This is the name of the profile that was entered.

Command Line
This is the command line template with the profile inserted.

Profile 2
This is the name of any second (optional) profile that was entered.

Command Line 2
This is the second command line template, if one was configured.

Managing the Action table
=========================
Below the Actions table are several additional buttons that can be used to manage the entries.

Move Up / Move Down
These buttons are intended for use in changing the sequence order of actions assigned to a single button or key press as described above under "Sequence".

Clear All
This clears the entire table.

Edit Action
Copies fields from the selected row back into the editor fields.

Delete Action
Removes the selected row from the table.

Save
Save all actions in the table to the bgps.json file. This is the configuration file that will be used normal background operation mode once the Settings screen is closed. 





  


