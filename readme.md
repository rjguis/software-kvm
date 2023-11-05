# Software-KVM
This repository documents an approach to having a single key toggle a keyboard, mouse and display between a Mac, Linux and a Windows system.

- Keyboard - Logitech MX Key Mac
- Mouse - Logitech MX Master 3
- Dell Monitor - Ultrasharp range

## Keyboard & Mouse
The logitech MX range like others support switching between multiple devices using a dedicated button on the device.

The repo https://github.com/marcelhoffs/input-switcher describes an approach to script device changes on Logitech devices.

I was unsuccessful in getting the approach working when the keyboard and mouse were connected using bluetooth.  Instead I adopted the use of the Logitech USB Receiver, which carries the additional advantage that the keyboard is available at boot time for BIOS/boot menu use.  

The hidapitester available for multiple OSs supports sending the relevant commands to switch the keyboard and mouse between devices.

As i was using the Logitech Recevier the vidpid was 46D:C52B.   This can be confirmed using hidapitester --list-details.

The 2nd hex byte in send-details is the index of the Logitech Keyboard/Mouse on the Logitech USB receiver.
The 5th hex byte in send-details signifies the computer number to switch to.  Zero indexed.   

## Monitor
Modern Dell monitors support scripting settings via ddcutil on Linux/MacOS and windduti on Windows.

It can be use to list 'capabilities' to identify the 'input source' feature number, and then value for that feature can set using 'setvcp'.   


## Bringing together with script & keyboard shortcut
For my setup i was using a PC (dual boot Linux/Windows) alongside a MacBookPro.   I wanted a single key to toggle between PC & Mac.

The corresponding scripts i came up with are at:  

    ├── linux
    ├── macos
    ├── windows

Launching the script based on a key was straightforward in Ubuntu using Settings->Keyboard.   On Windows to use my chosen key I exploited the Logitech Options software.
On MacOS i took the approach of using Automator' to create a 'service' which in turn was associated with the Key in Keyboard Settings. 