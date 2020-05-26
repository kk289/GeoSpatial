# GeoSpatial

Data Co-ordinates:

Fast Food:

1. Paradocs Coffee And Tea (34.057163, -118.364126)
2. Little Ethiopia (34.057035, -118.364565)
3. Lalibela (34.057426, -118.364533)
4. Market (34.057062, -118.364129)
5. E & M Cafe (34.057144, -118.363983)

Museum:

6. Academy Museum of Motion picture (34.063318, -118.360797)
7. Peterson Automotive Museum (34.062129, -118.361624)
8. The La Brea Tar Pits and Museum (34.063798, -118.355438)
9. Los Angeles Museum of the Holocaust (34.074531, -118.355719)
10. The Getty (34.078048, -118.474077)

Libraries:

11. Science and Engineering Library (34.019628, -118.288748)
12. Hoose Library of Philosophy (34.018698, -118.286600)
13. Leavey Library (34.021723, -118.282784)
14. Grand Avenue Library (34.019070, -118.276407)
15. J. Thomas McCarthy Library (34.031344, -118.276789)


KML File with 15 Coordinates: 

```
?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://earth.google.com/kml/2.0">
	<Document>
		<Style id="z1">
			<IconStyle><Icon><href>http://maps.google.com/mapfiles/kml/shapes/dining.png</href></Icon></IconStyle>
		</Style>
		<Style id="z2">
			<IconStyle><Icon><href>https://maps.google.com/mapfiles/kml/shapes/library_maps.png</href></Icon></IconStyle>
		</Style>
		<Style id="z3">
			<IconStyle><Icon><href>https://maps.google.com/mapfiles/kml/shapes/museum_maps.png</href></Icon></IconStyle>
		</Style>


<Placemark>
	<name>Fast Food</name>
	<styleUrl>#z1</styleUrl>
	<Point>
		<coordinates>-118.364126,34.057163</coordinates>
	</Point>
	</Placemark>

	<Placemark>
		<name>Fast Food</name>
		<styleUrl>#z1</styleUrl>
		<Point>
			<coordinates>-118.364565,34.057035</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Fast Food</name>
		<styleUrl>#z1</styleUrl>
		<Point>
			<coordinates>-118.364533,34.057426</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Fast Food</name>
		<styleUrl>#z1</styleUrl>
		<Point>
			<coordinates>-118.364129,34.057062</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Fast Food</name>
		<styleUrl>#z1</styleUrl>
		<Point>
			<coordinates>-118.363983,34.057144</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Museum</name>
		<styleUrl>#z3</styleUrl>
		<Point>
			<coordinates>-118.360797,34.063318</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Museum</name>
		<styleUrl>#z3</styleUrl>
		<Point>
			<coordinates>-118.361624,34.062129</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Museum</name>
		<styleUrl>#z3</styleUrl>
		<Point>
			<coordinates>-118.355438,34.063798</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Museum</name>
		<styleUrl>#z3</styleUrl>
		<Point>
			<coordinates>-118.355719,34.074531</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Museum</name>
		<styleUrl>#z3</styleUrl>
		<Point>
			<coordinates>-118.474077,34.078048</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Libraries</name>
		<styleUrl>#z2</styleUrl>
		<Point>
			<coordinates>-118.288748,34.019628</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Libraries</name>
		<styleUrl>#z2</styleUrl>
		<Point>
			<coordinates>-118.286600,34.018698</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Libraries</name>
		<styleUrl>#z2</styleUrl>
		<Point>
			<coordinates>-118.282784,34.021723</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Libraries</name>
		<styleUrl>#z2</styleUrl>
		<Point>
			<coordinates>-118.276407,34.019070</coordinates>
		</Point>
	</Placemark>
	<Placemark>
		<name>Libraries</name>
		<styleUrl>#z2</styleUrl>
		<Point>
			<coordinates>-118.276789,34.031344</coordinates>
		</Point>
	</Placemark>
	</Document>
</kml>
```

PostgresSQL Queries:

```
CREATE EXTENSION postgis;
CREATE TABLE geospatial(
location geometry
)
```

```
INSERT INTO geospatial (location)
VALUES
 ('point(34.057163 -118.364126)'),
 ('point(34.057035 -118.364565)'),
 ('point(34.057426 -118.364533)'),
 ('point(34.057062 -118.364129)'),
 ('point(34.057144 -118.363983)'),
 ('point(34.063318 -118.360797)'),
 ('point(34.062129 -118.361624)'),
 ('point(34.063798 -118.355438)'),
 ('point(34.074531 -118.355719)'),
 ('point(34.078048 -118.474077)'),
 ('point(34.019628 -118.288748)'),
 ('point(34.018698 -118.286600)'),
 ('point(34.021723 -118.282784)'),
 ('point(34.019070 -118.276407)'),
 ('point(34.031344 -118.276789)');
 ```
 
 ```
 select ST_AsText(location) from geospatial;
 ```
 
 ```
 SELECT ST_AsText(ST_ConvexHull(
	ST_Collect(location)))
	FROM geospatial;
```

RESULT:

POLYGON((34.078048 -118.474077,34.018698 -118.2866,34.01907 -118.276407,34.031344 -118.276789,34.074531 -118.355719,34.078048 -118.474077))

Then Update spatial.kml file: (Paste this code after line 120)
```
<!-- Convex hull for all 15 points -->
	<Style id="transBluePoly">
      <LineStyle>
        <width>1.5</width>
      </LineStyle>
      <PolyStyle>
        <color>7dff0000</color>
      </PolyStyle>
    </Style>
  	<Placemark>
    <name>Convex Hull</name>
    <styleUrl>#transBluePoly</styleUrl>
    <Polygon>
      <extrude>1</extrude>
      <altitudeMode>relativeToGround</altitudeMode>
      <outerBoundaryIs>
        <LinearRing>
          <coordinates>
          	-118.474077,34.078048,500
  			-118.286600,34.018698,500
  			-118.276407,34.019070,500
   			-118.276789,34.031344,500
   			-118.355719,34.074531,500
   			-118.474077,34.078048,500
          </coordinates>
        </LinearRing>
      </outerBoundaryIs>
    </Polygon>
  </Placemark>
```

Sample:

![convex hull](convex hull.png)


Assignment Link:
http://bytes.usc.edu/cs585/s20_db0ds1ml2agi/hw/HW3/index.html

KML Tutorial Link:
https://developers.google.com/kml/documentation/kml_tut#placemarks

