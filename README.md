# media-ctl-setup #

This script aids users configuring Linux media-ctl pipelines for
video capture when using the i.MX6 based Ventana boards.

For information regarding the media-ctl API and Gateworks Ventana
boards video capture capabilities see:
 * http://trac.gateworks.com/wiki/linux/media

## Compatibility ##

This script is intended to run on the Gateworks i.MX6 based ventana boards.

----------

## Usage ##
The media-ctl-setup bash script takes a single argument of sensor type:
 - adv7180 - for Analog video capture
 - tda1997x - for HDMI video capture

The script will output commands to stdout which are intended to be sourced 
from the shell. It is important to 'source' them in order for exported
variables to be defined that specifcy things like the capture device.

Examples:


Analog raw video capture:
```
media-ctl-setup adv7180 > adv7180-raw-setup
source ./adv7180-raw-setup
```

Digital raw video capture:
```
media-ctl-setup tda1997x > tda1997x-raw-setup
source ./tda1997x-raw-setup
```

When sourced in the shell the script will execute the commands necessary to
configure the media-ctl pipeline for the currently connected video input.
Note that you will need to re-execute the media-ctl-setup script if the
video input source format (resolution/framerate/pixel-format/colorimetry)
changes.

The following env variables will be exported:
 - DEVICE - the Linux video device to capture from
 - ENCODER - the Linux video device providing hardware encoding
 - DECODER - the Linux video device providing hardware decoding
 - MEM2MEM - the Linux video device providing IPU IC mem2mem video conversion
 - GST_CONVERT - the GStreamer element providing IPU IC video conversion
