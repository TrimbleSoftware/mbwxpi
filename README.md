MBWXPI (MeteoBridge WXnow.txt PlugIn)

Meteobridge user-defined plugin weatherstation to read, parse, convert and output weather data contained in a wxnow.txt file as a Meteobridge weatherstation. 
Operation of the plugin is customized by editing the accompanying UCI style config file.

This plugin is implemented as a rather sophisticated AWK script that downloads, parses, converts and outputs the values containd in a Cumulus or Weewx style wxnow.txt file into Meteobridge as user defined plugin weatherstation. 

The plugin has configurable options that are stored in the Openwrt UCI style configuration file named "mbwxpi". The following settings are configurable:
 
	wxnow_cmd: os command line to read wxnow.txt file from a webserver
	station_altitude: station altitude in meters
	rain_reset_month: month number to rest total rain to 0, 1 == Jan, 2 == Feb etc.
	logfile: pathname to meteobridge logfile
  pollsleep: plugin polling interval in seconds
  writetolog: flag set to 3 for vebose logging, 2 to write brief messages to logfile, set to 1 for no logging, except errors, set to 0 for no logging
	total_rain: total rainfall accumulated from wxnow.txt file over time in 0.1 mm

See the comments in the config file for more infomation.

This script also does an initial sleep to start its data gathering on an even polling time interval. For example if the polling interval is set to 60 seconds, the polling will start (and reoccure) on even minute intervals.

Sensor output:
    th0:    The "outdoor" temperature in 0.1 °C and humdity in %
    thb0:   These are duplicated "outdoor" values used for "indoor" temperature in 0.1 °C, humdity in % and station barometric pressure in 0.1 mb
    wind0:  Wind gust and wind speed in 0.1 m/s
    rain0:  Rain rate in 0.1mm/hr and total rain in 0.1 mm
    
To install on your Meteobridge PRO, NANO SD, RPI3 or RPI4 Meteobridge weather server:

Download the code (two files: mbwxpi.plugin and mbwxpi) from this repository and place these files into the "Scripts" folder share on your Meteobridge weather server.
Edit the configuration file (mbwxpi) as needed. In most cases the defaults should work.
From the Station tab on the Meteobridge web interface, select the "Station" tab and then the "Add Weather Station" button.
Select the the "User-Defined" entry from the Model: pulldown list.
Select the "script:mbwxpi" entry from the Plug-in: pulldown list
Select the "no restart of logger when lacking data from this station" checkbox.
Click on the "Save" button. (Ignore the error message the "Error (Station #x): Download of plugin script failed: No such file or directory". This seems to a superflous error and the plugin will be added to Meteobridge anyway.)
Check the "System/Logging" tab to see timestamped messages written to the logfile by the plugin (if logging is enabled) or the Live "Data/Raw Sensor Data" tab to see the sensor output.

Meteobridge forum topic: 

For more information on Meteobridge weather server visit this page: https://www.meteobridge.com/wiki/index.php/Home
