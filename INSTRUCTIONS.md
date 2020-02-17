# Arribada PMP v1.1 - instruction manual

## Description of operation
When the device is turned on and running, it will periodically enable and disable the 5V power supply, booting the Raspberry Pi module and camera.

After enabling the 5V power supply, the Raspberry Pi module will turn on, take a picture with Raspberry Pi camera, save it to USB flash drive and then shut itself down. When shutdown the Raspberry Pi also signals to the main board that it can now disable the 5V supply.

The main board will wait specified amount of time before again turning on the Raspberry Pi which will repeat the cycle.

## Turning on the device
1. Insert 18650 lithium-ion batteries into the device. Beware of the correct battery polarity; follow the markings on plastic battery holders.
2. To start the device, click the `battery activate` button in the corner of the board. You will be greeted with the IRNAS logo and Arribada PMP text, which will appear on the OLED display.
3. After the initial boot message on the OLED screen the device should be working normally.

## Checking captured pictures and setting environment variables
To access the captured pictures and to change the settings you will have to remove the USB flash drive, which is connected to the Raspberry Pi. There are two storage places, the `camera` directory and the `environment` file.

Captured pictures can be accessed in the `camera` directory. The pictures are named like this: `snapshot-{year}-{month}-{day}--{hour}-{minute}-{second}--{light}-(voltage)-(temperature).jpg`. The light parameter corresponds to light level detected by sensor when taking the photo.

The system can be configured by changing environment variables in the `environment` file located in the main directory. The file can be opened and modified with a text editor, e.g. Notepad or Notepad++.

A user can set how long the Raspberry Pi will stay turned off before being turned on to take a photo, which defines the time-lapse interval. This can be set by changing the values of `PIRA_SLEEP` and `PIRA_WAKEUP` variables, which take time values in seconds. Both variables should have the same value. For example, if we want the Raspberry Pi to stay off for 5 minutes before turning it on again, we will set the `PIRA_SLEEP` and `PIRA_WAKEUP` variables both to 300:
*	PIRA_SLEEP="300"
*	PIRA_WAKEUP="300"

In normal operating conditions, the Raspberry Pi is turned on for about 40 seconds. This means that setting the variables to 300 will set the time-lapse interval to approx. 340 seconds as it takes a minimum of 40 seconds to boot unless continous operation is configured.

⚠️ ATTENTION! Do not change any other variables to avoid disrupting the operation of the device!

## Accessing the device information on OLED display
Some basic information about the device can be seen on the OLED display. A user can see the `current time (UTC)`, `number of captured photos` and `time to next wakeup`. The information is displayed by pressing either `Button 1` or `Button 2` on the side of the board for approx. 5 second.

The current time (UTC) is obtained through the GPS. If there has not yet been a GPS fix after the device lost and regained power, a reset date that is saved in memory will be shown, which is 1.1.2020, 00:00. This will update once a fix has been aquired.

The number of captured photos and time to next wakeup are obtained from the Raspberry Pi just before the end of each cycle. If no cycle has yet been performed after the device lost and regained power, this information will not be available and will show once the Raspberry Pi has provided it.
