# MIDIDocs
USB-MIDI Documentation for Zoom G5 MultiFX Pedal

# Connecting to the device
The Zoom G5 communicated using Sysex messages, these have a specific format as follows:

    F0 [Vendor ID] [Device ID] [Product ID] [Command] F7

To get the Vendor ID and Device ID you can send a MIDI Identity Sysex Message:

    F0 7E 00 06 01 F7

This response is this:

    F0 7E 00 06 02     52          5B 00 00 00 31 2E 32 30 F7
           ^ Device ID  ^ Vendor ID ^ Product ID
           
# Sending Messages
## Editor Mode - Command 50/51
For most commands below, the device needs to be put in Editor Mode, this is done by sending command 50 to turn it on,  and 51 to turn it off.

## Get Bank and Patch Number - Command 33
Sending command 33 gets the current bank and program number, but this will also be returned whenever the patch changes.

The response is 2 CC Messages and a PC Message:
    
    B0 00 00
    B0 20 [Bank Number (00-62)]
    C0 [Patch Number (00-03)]
    
## Get Current Patch Details - Command 29
WIP - Need to work out what information is given

## Get Patch Number Details - Command 09 00 00 [Patch Number]
WIP - Need to work out how to get patches above 7F (It's something to do with the overflow bytes described below)

## Change Patch/Global Options - Command 31 A B C 00
There are multiple options to change the current patch or global settings all with the same format:

### Change Effect
    A = Effect Slot Number (00-08)
    B = 00
    C = Effect Number (??)

### Toggle Effect
    A = Effect Slot Number (00-08)
    B = 01
    C = 00 (off)/01 (on)
    
### Change Tap Tempo
    A = 0C
    B = 02
    C = 00 00 (00 00 - 7F 00 - 00 01 - 01 7A)
    
### Change Patch Level
    A = 09
    B = 02
    C = 00 00 (00 00 - 78 00)
    
### Change External Control Switch assignment
    A = 09
    B = 03
    C = 00 - 08 for Effects, 09 for Z Pedal, 0A for Tap Tempo and 0B for Mute

### Change Signal Direction
    A = 0C
    B = 03
    C = 00 (L -> R)/01 (R -> L)


# Recieving Messages
For most messages to be recieved the device needs to be in editor mode (see above).

## Recieving Patch Data
WIP - Need to work out what information is given

## Recieving Effect Changes
WIP - Need to work out what information is given

## Recieving Setting Changes
WIP - Need to work out what information is given
    
    
