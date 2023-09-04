### About This Project
This project utilizes Google geocoding API to take user entered data and place them on a Google Map. This works best with specific locations with one distinct location.

This script also utilizes SQLite and you will need to download this. Instructions are below:

You should install the SQLite browser to view and modify
the databases from:

http://sqlitebrowser.org/

### How to Use this Project

The first phase of the project uses where.data and reads one line at a time, retreives the geocoded response, and stoires it in the database (geodata.sqlite). B
To prevent excessive calls, before we use the geocoding API we already have the data for that particular line of input. If found it is stored in the database.

You can re-start the process at any time by removing the file
geodata.sqlite

If you want to try this with the API key, follow the
instructions at:

https://developers.google.com/maps/documentation/geocoding/intro

and put the API key in the code.

### Example of a Successful Run - Sample run after there is already some data in the database:

Mac: python3 geoload.py

Win: geoload.py

Found in database  Northeastern University

Found in database  University of Hong Kong, Illinois Institute of Technology, Bradley University

Found in database  Technion

Found in database  Viswakarma Institute, Pune, India

Found in database  UMD

Found in database  Tufts University

Resolving Monash University
Retrieving http://py4e-data.dr-chuck.net/json?key=42&address=Monash+University
Retrieved 2063 characters {    "results" : [
{u'status': u'OK', u'results': ... }

Resolving Kokshetau Institute of Economics and Management
Retrieving http://py4e-data.dr-chuck.net/json?key=42&address=Kokshetau+Institute+of+Economics+and+Management
Retrieved 1749 characters {    "results" : [
{u'status': u'OK', u'results': ... }

The first five locations are already in the database and so they
are skipped.  The program scans to the point where it finds un-retrieved
locations and starts retrieving them.

The geoload.py can be stopped at any time, and there is a counter
that you can use to limit the number of calls to the geocoding
API for each run.

Once you have some data loaded into geodata.sqlite, you can
visualize the data using the (geodump.py) program.  This
program reads the database and writes tile file (where.js)
with the location, latitude, and longitude in the form of
executable JavaScript code.



### A run of the geodump.py program is as follows:

Mac: python3 geodump.py
Win: geodump.py

Northeastern University, 360 Huntington Avenue, Boston, MA 02115, USA 42.3396998 -71.08975
Bradley University, 1501 West Bradley Avenue, Peoria, IL 61625, USA 40.6963857 -89.6160811
...
Technion, Viazman 87, Kesalsaba, 32000, Israel 32.7775 35.0216667
Monash University Clayton Campus, Wellington Road, Clayton VIC 3800, Australia -37.9152113 145.134682
Kokshetau, Kazakhstan 53.2833333 69.3833333
...
12 records written to where.js
Open where.html to view the data in a browser

The file (where.html) consists of HTML and JavaScript to visualize
a Google Map.  It reads the most recent data in where.js to get
the data to be visualized.  Here is the format of the where.js file:

myData = [
[42.3396998,-71.08975, 'Northeastern University, 360 Huntington Avenue, Boston, MA 02115, USA'],
[40.6963857,-89.6160811, 'Bradley University, 1501 West Bradley Avenue, Peoria, IL 61625, USA'],
[32.7775,35.0216667, 'Technion, Viazman 87, Kesalsaba, 32000, Israel'],
   ...
];

To view the results open where.html in a browser.  You
can hover over each map pin to find the location that the
geocoding API returned for the user-entered input. If you
cannot see any data when you open the where.html file, you might
want to check the JavaScript or developer console for your browser.

