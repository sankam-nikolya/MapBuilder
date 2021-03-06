MapBuilder class
-------------

ORIGINAL: http://www.phpclasses.org/package/7600-PHP-Display-maps-using-Google-Maps-API-v3.html OR http://www.tozalakyan.com/

Copyright (C) 2012 - 2014 Vagharshak Tozalakyan <vagh@tozalakyan.com>
Released under MIT license (http://opensource.org/licenses/mit-license.php)

MapBuilder class

**Requirements:**
- PHP 5.2 or higher version;
- JSON extension (optional, used for Geocoding only);
- Sockets extension (optional, used for Geocoding only with appropriate fetch mode);
- CURL extension (optional, used for Geocoding only with appropriate fetch mode);
- An active Internet connection to access the Google Maps API.


**DOCUMENTATION**
***********************************************************

1. Overview.
2. Description of Examples.
3. Constants.
4. Methods.
5. The Map Options Array.


1. OVERVIEW. 
-----------------------------------------------------------

This class can be used to generate dynamic maps of different types, sizes, UI control 
sets and to place customizable markers and info windows attached to markers on it.
It uses Google Maps API v3 service to generate Javascript and HTML output to display 
the map in browser's window. It also implements Google Maps Geocoding functionality to 
retrieve longitude and latitude coordinates from human readable address strings.
In the browsers, which support W3C Geolocation API, it can read Geolocation sensor 
(e.g. GPS) data and place a marker and/or set map's center position using that data.


2. DESCRIPTION OF EXAMPLES.
-----------------------------------------------------------

ex1 - Minimal installation.
ex2 - Geocoding, markers, map types, zoom level.
ex3 - Playing with controls.
ex4 - Info windows.
ex5 - Playing with different marker icons.
ex6 - Full screen mode.
ex7 - Using Geolocation service.
ex8 - Filling data from database.
ex9 - Working with map from JavaScript code.
ex10 - Working with polylines.
ex11 - Working with polygons.
ex12 - Using directions service.



3. CONSTANTS.
-----------------------------------------------------------

3.1. Map Types.

MAP_TYPE_ID_HYBRID
MAP_TYPE_ID_ROADMAP 
MAP_TYPE_ID_SATELLITE
MAP_TYPE_ID_TERRAIN

3.2. Control Positions.

CONTROL_POSITION_BOTTOM_CENTER
CONTROL_POSITION_BOTTOM_LEFT 	
CONTROL_POSITION_BOTTOM_RIGHT
CONTROL_POSITION_LEFT_BOTTOM	
CONTROL_POSITION_LEFT_CENTER 
CONTROL_POSITION_LEFT_TOP 
CONTROL_POSITION_RIGHT_BOTTOM 
CONTROL_POSITION_RIGHT_CENTER 
CONTROL_POSITION_RIGHT_TOP 
CONTROL_POSITION_TOP_CENTER 
CONTROL_POSITION_TOP_LEFT 
CONTROL_POSITION_TOP_RIGHT 

3.3. Map Type Control Styles.

MAP_TYPE_CONTROL_STYLE_DEFAULT 
MAP_TYPE_CONTROL_STYLE_DROPDOWN_MENU 
MAP_TYPE_CONTROL_STYLE_HORIZONTAL_BAR 

3.4. Scale Control Styles.

SCALE_CONTROL_STYLE_DEFAULT

3.5. Zoom Control Styles

ZOOM_CONTROL_STYLE_DEFAULT 
ZOOM_CONTROL_STYLE_LARGE 
ZOOM_CONTROL_STYLE_SMALL 

3.6. URL fetch Method For Geocoding.
    
URL_FETCH_METHOD_CURL
URL_FETCH_METHOD_SOCKETS
    
3.7. Marker Animations.
    
ANIMATION_BOUNCE 
ANIMATION_DROP


4. METHODS.
-----------------------------------------------------------

void __construct(string $id = '', string $apiKey = '') 
Object constructor. The first parameter is a unique identifier to be used as ID attribute of map's DIV tag.
If empty string passed as id, then a random identifier will be generated automatically. 
The second parameter is the Google Maps API key.
If empty string passed as apiKey, then no API key will be used. 

void setId(string $id) 
Sets a unique identifier to be used as ID attribute of map's DIV tag.

string getId() 
Returns the value of unique identifier to be used as ID attribute of map's DIV tag.

void setApiKey(string $apiKey)
Sets the Google Maps API key.

string getApiKey()
Returns the Google Maps API key.

void setSize(int $width, int $height) 
Sets the map size in pixels. Ignored when full screen mode is on (see below).

int getWidth()
Returns the map width in pixels.
 
int getHeight() 
Returns the map height in pixels.

void setFullScreen(bool $fullScreen)
Sets the full screen mode (width=100%, height=100%). 

bool getFullScreen()
Returns the recent full screen mode.

void setCenter(float $lat, float $lng)
Sets the location, which will be visible in the center of the map.
Parameters are latitude and longitude of the location.

float getCenterLat()
Returns the center point latitude.
 
float getCenterLng() 
Returns the center point longitude.

void setSensor(bool $sensor) 
Enables GPS sensor.

bool getSensor() 
Returns the recent sensor enabled mode.

void setZoom(int $zoom)
Sets the initial map zoom level.

int getZoom()
Returns the entire zoom level. 

void setMapTypeId(string $mapTypeId)
Defines the default map type.
Possible values are:
MapBuilder::MAP_TYPE_ID_HYBRID
MapBuilder::MAP_TYPE_ID_ROADMAP
MapBuilder::MAP_TYPE_ID_SATELLITE
MapBuilder::MAP_TYPE_ID_TERRAIN
Default map type is HYBRID.

string getMapTypeId()
Returns the entire map type.

array getLatLng(string $address, string $urlFetchMethod = URL_FETCH_METHOD_SOCKETS)
Returns latitude and longitude (an array with "lat" and "lng" keys) from an address string.
Second parameter is fetching method which will be used to access the Google Geocoding API.
Possible methods are: MapBuilder::URL_FETCH_METHOD_SOCKETS and MapBuilder::URL_FETCH_METHOD_CURL.

int addMarker(float $lat, float $lng, array $options = array())
Adds a new marker at position specified by $lat and $lng parameters.
Returns the newly added marker's index in array.
Please refer to the Marker Options Array section for details about the $options array.

mixed getMarkerLat(int $index) 
Returns the marker's latitude value by its index or false if the index is incorrect.

mixed getMarkerLng(int $index) 
Returns the marker's longitude value by its index or false if the index is incorrect.

mixed getMarkerOptions(int $index)
Returns the markers's options array by its index or false if the index is incorrect.
 
int getNumMarkers()
Returns the number of added markers. 

void removeMarker(int $index) 
Removes the marker by its index.

void clearMarkers() 
Removes all added markers.

int addPolyline(array $path, string $color, int $weight, float $opacity)
Add a new polyline by path as an array of [lat, lng] pairs, stroke color, weight and opacity.
Returns the numeric index of added polyline.

int getNumPolylines()
Returns the number of added polylines.

bool removePolyline(int $index)
Removes the polyline by its index.

void clearPolylines() 
Removes all added polylines.

int addPolygon(array $path, string $strokeColor, string $fillColor, int $strokeWeight, float $strokeOpacity, float $fillOpacity)
Add a new polygon by path as an array of [lat, lng] pairs, stroke color, fill color, stroke weight, stroke opacity and fill opacity.
Returns the numeric index of added polygon.

int getNumPolygons()
Returns the number of added polygons.

bool removePolygon(int $index)
Removes the polygon by its index.

void clearPolygons() 
Removes all added polygons.

void addGeoMarker(array $options = array())
Adds a marker to position returned by Geolocation API using GPS sensor.
Geolocation should be supported in browser.

void removeGeoMarker(bool $resetSensor = true) 
Removes the Geolocation marker and resets the sensor flag if parameter is true.

void overrideCenterByGeo(bool $override = true, bool $resetSensor = true)
Overrides the map's center location by Geolocation API position.
If the first parameter is false and the second parameter is true, it will reset the sensor flag. 
Geolocation should be supported in browser.

mixed show(bool $output = true)
Displays the map. When $output is false, the JS/HTML code will be returned as a string instead of beeing outputed directly to the browser.

Other map parameters
Please refer to official Google Maps API documentation for the description of options:
https://developers.google.com/maps/documentation/javascript/reference#MapOptions

void setDisableDefaultUI(bool $disableDefaultUI)
bool getDisableDefaultUI()
void setDisableDoubleClickZoom(bool $disableDoubleClickZoom)
bool getDisableDoubleClickZoom()
void setDraggable(bool $draggable)
bool getDraggable()
void setDraggableCursor(string $draggableCursor)
string getDraggableCursor()
void setDraggingCursor(string $draggingCursor)
string getDraggingCursor()
void setHeading(int $heading)
int getHeading()
void setKeyboardShortcuts(bool $keyboardShortcuts)
bool getKeyboardShortcuts()
void setMapMaker(bool $mapMaker)
bool getMapMaker()
void setMapTypeControl(bool $mapTypeControl)
bool getMapTypeControl()
void setMapTypeControlIds(array $mapTypeControlIds)
array getMapTypeControlIds()
void setMapTypeControlPosition(string $mapTypeControlPosition)
string getMapTypeControlPosition()
void setMapTypeControlStyle(string $mapTypeControlStyle)
string getMapTypeControlStyle()
void setMaxZoom(int $maxZoom)
int getMaxZoom()
void setMinZoom(int $minZoom)
int getMinZoom()
void setNoClear(bool $noClear)
bool getNoClear()
void setOverviewMapControl(bool $overviewMapControl)
bool getOverviewMapControl()
void setOverviewMapControlOpened(bool $overviewMapControlOpened)
bool getOverviewMapControlOpened()
void setPanControl(bool $panControl)
bool getPanControl()
void setPanControlPosition(string $panControlPosition)
string getPanControlPosition()
void setRotateControl(bool $rotateControl)
bool getRotateControl()
void setRotateControlPosition(string $rotateControlPosition)
string getRotateControlPosition()
void setScaleControl(bool $scaleControl)
bool getScaleControl()
void setScaleControlStyle(string $scaleControlStyle)
string getScaleControlStyle()
void setScaleControlPosition(string $scaleControlPosition)
string getScaleControlPosition()
void setScrollwheel(bool $scrollwheel)
bool getScrollwheel()
void setStreetViewControl(bool $streetViewControl)
bool getStreetViewControl()
void setStreetViewControlPosition(string $streetViewControlPosition)
string getStreetViewControlPosition()
void setTilt(int $tilt)
int getTilt()
void setZoomControl(bool $zoomControl)
bool getZoomControl()
void setZoomControlPosition(string $zoomControlPosition)
string getZoomControlPosition()
void setZoomControlStyle(string $zoomControlStyle)
string getZoomControlStyle()


5. THE MARKER OPTIONS ARRAY.
-----------------------------------------------------------

The marker's options array may contain the following keys:

string animation 
Which animation to play when marker is added to a map.
If set, the possible values are:
MapBuilder::ANIMATION_BOUNCE
MapBuilder::ANIMATION_DROP

bool clickable 
If true, the marker receives mouse and touch events. Default value is true.

string cursor 
Mouse cursor to show on hover.

bool draggable
If true, the marker can be dragged. Default value is false.

bool flat 
If true, the marker shadow will not be displayed.

string icon 
Custom icon's URL for the marker.

string defColor
When the custom icon is not set or empty, a default baloon marker could be shown using specified background color. 

string defSymbol 
When the custom icon is not set or empty, a default baloon marker could be shown using specified symbol (e.g. number or letter) in the center. 
        
bool optimized
Optimization renders many markers as a single static element. Optimized rendering is enabled by default. Disable optimized rendering for animated GIFs or PNGs, or when each marker must be rendered as a separate DOM element (advanced usage only).

bool raiseOnDrag 
If false, disables raising and lowering the marker on drag. This option is true by default.

string shadow 
The URL of the shadow image of the marker.
   
string title 
Marker rollover text.

bool visible
If false, the marker will not be visible.
 
int zIndex 
All markers are displayed on the map in order of their zIndex, with higher values displaying in front of markers with lower values. By default, markers are displayed according to their vertical position on screen, with lower markers appearing in front of markers further up the screen.

string html
Content to display in the info window when clicking on the marker. This can be an HTML element, a plain-text string, or a string containing HTML. The InfoWindow will be sized according to the content. To set an explicit size for the content, set content to be a HTML element with that size.
 
int infoMaxWidth 
Maximum width of the info window, regardless of content's width. 

bool infoDisableAutoPan 
Disable auto-pan on open. By default, the info window will pan the map so that it is fully visible when it opens.

int infoZIndex 
All info windows are displayed on the map in order of their zIndex, with higher values displaying in front of info windows with lower values. By default, info winodws are displayed according to their latitude, with info windows of lower latitudes appearing in front of info windows at higher latitudes. Info windows are always displayed in front of markers.

bool infoCloseOthers = false
Close other opened info windows before opening the entire info window.

Note: Almost all values in options array are set to null by default which indicate the corresponding parameters have not been set yet.
