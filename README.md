# Vizi
A simple UDP-interfaced visual stimulus presentation program.

Run the .exe file to open Vizi. Vizi listens to UDP port 61557 for a string of numbers. These numbers control the visual stimuli presented by Vizi.

============================================================================================

Controller.vi is a LabVIEW program which provides a minimal degree of control of Vizi without any additional coding. It is simply a GUI for configuring the UDP packets sent to port 61557.

To use the Controller, simply open the .vi file and click [SEND UDP]. The various sliders control the visual stimuli. The number fields next to Texture and Patches select their respective textures.

Click the green buttons next to the Patches to turn them on/off and click their respective Update buttons to configure them.

Inputting a value to the [Control] field and clicking the green button next to it will configure the following properties of Vizi:

(1) Full screen mode

(2) Windowed mode

(3) VSync on

(4) VSync off
 
(5) Read in the Patch 1 and Patch 2 Identities (UDP packet numbers [13] and [22]) as an update to Vizi's resolution (X, Y)

(6) Preset resolution 1 (2048 * 1152)

(7) Preset resolution 2 (1680 * 1200)

============================================================================================

To control Vizi more flexibly, your experiment should communicate the right signals to Vizi via UDP.

The general design principle is that the user controls a full-field Background texture for stimulus presentation, an optional Occlusion mask, and up to 9 additional 'Patches' (think of overlapping sheets of paper) for more versatile stimulus presentation (e.g. sparse noise, multiple items).

Vizi interprets each UDP packet received at port 61557 as a string of 92 individual numbers, separated by blank spaces, with their ordering encoding the following:

[1] Control (0 or 1)

[2] Control value


=== Background ===

[3] Identity (e.g. (31) displays full contrast sine-wave gratings, (12) displays a constellation of triangles on a grey background... play with it! (1) means 'off'.)

[4] Rotation

[5] X phase

[6] Y phase

[7] Tiling (i.e. spatial frequency)

=== Occlusion ===

[8] Identity (only 51 or 52 for a circular cut-out and a gradual blend, respectively)

[9] Rotation

[10] Lateral position

[11] Vertical position

[12] Size

=== Patch 1 ===

[13] Identity

[14] Overlap (ranges 1-19 to determine the ordering with respect to other patches. Occlusion is at 10, Background at 20)

[15] Size

[16] Lateral position

[17] Vertical position

[18] Rotation

[19] X phase

[20] Y phase

[21] Tiling

=== Patch 2 : 9 ===

Same as Patch 1 above, repeated, up to [122]
