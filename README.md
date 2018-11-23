# Video Experimenters Board
This is a circuit intended to facilitate experimentation with the ADV7184 video decoder and ADV7341 encoder, both from Analog Devices. 
It enables a microcontroller to display colour graphics over an NTSC or PAL video feed, by providing RGB and pixel-switch signals in sync with the video. Currently I am using this board as a basis for designing a colour OSD for multicopters and radio-controlled vehicles. See more about the project here: https://wekaosd.home.blog

To interface with the VEB you will need to do several things:
1. Provide regulated 1.8V and 3.3V power supplies
2. Program the 2 ICs using the I2C protocol via the SCK and SDA connectors. Programming scripts can be found at the Analog Devices website, or you can check the source for WekaOSD and see what I have done.
3. Feed the horizontal and vertical sync signals (HS and VS), and optionally odd/even field (FLD) and interrupt (INT) signals to your microcontroller. The microcontroller needs to lock to HS and VS, in order to send graphical output in sync with the video.
4. Generate RGB video signals, and use the fast-blank (FB) line to switch between the video feed and graphics as appropriate. RGB should be in the range of 0 - 0.7V. FB can be up to 3.3V. 
5. Connect an NTSC or PAL video source to one of the inputs, and a video monitor to one of the outputs. Component video output is also possible, and component video input should also work but I have not attempted to do so.

You will most likely want to implement a digital pixel bus with one or more bits allocated to each colour channel, and use a resistor divider to convert the digital signals to analogue RGB.

The STM32F4 series of microcontrollers are suitable microcontrollers, but any reasonably fast microcontroller should be capable. Given what has been achieved with the UzeBox project even an Arduino should be able to drive the VEB.
