# Teams Presence for Raspberry Pi
An open source python script to display your Microsoft Teams presence to an RGB LED panel. This project uses an [Unicorn pHAT for Raspberry Pi Zero](https://shop.pimoroni.com/products/unicorn-phat) combined with the latest version of the Microsoft Graph API.
It supports a variety of presence types, eg.
   - Available = Green
   - Busy = Red
   - Away = Yellow
   - Out of office = purple
   - and a lot more!

The Python script pulls the Microsoft Teams presence by using the Microsoft Graph API every 30 seconds and prints the result to console. The presence object will then be converted to a color, whill is displayed with the pHAT.

## Features
The script includes the checked features, while others are planned:
- [x] Display the current Microsoft Teams presence as RGB
- [x] Update the status every 30 seconds
- [x] Turn off LEDs at night
- [x] Start script with arguments
- [ ] Check for version number

## Prerequisites
- Get Rasbian running with the latest version of Python3
- Solder your pHAT with your Raspberry Pi

## Installation
To install the script and all the according libraries, clone the repository and run the ```sudo ./install.sh``` command.
Also, you will need to create your own Azure AD app. You will probably need permissions from your Azure administrator. As an alternative use the ids from the [original project](https://www.eliostruyf.com/diy-building-busy-light-show-microsoft-teams-presence/).

## Run the script
To run the script, simply execute the main file with ```sudo python3 teams-presency.py```. If you start the script the first time, it will ask you for your *Azure Tenant ID* and *Azure Client ID*.
Next it will ask you to register the app with your Azure Active Directory by following the displayed URL and logging in with your Microsoft work credentials. These will be stored in a cache file.
> **Note:** The script requires sudo, elsewise it will fail to run.

## Available options
Get all options with the ```sudo python3 teams-presence.py --help``` command. Included is:
   - ```--help``` - prints the help dialog
   - ```--version``` - prints the version number of the script
   - ```--refresh``` - sets the refresh value in seconds. Must be greater than 10 seconds.
   - ```--brightness``` - Sets the brightness of your pHAT. Must be between 0.1 and 1.
   - ```--afterwork``` - Check for presence after working hours.
   - ```--nopulse``` - Disables pulsing, if after work hours.

## Original project
This project is inspired by the [original project] back from April 2020 by Elio Struyf. He did an awesome job with his project, but it felt strange on how complicated everything was by setting up a local webserver and adding homebridge to update a presence light. 
Therefore I took the idea from pulling the presence status, but removing all the web service and homebridge parts. My version of the Teams presence status indicator simply pulls the Microsoft Graph API every 30 seconds and converts the result into a color, which will be displayed by the RGBs.

## Supported presence types
The script uses the [presence object](https://docs.microsoft.com/de-de/graph/api/resources/presence?view=graph-rest-beta) from the Microsoft Graph API. Implemented types are:
   - Available
   - Away
   - BeRightBack
   - Busy
   - DoNotDisturb
   - InACall
   - InAConferenceCall
   - Inactive
   - InAMeeting
   - Offline
   - OffWork
   - OutOfOffice
   - PresenceUnknown
   - Presenting
   - UrgentInterruptionsOnly
