The Andor Server can be accessed by running `andor_server.py` on the [[camera computer]]
To start the camera, make sure the following settings are set:
- EMCCD Gain: 300
- Exposure: 0.100s
and then press "Live Video"
You'll see a bunch of noise. Move the levels so that the bulk of the histogram is below the lower bound of your levels. Usually a good range is from ~400 to ~1000

Once you load an ion, you can reduce the side of the image region to make the frame rate less choppy

Double clicking on a spot will move the crosshairs there. The crosshairs are useful as a reference frame for whether the ion is moving, and for measuring the ion's position. 