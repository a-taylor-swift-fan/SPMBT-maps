# SPMBT-maps
Satellite height data to WinSPMBT map utility

Requirements:
* Linux
* Perl (5.?)
* Perlmagick (imagemagick utility)
* SRTM3 map data files from the region of your choice from http://dds.cr.usgs.gov/srtm/version2_1/SRTM3/

Installation:

Install the linux utlities perl and perlmagick:

Ubuntu and Debian:

sudo apt-get install perl perlmagick libgetopt-mixed-perl libjson-perl libwww-curl-perl


Usage:

perl map.pl --la N60.215486 --lo E24.768715 --water=1 --min 5

Will generate a map (approximately) centered at N60.215486,E24.768715, will reduce the height by 5 meters and will (later) convert the hexes with height less than 1 to water hex.

There will also be a small scale image xx.gif which contains the raw data (unscaled) and the upscaled image x.gif which is used for hex conversion.

Load the map nr. 999 into Map Editor, set fill range to 255 and clear terrain leaving the height information intact using the fill. This will redraw the hexes properly. Enjoy!

In case you get an error "410: No images defined" you need to install GhostScript as well. Run

sudo apt-get install gs

ISSUES AND BUGS:
* Water not yet implemented
* Will work best on non-coastal areas (water)
* Center of map may differ from specified location by some hexes
* -w shorthand trouble
* All the height data in hex are chosen by closest pixel which may cause unintended phenomena, i.e. artifacts in the map. Fix them by hand.


ADDENDUM AS OF 12-NOV 2025:
For new users using the latest version of Linux.
These procedures were written for and tested using Ubuntu 24.04.3 LTS.

These must be done after installing the dependencies mentioned previously.
  sudo apt-get update
  sudo apt-get install build-essential
  sudo apt-get install libswitch-perl 

Also, libgetopt-mixed-perl must be installed manually. This package is no longer included in latest versions of Linux distributions.

  Download here and install in terminal via sudo'd dpkg:
  https://mirror.cc.vt.edu/pub2/ubuntu/pool/universe/libg/libgetopt-mixed-perl/libgetopt-mixed-perl_1.008-10.2_all.deb

  sudo dpkg -i libgetopt-mixed-perl_1.008-10.2_all.deb

NOTE:
Possible off-by-one not-a-bug bug with the script where the longitude is off to the left by one. Incrementing the longitude by 1 fixes the issue.

For example, to recreate the downtown Louisville, KY USA area--Google says its coordinates are N38.26152, W85.74163.

On the Linux terminal, this must be entered as:

	$ sudo perl strm3-map.pl --la N38.26152 --lo W86.74163 --water=1 --min 5

NOTE 2:
When downloading heightmap files, ensure that they are also located in the same directory where the Venhola map tool resides. Otherwise the script throws an error message stating it cannot find the .hgt file.
