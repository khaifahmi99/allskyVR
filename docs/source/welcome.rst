Getting started
===============

*Immersive virtual reality experiences for all-sky astronomical data.*

To see an example in action using a Google Cardboard viewer:

* Using a WebGL compatible browswer, navigate to https://astronomy.swin.edu.au/~cfluke/vr/webundle/ on your smartphone
* Tap the Google Cardboard icon in the lower right of the screen
* Place your smartphone into a Google Cardboard viewer
* **Navigation**: turn your head to see the celestial sphere around you.
* **Menu**: turn your head to look for the Menu icon.  Line up the green circular target, and hold your gaze steady.  The menu will expand.
* **Selection**: to toggle visibility of a data category or the celestial coordinate system, line-up the reticule on the menu item and hold your gaze steady.

To exit the VR experience, you may need to either:

* Remove your smartphone from the Google Cardboard viewer, and tap the X icon (if visible) on the top-left corner
* Tap the "back" button on your smartphone, which should return to the web-browser

Please note that orientation-based navigation assumes that your smartphone is equipped with an accelerometer.

Quickstart
^^^^^^^^^^

The Quickstart versions works on Linux and MacOSX operating systems.  It requires a C compiler (gcc or cc).

1. Navigate to the Github repository: https://github.com/cfluke/allskyVR
2. Select *Clone or download*, then downland and expand the ZIP file 
3. Change into the *allskyVR* directory and ensure that permissions are set correctly on the scripts:

    chmod 744 *.csh
      
4. Execute the deploy script from the command line: 

    deploy.csh

5. Create the sample VR environment: 

    allskyVR -i exoplanets.csv -f format.txt

6. Transfer the export directory, *VR-allsky*, to a web server (see Troubleshooting section below)
7. Open your web browser, navigate to the export directory, and view *index.html*

You are now ready to explore your all-sky data with your personal head-mounted display.

Fully Customisable
^^^^^^^^^^^^^^^^^^

The Fully Customisable version requires a working installation of `S2PLOT <https://github.com/mivp/s2plot>`_ (Version 3.4.0 or higher).  Please see the *S2PLOT* repository for installation notes, including the required environment variables.  

The *allskyVR* source code is written in C.  The preferred starting point is to modify and use the *templateSpherical.c* code. 

Before executing, set the following two *S2PLOT* environment variables to the same value (the example uses tcsh *setenv* commands).  Choose a pixel size that is as large as possible for your display:

    setenv S2PLOT_WIDTH 800
    
    setenv S2PLOT_HEIGHT 800
    
Build and execute the *templateSpherical.c* example code:

    us2build.csh templateSpherical
    
    templateSpherical -i exoplanets.csv -f format.txt
    
At the Graphics device prompt enter 

    /S2MONO<enter> 
    
then press **Shift-V** to commence the VR asset export.  



Creating your own data file and format file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now it is time to explore your own dataset.

1. Create a comma-separated value (csv) data file (yourdata.csv in this example). 
Each celestial object is defined on a separate line with the format: 

    RA,Dec,Radius,Category,Scale 

* Celestial coordinates are in decimal degrees
* For an all-sky view set the Radius to 1
* Assign a Category index number in the range [1..10]
* Provide the relative scale factor for each object.  Use a value of 1 if you are not sure what to choose. In the exoplanet example, planetary systems in the main Kepler field have *Scale=1* to minimise overlaps in the visualisation.

2. The format file sets the colours that will be assigned to the different category index values.   The text file format, one item per line, is:

    CAT=R,G,B,Label
    
*R* , *G* , and *B* are integer red, green, and blue colour index values in the range [0...255], and *Label* is a short text-only label to appear in the A-Frame menu item.   It is necessary to avoid spaces and some symbols that have special meanings in LaTeX (e.g. $ and _ ).  The Label is ignored in Quickstart mode - customisation can be performed by creating relevant textures in an appropriate graphics package.
 
For best visual quality, we recommended the use of colour choosing resources such as the `ColorBrewer <http://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3">`_.

The number of entries in the format file *must* match the number of category indices assigned in the data file.

3. Create your immersive environment using the quickstart mode: 

    allskyVR -i yourdata.csv -f yourformat.txt
    
or in fully customisable mode, launch the executable and then press **Shift-V**:

    templateSpherical -i youdata.csv -f yourformat.txt


Troubleshooting
^^^^^^^^^^^^^^^

* *Can't navigate?* You may need to active WebGL in your browser.  For information on supported browsers see: https://get.webgl.org/get-a-webgl-implementation/

* *Don't have access to a web service?* A number of free website hosting services exist, but may not always be suitable for continous live operation without purchasing or upgrading an existing account.  One option is http://000webhost.com, which offers support for PHP and mySQL.  On signing in, create a web-site that will hold your *allskyVR* assets.  Upload all of the files containd in the export *VR-allsky* directory into the *public_html* directory, and you should be able to view the results in a WebGL compatible browswer.  See the example at https://allskyvr.000webhostapp.com
