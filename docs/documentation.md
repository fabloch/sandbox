# Documentation - fr

Atention, ce document vaut uniquement pour les réglages de la sandbox après une installation de une installation 

Pour le projecteur utilisé c’est ici :

https://www.projectorcentral.com/BenQ-MX631ST.htm


Les versions  installées actuellement sur le laptop MSI de la fabrique.


- Xubuntu 18.04
- Version 4.5-004 of the Vrui VR Development Toolkit (automatically selected by Vrui installation script)
- Version 3.6 of the Kinect 3D Video Package
- Version 2.5.004 of the Augmented Reality Sandbox

Pour une installation complète c’est ici :
http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/

Le tuto partira alors sur l’installation de Linux Mint et l’éditeur de texte XED
avec Ubuntu l’éditeur de texte est GEDIT, avec Xubuntu l’éditeur de texte par défaut est …
et les nouvelles versions des 3 “briques “ nécessaires pour faire fonctionner la SandBox.


- Version 4.6 of the Vrui VR Development Toolkit (automatically selected by Vrui installation script)
- Version 3.7 of the Kinect 3D Video Package
- Version 2.6 of the Augmented Reality Sandbox


Nous allons nous efforcer de commenter/compléter ici les réglages pour la calibration afin de remplacer le “savoir faire” trouvé dans les vidéos.

**System Integration, Configuration, and Calibration**

**Step 6: Connect and Configure the 3D Camera**
Plug in your 3D camera and download intrinsic calibration parameters directly from its firmware. In a terminal window, run:

    sudo /usr/local/bin/KinectUtil getCalib 0

This might ask you for your password again; if so, enter it to continue.
Step 6 starts at [28:52 in the walk-through video](https://youtu.be/R0UyMeJ2pYc?t=28m52s).


Step 6a (Optional): Calculate Per-pixel Depth Correction
First-generation Kinect cameras (Kinect-for-Xbox-360) have a certain amount of non-linear depth distortion. If you point such a camera at a flat surface, the 3D reconstruction will not be flat, but slightly bowl-shaped. This distortion can prevent getting a good alignment between the physical sand surface and the topographic map projection in [Step 10](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step10).
RawKinectViewer has a built-in calibration utility to correct for this distortion. This step is not necessary for operation of the AR Sandbox, but it usually improves alignment quality. Again, this issue only applies to first-generation Kinect cameras (models 1414, 1473, and 1517). It is easiest to perform this calibration step with the Kinect camera removed from the AR Sandbox, so if your Kinect is difficult to remove after assembly, it might be a good idea to do this step before putting it in place.
To perform per-pixel depth correction, place your Kinect camera such that it faces a large flat non-shiny surface, like an empty wall. Then start RawKinectViewer as administrator, as it will need to write a calibration file to the system location /usr/local/etc/Vrui-4.6/Kinect-3.7. In a terminal window, run:

    sudo /usr/local/bin/RawKinectViewer -compress 0

and enter your password if/when asked.
To begin calibration, move your camera towards the flat surface until black blotches start appearing in the depth image stream on the left side of RawKinectViewer's display window, and then pull back until there are only small and isolated black spots. It is best to have the camera face the flat surface head-on; rotate the camera left/right and up/down until the displayed depth color is uniform between the left, right, top, and bottom edges.
Next, assign a calibration tool to two arbitrary keys. Press the first key, say "A", and move the mouse to highlight "Calibrate Depth Lens" in the tool selection menu that pops up, then release the key. This will bring up a dialog window asking to press another key for tool function "Calibrate." Pick one, say "S", press and release it. This will close the dialog window.
To capture a calibration tie point, keep the camera very still and press the "A" key once. This will show a "Capturing average depth frame..." message. Do *not* touch or move the camera while this message is being displayed. After it disappears a few seconds later, move the camera a little distance further away from the flat surface, and press "A" again to capture the next tie point.
Repeat this process a few times to collect anywhere between five and ten tie points, from distances between about 0.5m and 1.5m. Once done, press the "S" key. This will calculate per-pixel depth correction factors and write them to a calibration file in the /usr/local/etc/Vrui-4.6/Kinect-3.7 directory. RawKinectViewer will print "Writing depth correction file /usr/local/etc/Vrui-4.6/Kinect-3.7/DepthCorrection-<camera serial number>.dat" when it is finished. If any error messages appear at this point, close RawKinectViewer and redo the entire process. Otherwise, close RawKinectViewer, install the camera in the AR Sandbox, and continue with the next installation step.
Step 7: Align the 3D Camera
Align your camera so that its field of view covers the interior of your sandbox. Use RawKinectViewer to guide you during alignment. To start it, run in a terminal window:

    cd ~/src/SARndbox-2.6
    RawKinectViewer -compress 0

Ignore the color video stream on the right side of RawKinectViewer's display window and focus on the depth image stream on the left (the AR Sandbox does not use the color video stream). Move and/or rotate the camera until it can see the entire interior of your sandbox.
Step 8: Measure Sandbox's Base Plane Equation
Calculate your sandbox's base plane, by following the instructions in the [AR Sandbox calibration video, starting at 0:00](https://youtu.be/EW2PtRsQQr0?t=0m0s). You can use the already-running instance of RawKinectViewer from [Step 7](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step7). You need to enter the base plane equation (and the 3D sand surface extents in the next step) into the BoxLayout.txt file in etc/SARndbox-2.6 inside the SARndbox source directory. To edit the file using xed, run in a terminal window:

    cd ~/src/SARndbox-2.6
    xed etc/SARndbox-2.6/BoxLayout.txt &

The ampersand ("&") at the end of the second command will keep the terminal window usable while the text editor is running. Now enter the base plane equation as described in the video. To copy text from a terminal window, highlight the desired text with the mouse, and then either right-click into the terminal window and select "Copy" from the pop-up menu that appears, or press Shift-Ctrl-c. To paste into the text editor, use the "Edit" menu, or press Ctrl-v. Or, highlight the desired text in the terminal window with the mouse, and then move the mouse into the desired position in the text editor window and press the middle mouse button to copy and paste.
RawKinectViewer prints two plane equations when a depth plane is extracted: the first in depth space, the second in camera space. The AR Sandbox needs the second, camera-space, plane equation. After copying it, the equation has to be reformatted slightly. RawKinectViewer will print:

    Camera-space plane equation: x * <some vector> = <some offset>

where <some vector> is a three-component direction vector defining the "up" direction in camera coordinates, typically close to (0.0, 0.0, 1.0), and <some offset> is the vertical position of the measured plane underneath the camera, which is in centimeters and negative. BoxLayout.txt needs that plane equation in the following format:

    <some vector>, <some offset>

where the direction vector and the offset are separated by a comma.
**Note:** For some reason, the depth plane equation reported by second-generation Kinect cameras (Kinect-for-Xbox-One) may be inverted. Before continuing, check that the fourth component (offset) of the camera-space plane equation is in fact negative. If it is not, flip the signs of *all four* components of the plane equation in BoxLayout.txt, e.g., (-0.01, 0.04, -0.9991), 105.3 becomes (0.01, -0.04, 0.9991), -105.3.
Step 9: Measure Sandbox's 3D Box Corner Positions
Measure the 3D extents of the sand surface. As of version 3.2 of the Kinect package, this can be done inside RawKinectViewer as well by following the instructions in the [AR Sandbox calibration video, starting at 4:10](https://youtu.be/EW2PtRsQQr0?t=4m10s). Make sure to measure the box corners in the order lower-left, lower-right, upper-left, upper-right. After you have copied the box corner positions into the text editor as described in the video, save the file (via the "File" menu or by pressing Ctrl-s), and quit from the text editor (via the "File" menu or by pressing Ctrl-q or by closing the window).
After Steps 8 and 9 have been completed, the contents of BoxLayout.txt should look like the following, with different numbers depending on your installation:

    (-0.0076185, 0.0271708, 0.999602), -98.0000
    (  -48.6846899089,   -36.4482382583,   -94.8705084084)
    (   48.3653058763,   -34.3990483954,   -89.3884158982)
    (   -50.674914634,    35.8072086558,   -97.4082571497)
    (   48.7936140481,    36.4780970044,     -91.74159795)

Ensure that this text starts in the first column of the first line, and that the file contains no other text at all.
Step 10: Align the Projector
Align your projector such that its image fills the interior of your sandbox. You can use the calibration grid drawn by Vrui's XBackground utility as a guide. In a terminal window, run:

    XBackground

After the window showing the calibration grid appears, press F11 to toggle it into full-screen mode. Ensure that the window really covers the entire screen, i.e., that there are no title bar, desktop panel, or other decorations left. Press the "Esc" key to close XBackground's window when you're done.
Ensure to disable all digital image distortion features of your projector before alignment, and only use optical features, i.e., optical focus adjustment and optical zoom. Specifically, disable any kind of digital keystone correction, and check that the projector maps the incoming video signal 1:1 to its display pixels. The best way to check for 1:1 matching is to look at the central horizontal bar in XBackground's test image. It should be a clear pattern of alternating white and black one-pixel-wide vertical lines with no smearing or stair steps.
Slight overprojection outside of the sandbox, and any remaining keystone distortion of the projected image, will be taken care of by the following projector calibration step.
Step 11: Projector/Camera Calibration
Calibrate the Kinect camera and the projector with respect to each other by running the CalibrateProjector utility:

    cd ~/src/SARndbox-2.6
    ./bin/CalibrateProjector -s <width> <height>

where <width> and <height> are the width and height of your projector's image in pixels, respectively. For example, for an XGA projector like the recommended BenQ model, the command would be:

    ./bin/CalibrateProjector -s 1024 768

Ensure that the given image size exactly matches the size of the projector's input video signal.
**Very important:** Set CalibrateProjector's window to full-screen mode by pressing F11 before proceeding. Then follow the instructions in the [AR Sandbox calibration video, starting at 10:10](https://youtu.be/EW2PtRsQQr0?t=10m10s). The calibration program expects a disk of diameter 120mm (4.7"), which is a standard CD, CD-ROM, or DVD. The easiest way to create a calibration disk is to glue a sheet of white paper to the data side of a CD/DVD/..., carefully cut around the edge of the CD, and draw a cross onto the paper that intersects exactly in the center of the CD's hole.
**Note:** Do not worry if the projected calibration image (yellow background, yellow or green disk) does not line up with the physical sandbox. This calibration step will *make* the image line up after it's done.
**Running the Augmented Reality Sandbox**
At this point, the Augmented Reality Sandbox is configured, calibrated, and ready to run.
Step 12: Run the AR Sandbox
To run the main AR Sandbox application, run in a terminal window:

    cd ~/src/SARndbox-2.6
    ./bin/SARndbox -uhm -fpv

The -uhm argument tells the SARndbox application to apply an elevation color map to the sand surface, and the -fpv argument tells it to use the projector/camera calibration collected in [Step 11](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step11).
**Very important:** Set SARndbox's window to full-screen mode by pressing F11, or the projector/camera calibration will not line up.
**Post-Installation Setup and Fine-Tuning**
The instructions above get the AR Sandbox software installed and running, but there are still a lot of (optional) improvements to be made. The following steps automate full-screen display and tool bindings, configure multiple displays, etc.
Step 13: Create Per-application Configuration File Directory
The Vrui VR toolkit supports per-application configuration files, to set display or interaction options, or pre-bind regularly-used tools. These configuration files are stored in a directory ~/.config/Vrui-<version>/Applications, and are given the same name as the application to which they belong, plus a .cfg extension. Create the configuration file directory by running in a terminal window:

    mkdir -p ~/.config/Vrui-4.6/Applications

Step 14: Create Configuration File for CalibrateProjector
Create a configuration file for the CalibrateProjector application using the xed text editor:

    xed ~/.config/Vrui-4.6/Applications/CalibrateProjector.cfg

Into that new file, paste exactly the following text:

    section Vrui
        section Desktop
            section Window
                # Force the application's window to full-screen mode:
                windowFullscreen true
            endsection
            
            section Tools
                section DefaultTools
                    # Bind a tie point capture tool to the "1" and "2" keys:
                    section CalibrationTool
                        toolClass CaptureTool
                        bindings ((Mouse, 1, 2))
                    endsection
                endsection
            endsection
        endsection
    endsection

then save the new file and exit from the text editor. (Reminder: You can copy&paste the above text by highlighting the entire contents of the text box with the left mouse button, then moving the mouse over into the empty text editor window, and pressing the middle mouse button.)
If you now start CalibrateProjector, its window will cover the entire screen, with no title bars or panels remaining. If you press the "1" key, the program will capture a calibration tie point, and if you press the "2" key, it will re-capture the background, indicated by the screen turning red for two seconds.
You can replace the "1" and "2" key names in the "bindings" tag with any other keys you like.
Step 15: Create Configuration File for SARndbox
Create a configuration file for the SARndbox application using the xed text editor:

    xed ~/.config/Vrui-4.6/Applications/SARndbox.cfg

Into that new file, paste exactly the following text:

    section Vrui
        section Desktop
            # Disable the screen saver:
            inhibitScreenSaver true
            
            section MouseAdapter
                # Hide the mouse cursor after 5 seconds of inactivity:
                mouseIdleTimeout 5.0
            endsection
            
            section Window
                # Force the application's window to full-screen mode:
                windowFullscreen true
            endsection
            
            section Tools
                section DefaultTools
                    # Bind a global rain/dry tool to the "1" and "2" keys:
                    section WaterTool
                        toolClass GlobalWaterTool
                        bindings ((Mouse, 1, 2))
                    endsection
                endsection
            endsection
        endsection
    endsection

then save the new file and exit from the text editor.
As in [Step 14](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step14), this will force SARndbox to start in full-screen mode, ensuring that the calibration created using CalibrateProjector exactly matches the one used in the actual AR Sandbox. In addition, the "inhibitScreenSaver" setting will prevent the screen from blanking if no keys are pressed, and the "mouseIdleTimeout 5.0" setting will hide the mouse cursor after five seconds of inactivity. To get the cursor back (for menu interactions etc.), simply move the mouse. Finally, the "WaterTool" section binds a tool to add or remove water to/from the entire AR Sandbox, by pressing "1" to rain, and "2" to drain. As previously, set the binding to whatever keys you prefer.
Step 16: Create a Desktop Icon to Launch the AR Sandbox
Starting the AR Sandbox may require typing a lengthy command line into a terminal window, which might get tedious. To simplify things, you can create a desktop icon to launch the AR Sandbox by simply double-clicking. This is best done in two steps: first, create a shell script to launch the SARndbox application with all command line arguments; second, link that shell script to a desktop icon.
To create a shell script, run in a terminal window:

    xed ~/src/SARndbox-2.6/RunSARndbox.sh

This will open an editor window with an empty file. Paste *exactly* the following contents into that file:

    #!/bin/bash
    
    # Enter SARndbox directory:
    cd ~/src/SARndbox-2.6
    
    # Run SARndbox with proper command line arguments:
    ./bin/SARndbox -uhm -fpv

Add any command line arguments you normally use to the last line. Then save the file, exit the text editor, and run in the same terminal:

    chmod a+x ~/src/SARndbox-2.6/RunSARndbox.sh

This will tell the operating system that the shell script can be executed.
To create a desktop icon, run in a terminal window:

    xed ~/Desktop/RunSARndbox.desktop

Into the empty text file, paste the following contents:

    #!/usr/bin/env xdg-open
    [Desktop Entry]
    Version=1.0
    Type=Application
    Terminal=false
    Icon=mate-panel-launcher
    Icon[en_US]=
    Name[en_US]=
    Exec=/home/<username>/src/SARndbox-2.6/RunSARndbox.sh
    Comment[en_US]=
    Name=Start the AR Sandbox
    Comment=

Replace <username> with your actual user name, to locate the shell script created in the previous step. Then save the file, exit the text editor, and make the file executable:

    chmod a+x ~/Desktop/RunSARndbox.desktop

Now, double-clicking the icon will start the AR Sandbox with all command line arguments.
Step 17: Launch the AR Sandbox on Login / Boot
To run the AR Sandbox as a computational appliance that starts automatically when the PC is powered on, you need to create an auto-login account during Linux installation in [Step 1](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step1), and create a shell script to run the SARndbox application as described in [Step 16](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step16). Then you add that shell script to your user account's start-up list. Select the "Startup Applications" applet in the MATE Control Center, and click the "Add" button next to the list of "Additional startup programs." Into the dialog box that opens, enter a name (such as "Start AR Sandbox"), and into the Command field enter the full name of the shell script, i.e., /home/<username>/src/SARndbox-2.6/RunSARndbox.sh, where you replace <username> with your actual user name.
The next time you log into your account, or the next time the PC powers up (if auto-login is enabled), the AR Sandbox will start automatically. To exit from the application, for example to run a new projector calibration or do other maintenance tasks, simply press the "Esc" key.
Step 18: Use Multiple Screens
If you are running an AR Sandbox from a laptop, or if your desktop computer has a main monitor in addition to the sandbox projector, you can tell CalibrateProjector and SARndbox to use the projector, and leave the main monitor for other purposes, such as starting scripts or displaying a secondary view of the virtual topographic map from arbitrary points of view. First, determine to which video output port the sandbox projector is connected. In a terminal window, run:

    xrandr | grep connected

The xrandr utility will print a list of all video output ports that exist on the computer, and information about the monitors/projectors connected to those ports. An xrandr report might look like this:

    DVI-I-0 disconnected primary (normal left inverted right x axis y axis)
    DVI-I-1 connected 2560x1600+0+0 (normal left inverted right x axis y axis) 641mm x 401mm
    HDMI-0 disconnected (normal left inverted right x axis y axis)
    DP-0 disconnected (normal left inverted right x axis y axis)
    DVI-D-0 connected 1600x1200+2560+0 (normal left inverted right x axis y axis) 367mm x 275mm
    DP-1 disconnected (normal left inverted right x axis y axis)

This report shows two connected monitors: One with 2560x1600 pixels connected to port DVI-I-1, and a secondary with 1600x1200 pixels and origin +2560+0, i.e., positioned to the right of the main monitor, connected to port DVI-D-0.
From your xrandr report, determine the port name connected to your sandbox projector, for example by looking for the projector's pixel size, e.g., 1024x768. Then direct CalibrateProjector and SARndbox to open their display windows on that video output port by editing their respective configuration files:

    xed ~/.config/Vrui-4.6/Applications/CalibrateProjector.cfg

and afterwards

    xed ~/.config/Vrui-4.6/Applications/SARndbox.cfg

In both files, insert the following "outputName" setting into the existing "Window" section:

            section Window
                ...
                # Open the window on a specific video output port:
                outputName <port name>
                ...
            endsection

where <port name> is replaced with the name of the actual video output port from your xrandr report, e.g., DVI-D-0.
Afterwards, starting CalibrateProjector or SARndbox will send their display windows to the sandbox projector and full-screen them there. Check that there are no remaining window frames or panels etc.
The xrandr utility can also be used to turn connected monitors/projectors on or off. For example, let's say that your main monitor is connected to port DVI-I-1, and your projector to port HDMI-0. Then you can turn on the projector, and place it to the right of your main monitor, by running:

    xrandr --output DVI-I-1 --auto --primary --output HDMI-0 --auto --right-of DVI-I-1

To turn the projector off again, run:

    xrandr --output DVI-I-1 --auto --primary --output HDMI-0 --off

Step 19: Show a Secondary View of the AR Sandbox
If you have multiple displays connected to the PC running your AR Sandbox, and have done the multi-screen setup in [Step 18](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step18), then you can show a second display window that does not just replicate the projected view shown in the sandbox itself, but that can show the captured 3D topography from arbitrary points of view, in full 3D, as explained in [this video](https://www.youtube.com/watch?v=NXD7Dfo7Ngo).
To create a secondary view, you first need to edit the SARndbox application's configuration file and instruct it to open a second window on a different display. Run in a terminal window:

    xed ~/.config/Vrui-4.6/Applications/SARndbox.cfg

At the beginning of the "Desktop" section, insert the following setting:

    section Vrui
        section Desktop
            # Open a second window:
            windowNames += (Window2)
            ...
        endsection
    endsection

Then, after the existing "Window" section, insert a new section "Window2" with the following settings:

    section Vrui
        section Desktop
            ...
            section Window
                ...
            endsection
            
            section Window2
                viewerName Viewer
                screenName Screen
                windowType Mono
                
                # Open the window on a specific video output port:
                outputName <port name>
                
                # Open the window to full-screen mode:
                windowSize (800, 600)
                windowFullscreen true
            endsection
            ...
        endsection
    endsection

where <port name> is replaced with the name of the actual video output port to which your non-sandbox display is connected, as gathered from your xrandr report in [Step 18](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step18).
After the above changes, SARndbox will open a second window on the secondary display, but it will still show the same fixed projector view as the main projector, possibly squished due to a different aspect ratio on the secondary display. To allow an independent view on the secondary display, you have to modify SARndbox's command line. The best way to do this is to edit the RunSARndbox.sh shell script you created in [Step 16](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step16). In a terminal window, run:

    xed ~/src/SARndbox-2.6/RunSARndbox.sh

The simple command line entered in [Step 16](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step16) only has two arguments:

    ./bin/SARndbox -uhm -fpv

These instruct SARndbox, in order, to apply the default elevation color map, and to lock the display to the projector calibration matrix captured in [Step 11](http://idav.ucdavis.edu/%7Eokreylos/ResDev/SARndbox/SoftwareInstallation.html#Step11). By default, SARndbox applies display options from the command line to all windows it opens, but this can be overridden by using a -wi <window index> argument, where <window index> is the zero-based index of a window. After seeing that argument, SARndbox will apply all following display options to all windows with the same or a larger index, and also reset the -fpv option. Thus, append the following to SARndbox's command line:

    ./bin/SARndbox -uhm -fpv -wi 1 -rws

The (optional) -rws argument will draw water as a three-dimensional surface instead of applying it to the topography as a texture, as is the default setting. This will create a better representation of water flow when seen from oblique angles.
After these changes, the AR Sandbox will show a navigable three-dimensional view of the 3D topography model, including water drawn as a real 3D surface, on the secondary display. The secondary display can be rotated, translated, and scaled as in many other 3D graphics software, using a combination of mouse buttons and keyboard keys. Most importantly, pressing the left mouse button will rotate the view around the center of the window, and pressing the "Z" key while moving the mouse will translate the view in the window's plane. Pressing the left mouse button and "Z" key together, while moving the mouse up and down, will scale the view (zoom in or out), as will rolling the mouse wheel. Finally, pressing the left mouse button, the "Z" key, and the left Shift key, while moving the mouse up or down, will "dolly" the view in or out of the window's plane, as will rolling the mouse wheel while pressing the left Shift key.
On start-up, SARndbox will show a default view of the 3D topography in its secondary window. If you would like to show a different view on start-up, you can use the navigation techniques described in the previous paragraph to create the perfect view that you want, and then save it. To do this, press and hold the right mouse button to show the main application menu. Move the mouse to the last entry, "Vrui System", and from there to the "View" sub-menu, then to the "Save View..." entry, and there release the right mouse button. This will open a file selection dialog where you can specify a file name and location for the view file about to be written. Leave the default file name ("SavedViewpoint0001.view") and default location (the AR Sandbox's project directory) alone, and press the "OK" button. This will close the file selection dialog and save the current view to the selected file.
After exiting from SARndbox, change the command line in the RunSARndbox.sh shell script again, this time appending a command to load the view file you just saved. Run in a terminal:

    xed ~/src/SARndbox-2.6/RunSARndbox.sh

and change the command line to:

    ./bin/SARndbox -uhm -fpv -wi 1 -rws -loadView SavedViewpoint0001.view

If you changed the name of the view file before saving it (or renamed it later), use the correct name here. Afterwards, the AR Sandbox will start up with your preferred view displayed in its secondary window.

