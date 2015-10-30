# iPeeU
Arduino Code to brute-force unlock an iPhone iPad PIN code / Passcode etc (possibly needs to be below iOS 8, although could be altered to turn off the phone after each attempt by wiring up to battery or putting some servos on the home and power buttons).

# Requires:
- iDevice camera connection kit for your iDevice model (lightning or 30-pin)
- USB A-B lead (same as printers use) -an OLED display on the device
- webcam in surveillance mode (to capture when it unlocks).
- maybe a power supply for the arduino, but the iDevice will power it.  Using a power supply does NOT charge the iDevice as well though

# Features:
- Works even if 'iPhone is Disabled, connect to iTunes' is shown (which will probably be shown during the cracking anyway)
- Allows the user to try specific PINs first -A date range can be specified to run next
- Won't repeat PINs already tried  during the current run
- Timing can be altered to run faster/slower.  Although be warned, to vary from defaults may make the iDevice ignore the correct PIN, please read the comments on each define before changing them

# Should be (but not tested):
- Easy to alter for 6 digit PIN codes
- Easy to compile for other Arduino boards (code is for a clone of an Arduino Uno, but for others, just change the pin-outs for the LED and OLED)

# Tested:
- iPad 4 (iOS 7.1.1)
- iPhone 4 (iOS 7.1.2)

# Possible Future  Work:
- Don't think I need the Return at the end of the PIN
- May not need the ESC at the start
- Add a LDR (Light Dependant Resistor) to a PIN and monitor the value that returns for a sudden change, then we have the PIN
- Sometimes the iDevice will not recognise it as a keyboard (just unplug it and plug it in again until it does). I'd like to figure out a way of detecting that the iDevice has not recognised it, Then reset through software until it does, or someway of making it so you don't have to unplug it until it recognises it (especially as in 'is disabled, connect to itunes' mode, as you can't see any feedback on the screen to know if it is recognised and working or not)
- Somehow power the iDevice at the same time

# Instructions:
## ***once only***
- Connect the OLED to the board, my pin-out is in the comment section of the code

## ***each time***
- Change the defines in the code to your own liking (note that the pin-outs for OLED and LED may need changing for your board)
- Upload the code to the arduino (use arduino's own IDE, works a treat)
- If need be (needed for the UNO) upload the keyboard firmware to the board, to change it into a HID keyboard (using FLIP and putting the board into DFU mode by bridging the two pins nearest the USB port.  Remember to power cycle it afterwards.  When done, or to upload the code again, if you change the define for instance, reflash with the arduino firmware, power cycling after the flash)
- Using whatever you have handy (I used a cup full of felt-tips) prop the board and OLED infront/to the side of the iDevice with the webcam pointing a them (check they are both in shot and focused, you may or may not also want to see the flashing LED light on the board, which shows when keys are being set to the iDevice, all keys not just the PIN).  For survellance software I used cyberlink youcam, but a freeware option is spycam.  Set it to take one frame of video per second. Start the survallance software. 
- Plug the USB from the board into the iDevice via the camera connection kit whilst the screen is OFF.  If the iDevice screen does not wake up when the LED on the board (ie a key press is sent), try unplugging it and pluggin it in again, or reflashing with the keyboard firmware (did you power cycle after).  With an iPhone (not iPad), I also found that the iDevice gave a short vibration when it finished each PIN, if it was connected properly.
- Press the reset key on the board to start the cracking from the beginning
- Wait..... If the iDevice run out ofbattery, change the define to start off from where the webcam says it died and set doFirst and doDate to false and reupload the code to the board
