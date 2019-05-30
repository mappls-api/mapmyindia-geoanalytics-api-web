![MapmyIndia APIs](https://www.mapmyindia.com/api/img/mapmyindia-api.png)
# MapmyIndia Geo-Analytics Listing API
## (For use exclusively with MapmyIndia Geo-Analytics Core APIs)

## Version History

| Version | Last Updated | Author |
| ---- | ---- | ---- |
| 2.0 | 20 May 2019 | MapmyIndia API Team ([NS]())
| 1.0 | 21 January 2019 | MapmyIndia API Team ([NS]())


## Introduction
Geo-Analytics API is an API set that gives the users the power to display & style the data which is archived in MapmyIndia’s pan-India database and overlay it either  on MapmyIndia’s Maps service for web or on any user created maps.
Listing API is an API that gives the users information on the different layers & attributes available within Geo-Analytics Core APIs. This API acts as an assisting API to quickly get the necessary details that are required to accurately fetch the required overlays from the core Geo-Analytics APIs.
Listing API is an API that provide list of attributes along with unique ID. User can get bounding box of the required feature/area as well.

### About This Release
This is the first production release of this API which contains the basic definitions, usages, parameters, and other information regarding the API. Further releases would add more functions and modifications.

### Annexure
The complete list of attributes per layer as available within our APIs is [available here](https://mmi-api-team.s3.ap-south-1.amazonaws.com/geoAnalyticsApiImages/geoAnalyticsAPIs_LayerSpecification_V2.0.pdf). 

## API URL

https://geoanalytics.mapmyindia.com/listingapi?

## Security Type
This APIs follow OAuth2 based security. To know more on how to create your authorization tokens, please use our authorization token URL. More details available [here](https://www.mapmyindia.com/api/advanced-maps/doc/authentication-api.php)

## Request Method
GET

## Request Parameters

1.	`Parent-type Based`: (Mandatory - If addr is not given)
	-	`geo_bound_type`(Mandatory):  Single valued parent type, for example: stt_nme, dst_nme, sdb_nme etc.
		For parent type refer [here](https://github.com/MapmyIndia/mapmyindia-geoanalytics-api-web/blob/master/Appendix/geoAnalyticsAPIs_LayerSpecification_V2.0.pdf).
	-	`geo_bound`(Mandatory): child values, for example: Haryana, Maharashtra, Goa etc
2.	`Address Based` (Mandatory - If geo_bound_type & geo_bound are not given)
	-	`addr` (string) : comma separated address with each parent value. (For eg. lucknow city details addr will be lucknow,uttar Pradesh)
		For parent type refer [here](https://github.com/MapmyIndia/mapmyindia-geoanalytics-api-web/blob/master/Appendix/geoAnalyticsAPIs_LayerSpecification_V2.0.pdf).
3.	`api`(Mandatory): api layer name (such as state, district, subdistrict, village, pincode etc)
4.	`get_attr`(Mandatory): field name/Bounding Box  requested w.r.t api (api) & parent type (geo_bound_type).
Bounding box can be requested as "b_box" variable.

## Request Headers

The API leverages OAuth 2.0 based security. Hence, the developer would need to send a request for access token using their client_id and client_secret to the OAuth API. Once validated from the OAuth API, the access_token and the token_type need to be sent as Authorization header with the value: “{token_type} {access_token}”.

-  `Authorization:  “token_type access_token”`.

## Response Type
JSON

## Response Parameters

1.	`responseCode` (int): The response code of the operation. The 400 series is for client side (application end) error while 500 series is for server side (MapmyIndia) error, 200 series is for success.
2.	`version` (string): The version of the API you’re connected to.
3.	`total_feature_count` (number): total  number of features in the request.
4.	`results` (object):
	-  `api_name` (string): as requested
	- `attribute` (string): as requested
	- `get_attr_values` (object): 
		- `geo_bound` (string)): child value
		- `get_attr_values` (array of strings): list of names/b_box requested


## Examples

### Sample Input 1

```css
https://geoanalytics.mapmyindia.com/listingapi?api=state&geo_bound_type=india&geo_bound=india&get_attr=stt_nme
```

### Sample Output 1
```css
{
	"responseCode": 200, 
	"version": "1.0.0", 
	"total_feature_count": 36, 
	"results": 
		{
			"api_name": "state", 
			"attribute": "stt_nme", 
			"get_attr_values": [
				{
					"geo_bound": "India",
					"get_attr_values": [
						 {
							"stt_nme": "ANDAMAN & NICOBAR ISLANDS"
						  }, 
						  {
						   "stt_nme": "ANDHRA PRADESH" 
						  },
						  {
					       "stt_nme": "ARUNACHAL PRADESH"
						  }, 
						  {
					       "stt_nme": "ASSAM" 
						  },
						  {
						   "stt_nme": "BIHAR"
						  },
						  {  
						   "stt_nme": "CHANDIGARH"
						  }, 
						  {
						   "stt_nme": "CHHATTISGARH"
					      },
						  {  
						   "stt_nme": "DADRA & NAGAR HAVELI"
						  }, 
						  {
					   	   "stt_nme": "DAMAN & DIU"
					      },
					      {  
					        "stt_nme": "DELHI"
					      },
					      {
					        "stt_nme": "GOA" 
					      },
					      {  
					        "stt_nme": "GUJARAT"
                          },
                          {
                            "stt_nme": "HARYANA" 
                          },
                          {  
                            "stt_nme": "HIMACHAL PRADESH"
                          },
                          {
                            "stt_nme": "JAMMU & KASHMIR"
                          },
                          {  
                            "stt_nme": "JHARKHAND"
                          }, 
                          {
                            "stt_nme": "KARNATAKA" 
                          },
                          {  
                            "stt_nme": "KERALA"
                          }, 
                          {
                            "stt_nme": "LAKSHADWEEP"
                          },
                          {  
                            "stt_nme": "MADHYA PRADESH"
                          },
                          {
                            "stt_nme": "MAHARASHTRA" 
                          },
                          {  
                            "stt_nme": "MANIPUR"
                          },
                          {
                            "stt_nme": "MEGHALAYA"
                          },
                          {  
                            "stt_nme": "MIZORAM"
                          }, 
                          {
                            "stt_nme": "NAGALAND"
                          },
                          {  
                            "stt_nme": "ODISHA"
                          },
                          {
                            "stt_nme": "PUDUCHERRY"
                          },
                          {  
                            "stt_nme": "PUNJAB"
                          },
                          {
                            "stt_nme": "RAJASTHAN" 
                          },
                          {  
                            "stt_nme": "SIKKIM"
                          }, 
                          {
                            "stt_nme": "TAMIL NADU"
                          },
                          { 
                            "stt_nme": "TELANGANA"
                          },
                          {
                            "stt_nme": "TRIPURA"
                          },
                          {  
                            "stt_nme": "UTTAR PRADESH" 
                          },
                          {
                            "stt_nme": "UTTARAKHAND"
                          },
                          {  
                            "stt_nme": "WEST BENGAL"
                           } 
                         ]
                       } 
                     ]
                   } 
                 }
```
### Sample Input 2

```css
https://geoanalytics.mapmyindia.com/listingapi?api=district&get_attr=dst_id,dst_nme,stt_nme,stt_id,b_box&addr=jhansi,uttar pradesh
```

### Sample Output 2
```css
{
         "responseCode": 200,
         "version": "1.0.0", 
         "total_feature_count": 1, 
         "results": {
           "api_name": "district",  
           "attribute": "dst_id,dst_nme,stt_nme,stt_id,b_box",             
           "get_attr_values": [
             {  
               "geo_bound": "JHANSI,UTTAR PRADESH", 
               "get_attr_values": [
                 {  
                   "dst_id": "09166",  
                   "dst_nme": "JHANSI",  
                   "stt_nme": "UTTAR PRADESH",  
                   "stt_id": "09",  
                   "b_box": "BOX(78.300549 25.107214,79.419441 25.952543)"
                    }
                  ]
                } 
              ]
            }
          } 
```

### Sample Input 3

```css
https://geoanalytics.mapmyindia.com/listingapi?api=district&get_attr=dst_id,dst_nme,stt_nme,stt_id,b_box&addr=meerut,uttar pradesh
```

### Sample Output 3
```css
{
      "responseCode": 200,
      "version": "1.0.0",
      "total_feature_count": 1, 
      "results": {
        "api_name": "district",  
        "attribute": "dst_id,dst_nme,stt_nme,stt_id,b_box",
        "get_attr_values": [
          {  
            "geo_bound": "MEERUT", 
            "get_attr_values": [
              {  
                "dst_id": "09138",  
                "dst_nme": "MEERUT",  
                "stt_nme": "UTTAR PRADESH",  
                "stt_id": "09",  
                "b_box": "BOX(77.424514 28.762287,78.123699 29.266268)"
               }
             ]
           }
         ]
       }
     } 
```

### Sample Input 4

```css
https://geoanalytics.mapmyindia.com/listingapi?api=district&geo_bound_type=stt_nme&geo_bound=goa&get_attr=dst_id,dst_nme,stt_nme,stt_id,b_box
```

### Sample Output 4
```css
{
 "responseCode": 200,
 "version": "1.0.0",
 "total_feature_count": 2, 
 "results": {
     "api_name": "district",  
     "attribute": "dst_id,dst_nme,stt_nme,stt_id,b_box", 
     "get_attr_values": [
        {  
            "geo_bound": "GOA", 
            "get_attr_values": [
                 {  
                  "dst_id": "30585",  
                  "dst_nme": "NORTH GOA",  
                  "stt_nme": "GOA",  
                  "stt_id": "30",  
                  "b_box": "BOX(73.674383 15.270055,74.292064 15.801544)"
              },
              {
				"dst_id": "30586",  
				"dst_nme": "SOUTH GOA",  
				"stt_nme": "GOA",  
				"stt_id": "30",  
				"b_box": "BOX(73.761123 14.89943,74.343828 15.492524)"
				   }
		         ]
		      }
	       ]
        }
     } 
```

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