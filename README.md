
### Metar.sh 

A simple cli tool to get your weather report. 

Basic sytax :

	metar 'get'
	metar 'print'
	metar 'set' station
	metar 'list' [prefix]
	metar 'closest' [latitude longitude] [list]


Description : Metar.sh is a simple utility for find weather stations and get METAR reports. Most METAR stations are
	      airports.

CLI actions :

	get
		Gets the most recent weather report from the selected METAR
		station. The first line in the report will contain the station's
		name, country, ICAO station identifier, and location. There are
		however some station there this information is missing.

Example : $ metar get or metar 'get'


	print
		Print the ICAO station identifier of the selected METAR station,
		the station from which weather reports are retrieved. This is
		equivalent to running,

		(cat ~/.config/metar || cat /etc/metar) 2> /dev/null | head -n 1

Example : $ metar print or metro 'print'

	set station

		Stores the station as the METAR station from which weather
		reports shall be retrieved. station shall be the stations's
		ICAO station identifier. This is equivalent to running

		printf '%s\n' station > ~/.config/metar

Example : $ metar set 'insert_station_name'


	list [prefix]

		Print all METAR stations. This can take a very long time. For a,
		not as good, list you can look at http://www.aviationweather.gov/static/adds/metars/stations.txt
		Optionally the output can b e stored in a file.

		To speed up the listing process, you can filter the output
		by selecting the prefix of the ICAO station identifiers. If you
		look at the page with the URL above, you will find the prefix regex
		for your country.  These regular expressions are listed in the prefixes file.

		Each station will be printed on a line, containing the its
		name, country, ICAO station identifier, and location. The
		ICAO station identifier is in parenthesis. 


Example : $ metar list 'v[aeio]' will start printing the list of stations in India which can then be 'set' and 'get'   					 from the list.


	closest [latitude longitude] [list]
		Given a latitude and longitude in decimal format, print the
		ICAO station identifier of the closest METAR station. If you
		have already created a list of all stations using the action
		list, specify the filename of that list as the list argument.
		If latitude and longitude are omitted, ~/.config/geolocation,
		or /etc/geolocation, is used.

Example operation : Run make install from your shell to install the script. 
		    To run the shell script, run meter from the shell followed by the desired parameters.
		    
			
		    $ metar set 'station_code'
                    $ metar get
		
		This will print the details of the specified station.

		    $ metar list 'v[aeio]' (this will print out all the stations)
		    $ meter set 'station_code' (this sets the desired station to be returned via get)
		    $ meter get (to return the station's details)		    


File info

	~/.config/metar

		Contains the ICAO station identifier for the selected weather
		station, and nothing else, except an LF at the end. This will
		never change. Other programs are encouraged to use this file
		too.

		If the file contains more than one line, only the first line,
		even if it is empty, is used.

	/etc/metar

		Fallback file use if ~/.config/metar is missing. Other
		programs are encouraged to use this file too.

	~/.config/geolocation

		Used to get your location in case 'metar closest' is invoked
		without LATITUDE and LONGITUDE. This file contains your
		geographical location using the Global Positioning System in
		decimal format. This will never change. Other programs are
		encouraged to use this file too.

		If the file contains more than one line, only the first line,
		even if it is empty, is used.

	/etc/geolocation
		Fallback file use if ~/.config/geolocation is missing. Other
		programs are encouraged to use this file too.
