![MapmyIndia APIs](https://www.mapmyindia.com/api/img/mapmyindia-api.png)
# MapmyIndia Geo-Analytics APIs
## (With basemap agnostic GeoAnalytics JS Library)

## Version History

| Version | Last Updated | Author |
| ---- | ---- | ---- |
| 3.1 | 20 May 2019 | MapmyIndia API Team ([NS]())
| 3.0 | 02 April 2019 | MapmyIndia API Team ([NS]())
| 1.0 | 14 Jan 2019 | MapmyIndia API Team ([NS]()) |
| 1.0 | 03 August 2018 | MapmyIndia API Team ([NS]())

### Compatible Web Browsers
1. Google Chrome (Version 67 and above)
2. Mozilla Firefox (Version 60 and above)

### Base Map Agnostic Web Libraries

#### JavaScript Library Name: 
| Version | Name | Revision Remarks | Author 
| ---- | ---- | ---- | ---- | 
| 1.0 | [`geoAnalytics_Global_L.js`](https://github.com/MapmyIndia/mapmyindia-geoanalytics-api-web/blob/master/JS/geoAnalytics_Global_L.js) | Initial Release | [NS]()

#### Accompanying CSS: 
| Version | Name | Revision Remarks | Author 
| ---- | ---- | ---- | ---- | 
| 1.0 | [`geoAnalytics_Global_L.css`](https://github.com/MapmyIndia/mapmyindia-geoanalytics-api-web/blob/master/JS/geoAnalytics_Global_L.css) | Initial Release | [NS]()


## Methods available in GeoAnalytics APIs

### 1. Making Layers
This method takes in a URL of any Map and creates a layer object which would be displayed on the map or would be made a basemap.

#### Method Name
`geoAnalytics.makeLayer`

#### Parameters
1. `url`: The URL of the basemap with format: z/x/y.png
(Slippy Map Tiles)

#### Example
To call MapmyIndia’s basemap:
```css
var map_url  =	‘https://mt3.mapmyindia.com/advancedmaps/v1/<map_key>/still_map/{z}/{x}/{y}.png';
var MapmyIndia_layer =  geoAnalytics.makeLayer(map_url);
```

### 2. Setting View
This method creates the initial view of the map when the map is loaded for the first time or if the browser is refreshed.

#### Method Name
`geoAnalytics.setView`

#### Parameters
1. `Center`: An array of Latitude & Longitude values of the center of the map.
2. `Zoom`: Initial zoom of the map on refreshing the browser.

#### Example
```css
var view = geoAnalytics.setView([29.0588, 76.0856], 8);
```

### 3. Creating a Map object
This method creates a map object which takes the initial view object, layer object, and a target div id on which the map will be displayed.

#### Method Name
`geoAnalytics.Map`

#### Parameters
1. `Target`: The target <div> element id is to be entered here.
2. `Layer`: Layer object created with the method geoAnalytics.makeLayer.
3. `View`: View object created by the method geoAnalytics.setView.

#### Example
```css
var map =  geoAnalytics.Map('map', MapmyIndia_layer, view);
```

### 4. Getting Layers
This method gets the layer specified which is stored in MapmyIndia’s Database and gives a WMS layer as an output with any filters or styles specified by the user. 
Example: `geoAnalytics.getState`, `geoAnalytics.getCity`, `geoAnalytics.getPincode`, etc.

#### Method name
`geoAnalytics.get<LayerName>`

where: 
- LayerName is the [list of layers(APIs) available](#layers).

#### Parameters
Parameters are sent to the APIs as **`geoparams`**
1. `AccessToken` (): These APIs follow OAuth2 based security. To know more how to create your authorization tokens, please use our authorization URL. More details are available [here](https://www.mapmyindia.com/api/advanced-maps/doc/authentication-api.php)
2. `GeoBoundType` (String; Mandatory): The type of geographical extents on which data would be bound, i.e. the parent layer types (India, State, District, Sub District, etc.)
**Note**: To see the list of available parent later types see the appendix [here](https://github.com/MapmyIndia/mapmyindia-geoanalytics-api-web/blob/master/Appendix/geoAnalyticsAPIs_LayerSpecification_V2.0.pdf).
3. `GeoBound` (Array of Strings; Mandatory): The values of the extent depending on the GeoBoundType. (Array of Names)
**Note**: To see the list of available types see the Listing API [here](https://github.com/MapmyIndia/mapmyindia-geoanalytics-api-web/blob/master/listingAPI.md).
4. `Attribute` (String; Optional): The name of Attribute to filter the output, such as population or number of households.
**Note**: To see the list of available parent later types see the appendix [here](https://github.com/MapmyIndia/mapmyindia-geoanalytics-api-web/blob/master/Appendix/geoAnalyticsAPIs_LayerSpecification_V2.0.pdf).
5. `Query` (String; Optional*):  A string containing an operator and a value which would be applied to the attribute filter. Applicable queries include < (Less than) OR > (Greater then) OR <> (Between). 
Example 1: ‘> 10000’ 
Example 2: BETWEEN `value1` AND `value2`
***Note**: `Query` is mandatory if `Attribute` is given.
6. `Style` (Object; Optional): 
	- `Label` (Boolean; Optional*): Value to display labels. Set as true OR false.
	- `LabelColor`(Hex Value; Optional*): Value of the color of label. 
	- `LabelSize`(Number; Optional*): Size of labels to be displayed. 
	- `FillColor`(Hex Value; Optional*): Value of the polygon/point color. 
	- `PointSize`(Number; Optional*): Size of point data.  (Applicable for Point geometry only)
	- `BorderColor`(Hex Value; Optional*): Value of the color of the label. 
	- `BorderWidth`(Number; Optional*): Width of the polygon border. 
	- `Opacity`(Float; Optional*): Opacity value of whole layer. (Any range between 0 & 1)
		***Note**: All starred parameters are mandatory if `Style` is given.

#### Example
```css
var geoParams = 
{
	GeoBoundType	:	'stt_nme',
	GeoBound		:	['haryana'],
	Attribute		:	't_p',
	Query			:	'>10000',
    Style: 
		{
			Label		:	true,
			LabelColor	:	'13592e',
			LabelSize	:	10,
			FillColor	:	'ffe0aa',			  
			BorderColor	:	'13592e',
			BorderWidth	:	2,
			Opacity		:	0.5
        }
};
var GeoDataLayer = geoAnalytics.getPanchayat(geoParams);
map.addLayer(GeoDataLayer);
```

#### <a name="layers"></a>APIs: List of Available Layers
1. getState
2. getDistrict
3. getSubdistrict
4. getTown
5. getCity
6. getPincode
7. getWard
8. getLocality
9. getPanchayat
10. getBlock
11. getVillage

## Layers and Attributes
To get the list of available layer's and attribute's names, please use the Listing API [available here](https://github.com/MapmyIndia/mapmyindia-geoanalytics-api-web/blob/master/listingAPI.md).

## Getting Started

Now that you’re all caught up with the features, let's get down right to them and look at how you can  integrate our Interactive Map JS API in conjunction with the above geoAnalytics methods to add data on that map to your Website from scratch.

### Initializing The Map
Follow the below steps to integrate a base map into your existing code base.

- Declare application as HTML5:
```css
define <!DOCTYPE html> on top of your HTML.
```
- Download the geoAnalytics CSS from here and declare as given below: 
```css
<link rel="stylesheet" href="<path to css>" type="text/css" />
```
- Integrate our GeoAnalytics JS (Leaflet based) into your HTML5 page using script tag.
Example: 
```css
<script src=""></script>
```
- Define a style in the head section to load in your CSS.
```css
<style> html, body, #map {position: absolute;height: 100%;z-index: 0;width:100%;} </style>
```
- Define a div object in the body tag of the HTML where you want the base map to show up.
```css
<div id="map"></div>;
```
- Initialize your chosen map, by declaring your map URL:
```css
var map_url  = ‘https://mt3.mapmyindia.com/advancedmaps/v1/<map_key>/still_map/{z}/{x}/{y}.png';
```
- Next, call new `geoAnalytics.makeLayer` method  in the JavaScript and pass it the `map_url` declared previously.
```css
var MapmyIndia_layer =  geoAnalytics.makeLayer(map_url);
```
- Now, Call new `geoAnalytics.setView` method  in the JavaScript and pass it the `centre` and `zoom` level required for map.
```css
var view = geoAnalytics.setView([29.0588, 76.0856], 8);
```
- Finally, call new `geoAnalytics.map` method  in the JavaScript and pass it the `div` object in which you want the map populated, `MapmyIndia_layer` object and `view` object.
```css
var map =  geoAnalytics.Map('map', MapmyIndia_layer, view);
```
- Load the map.

### Adding Your First DataLayer
To add a `DataLayer` to the map, go through the following steps after declaring the map object:

- First, declare the `DataLayer` object
```css
var geoParams =
{
	GeoBoundType	: 	'stt_nme',
	GeoBound	: 	['haryana'],
	Attribute		:	't_p',
	Query		:	'>10000',
	Style		:	
		{
	        Label	:	 true,
	        LabelColor	: 	'13592e',
	        LabelSize	: 	10,
	        FillColor	: 	'ffe0aa',
			BorderColor	 :	 '13592e',
			BorderWidth  :	 2,
			Opacity	: 	0.5
		}
};
```
- Second, declare the `GeoDataLayer` object by calling new `geoAnalytics.get<layerName>` method in the JavaScript and passing the above created `geoParams` object in it.
```css
var GeoDataLayer = geoAnalytics.getPanchayat(geoParams); // for panchayat layer
```
- Third, Add the `GeoDataLayer` object on the map on the map object created above:
```css
map.addLayer(GeoDataLayer);
```
- Finally, call the MapmyIndia’s Listing APIs to get the bounding box of the `DataLayer` to set the bounds of the map with respect to the `DataLayer` . Refer to the Listing API documentation for more information  (Alternatively call the new `geoAnalytics.setBounds` method in the JavaScript and pass it layer name, `geoParams` and map objects in it to set the bounds of map to the bounding box of `GeoDataLayer`. 
```css
geoAnalytics.setBounds('pincode',geoParams,map); // for pincode layer
```
### Info Windows
Info Windows are a convenient way of showing data about a point in the `DataLayer`. The expected behaviour of a user to know about any point in the `DataLayer` is to try and click on it to know what it is all about. The mechanism to accomplish this is by showing an info window.
The info window for a `DataLayer`(created previously) can be obtained through following steps:
- Create a click event on the map.
```css
map.on('click', function(e) 
{
// e stands for the event in which the click happens
});
```
- Declare the attribute names in propertyName  that you want to see in the info  window.
```css
map.on('click', function(e) 
{
var propertyName = 'stt_nme,stt_id,t_p,t_m,t_f,label';
});
```
- Call a new `geoAnalytics.getFeatureInfo` method in the JavaScript and pass the `event`, `propertyName` and `GeoDataLayer` in it. This will give json response in which all the information for the requested attribute will be available.
```css
map.on('click', function(e) 
{
var propertyName = 'stt_nme,stt_id,t_p,t_m,t_f,label';
var Infodata = geoAnalytics.getFeatureInfo(e,propertyName,GeoDataLayer);
});.
```
- Create a variable html and add the data into it.
```css
map.on('click', function(e) 
{
var propertyName = 'stt_nme,stt_id,t_p,t_m,t_f,label';
var Infodata = geoAnalytics.getFeatureInfo(e,propertyName,GeoDataLayer);
var html = "";
if(Infodata.features[0])
	{
	html += "<div class='mainlabel_details'><label class='label_name'>Town Name:</label> " + Infodata.features[0].properties["twn_nme"] + "</div> ";
	html += "<div class='mainlabel_details'><label class='label_name'>State ID:</label> " + Infodata.features[0].properties["stt_id"] + "</div>";
	html += "<div class='mainlabel_details'><label class='label_name'>State Name:</label> " + Infodata.features[0].properties["stt_nme"] + "</div> ";
    html += "<div class='mainlabel_details'><label class='label_name'>Total Population:</label> " + Infodata.features[0].properties["t_p"] + "</div> ";
    
          	  }
	  else if(Infodata.features[0] == undefined)
	  console.log("Not Exists");
	}
);
```
- Finally, add the info window to the map by creating a leaflet popup.
```css
map.on('click', function(e) 
{
var propertyName = 'stt_nme,stt_id,t_p,t_m,t_f,label';
var Infodata = geoAnalytics.getFeatureInfo(e,propertyName,GeoDataLayer);
var html = "";
if(Infodata.features[0])
	{
	html += "<div class='mainlabel_details'><label class='label_name'>Town Name:</label> " + Infodata.features[0].properties["twn_nme"] + "</div> ";
	html += "<div class='mainlabel_details'><label class='label_name'>State ID:</label> " + Infodata.features[0].properties["stt_id"] + "</div>";
	html += "<div class='mainlabel_details'><label class='label_name'>State Name:</label> " + Infodata.features[0].properties["stt_nme"] + "</div> ";
    html += "<div class='mainlabel_details'><label class='label_name'>Total Population:</label> " + Infodata.features[0].properties["t_p"] + "</div> ";

    L.popup({ maxWidth: 800})
      .setLatLng(e.latlng)
      .setContent(html)
      .addTo(map);
          	  }
	  else if(Infodata.features[0] == undefined)
	  console.log("Not Exists");
	}
);
```

## Examples

### getState (some states with default style)
![getState](https://mmi-api-team.s3.amazonaws.com/geoAnalyticsApiImages/getState.png)

### getState (all states with default style)
![getState](https://mmi-api-team.s3.amazonaws.com/geoAnalyticsApiImages/stateswithDefaultstyling.png)

### getCity(city with default style)

![getCity](https://mmi-api-team.s3.amazonaws.com/geoAnalyticsApiImages/getCity.png)

### getDistrict (all districts of one state with default style)
![getDistrict](https://mmi-api-team.s3.amazonaws.com/geoAnalyticsApiImages/districtswithCustomstyling.png)



For any queries and support, please contact: 

![Email](https://www.google.com/a/cpanel/mapmyindia.co.in/images/logo.gif?service=google_gsuite) 
Email us at [apisupport@mapmyindia.com](mailto:apisupport@mapmyindia.com)

![](https://www.mapmyindia.com/api/img/icons/stack-overflow.png)
[Stack Overflow](https://stackoverflow.com/questions/tagged/mapmyindia-api)
Ask a question under the mapmyindia-api

![](https://www.mapmyindia.com/api/img/icons/support.png)
[Support](https://www.mapmyindia.com/api/index.php#f_cont)
Need support? contact us!

![](https://www.mapmyindia.com/api/img/icons/blog.png)
[Blog](http://www.mapmyindia.com/blog/)
Read about the latest updates & customer stories


> © Copyright 2019. CE Info Systems Pvt. Ltd. All Rights Reserved. | [Terms & Conditions](http://www.mapmyindia.com/api/terms-&-conditions)
>  Written with [StackEdit](https://stackedit.io/) by MapmyIndia.