Getting started
===============
Immersive virtual reality experiences for all-sky astronomical data.

To see an example in action:
- Using a WebGL compatible browswer, navigate to https://astronomy.swin.edu.au/~cfluke/vr/webundle/ on your smartphone
- Tap the Google Cardboard icon in the lower right of the screen
- Place your smartphone into a Google Cardboard viewer
- Navigation: turn your head to see the celestial sphere around you.
- Menu: turn your head to look for the Menu icon.  Line up the green circular target, and hold your gaze steady.  The menu will expand.
- Selection: to toggle visibility of a data category or the celestial coordinate system, line-up the reticule on the menu item and hold your gaze steady.


Quickstart
^^^^^^^^^^

The Quickstart versions works on Linux and MacOSX operating systems.  It requires a C compiler (gcc or cc).

1. Download the contents of the allskyVR repository
2. Expand the zip file and move to the directory of your choice
3. Change into the allskyVR directory and execute the deploy script from the command line: <tt>deploy.csh</tt>
4. Create the sample VR environment: <tt>allskyVR -i exoplanets.csv -f format.txt</tt>
5. Transfer the export directory, <tt>VR-allsky</tt>, to a web server
6. Open your web browser, navigate to the export directory, and view <tt>index.html</tt>

You are now ready to explore your all-sky data with your personal head-mounted display.

Fully Customisable
^^^^^^^^^^^^^^^^^^

The Fully Customisable version requires a working installation of <a href="https://github.com/mivp/s2plot" target=_NEW>s2plot</a> (Version 3.4.0 or higher).  Please see the <tt>s2plot</tt> repository for installation notes, including the required environment variables.  

The <tt>allskyVR</tt> source code is written in C.  The preferred starting point is to modify and use the <tt>templateSpherical.c</tt> code. 

Before executing, set the following two <tt>s2plot</tt> environment variables to the same value (example uses tcsh <tt>setenv</tt> commands).  Choose a pixel size that is as large as possible for your display:

<tt>setenv S2PLOT_WIDTH 800</tt>

<tt>setenv S2PLOT_HEIGHT 800</tt>


Creating your own data file
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now it is time to explore your own dataset.

1. Create a comma-separated value (csv) data file (yourdata.csv in this example). 
Each celestial object is defined on a single line with the format: 

    RA,Dec,Radius,Category,Scale 

  - Celestial coordinates are in decimal degrees
  - For an all-sky view set the Radius to 1
  - Assign a category index number in the range [1..10]
  - Provide the relative scale factor, using value of 1 if you are not sure what to choose!
2. Create your immersive environment: allsky -i yourdata.csv -f format.txt

Creating your own format file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The format file sets the colours that will be assigned to the different category index values.   The text file format, one item per line, is:

    CAT=R,G,B,Label
    
R,G,B are integer red, green, and blue colour index values in the range [0...255], and <tt>Label</tt> is a short text-only label to appear in the A-Frame menu item.   It is necessary to avoid spaces and some symbols that have special meanings in LaTeX (e.g. $ and _ ).  The Label is ignored in Quickstart mode - customisation can be performed by creating relevant textures in appropriate graphics package.
 
For best visual quality, we recommended the use of colour choosing resources such as the <a href="http://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3">ColorBrewer 2.0</a>.

Troubleshooting
^^^^^^^^^^^^^^^

- Can't navigate? You may need to active WebGL in your browser.  For information on supported browsers see: https://get.webgl.org/get-a-webgl-implementation/
