**Vade Realtime API**
---
The Vade Realtime API provides live parking data that is captured from our network of CCTV cameras and Vade Parksight cameras. 

All endpoints listed below will be added to the following base url:
**`https://realtime.beta.inf.vadenet.org/v1`**

**Authentication**
---
The realtime API requires an apiKey included in the header of your request. 
`apiKey:realtime-xxxxx-xxxxxx-xxxxxxx`

To obtain your key please contact us at team@vadepark.com

**Available Endpoints**
---
- /geo - returns a list of parking spaces and their current occupancy state within a point and radius (best for way-finding)
- /zones - returns parking spaces and their occupancy within a zone defined by Vade or a partner
- /spots - returns information and occupancy of a specific parking space



**`GET` Parking Spots By Latitude and Longitude** 
----
  _returns a list of parking spaces and their current occupancy state within a point and radius (best for way-finding)._

**URL**

	 https://realtime.beta.inf.vadenet.org/v1/geo?pageSize=50&pageNumber=1&latitude=-78.685396&longitude=35.779223&distance=10000


|Parameter| Description |Type| required
|--|--|--|--|
| latitude | latitude of search center |float |yes
| longitude| longitude of search center| float | yes
|distance| search radius (in meters) | int | yes
|pageSize| size of search result list (<=50)| int| yes
|pageNumber | the starting page number of the search | int | yes



**Success Response:**
  
 _A successful response will return a list of parking spaces and their occupancy parameters, check out the example below_

  * **Code:** 200 <br />
    **Content:** 
    ```json
    {
      "spots":[
        {
           "uuid":"a8efdb0d-aj4s-4a9e-8e0c-6b72ff0c585b",
           "zone":"7434aecd-jska-4608-b097-8f0c3bc9e9bc",
           "name":"UC-Davis-ADA-2-8",
           "mdid":"N/A",
           "type":"standard",
           "location":{
              "type":"Point",
              "coordinates":[
                 -121.756550153,
                 38.54262097
              ]
           },
           "lastUpdated":"2021-12a-22T17:50:56Z",
           "occupied":false,
           "rawScore":0,
           "occpuancyThreshold":0.6
        },
        {
           "uuid":"781f649d-82hs-4968-a6b8-f9b6d721f6e7",
           "zone":"f816698f-jska-4d75-ba4a-2ac9636ad688",
           "name":"FDOT_BAKER_EB_4R-Spot-20",
           "mdid":"N/A",
           "type":"curbspace",
           "location":{
              "type":"Point",
              "coordinates":[
                 -82.401195184,
                 30.253478619
              ]
           },
           "lastUpdated":"2021-12-05T21:21:59Z",
           "occupied":true,
           "occpuancyThreshold":0.5,
           "curbspaceVehicleCount":1
        },
      ],
       "query":{
          "latitude":-121.75,
          "longitude":38.54,
          "distance":10000,
          "pageNumber":1,
          "pageSize":1000,
          "self":"/v1/geo?distance=10000&latitude=-121.75&longitude=38.54"
       },
       "numSpots":34,
       "spotsReporting":34,
       "spotsOccupied":5,
       "lastUpdated":"2021-12-05T00:02:34Z"
    }


**`GET` Parking Spots By Zone** 
----
  _returns a list of parking spaces and their current occupancy state within a municipality defined zone._

**URL**


	 https://realtime.beta.inf.vadenet.org/v1/zones/3512668c-540f-41dc-903f-6625dc3362e8


|Parameter| Description |Type| required
|--|--|--|--|
| zone_id | a uuid referencing a municipality defined zone |string |yes


**Success Response:**
  
 _A successful response will return a list of parking spaces and their occupancy parameters, check out the example below_

  * **Code:** 200 <br />
    **Content:** 
    ```json
    {
        "spots": [
            ,
            {
                "uuid": "cb6466c0-fd3f-4de3-926b-3e40c7b25123",
                "zone": "3512668c-540f-41dc-903f-6625dc3362e8",
                "name": "parksight-66-0",
                "mdid": "hillsboro-st/pauge-st:1",
                "location": {
                    "type": "Point",
                    "coordinates": [
                        -78.637428866,
                        35.776427443
                    ]
                },
                "lastUpdated": "2021-05-20T21:42:44.408191Z",
                "occupied": false,
                "rawScore": 0.2862340956795516,
                "occpuancyThreshold": 0.8
            },
        ],
        "query": {
            "latitude": -78.685396,
            "longitude": 35.779223,
            "distance": 10000,
            "pageNumber": 1,
            "pageSize": 50,
            "self": "/v1/geo?distance=10000&latitude=-78.685396&longitude=35.779223&pageNumber=1&pageSize=50"
        },
        "numSpots": 2,
        "spotsReporting": 2,
        "spotsOccupied": 1,
        "lastUpdated": "2021-05-20T21:42:44.408191Z"
    }




**`GET` Individual Parking Spot** 
----
  _returns an individual of parking space and its current occupancy state._

**URL**

	 https://realtime.beta.inf.vadenet.org/v1/spots/7fa8dbcf-e087-4b46-bb5b-18af2577a4cf


|Parameter| Description |Type| required
|--|--|--|--|
| spot_id | a uuid referencing a specific parking space object |string |yes


**Success Response:**
  
 _A successful response will return an individual parking space and its occupancy parameters, check out the example below_

  * **Code:** 200 <br />
    **Content:** 
    ```json
    {   
        "uuid": "7fa8dbcf-e087-4b46-bb5b-18af2577a4cf",
        "zone": "3512668c-540f-41dc-903f-6625dc3362e8",
        "location": {
            "type": "Point",
            "coordinates": [
                -82.918095365,
                40.01498588
            ]
        },
        "mdid": "7",
        "name": "parksight-10-7",
        "occupied": false,
        "rawScore": 0.3412363710685651,
        "occupancyThreshold": 0.8,
        "lastUpdated": "2021-04-14T13:56:01Z",
        "vehicleDetails": {
            "typeOptions": [
                {
                    "type": "sedan",
                    "confidence": 0.8848352432250977
                },
                {
                    "type": "large-sized bus",
                    "confidence": 0.05155378580093384
                },
                {
                    "type": "large truck",
                    "confidence": 0.022109033539891243
                }
            ]
        }
    }
    

**Spot Data Types** 
----
  _We use 2 data structures to represent parking spaces_

- **Standard**

A standard parking space fits the normal description of what most people would consider a parking space - a single stall for a vehicle.

```json
{
   "uuid": str - A unique identifer for the spot in the Vade database,
   "zone": str - A unique identifier for the specific zone this spot is linked to,
   "name": str - The easy to read name of the parking space,
   "mdid": str - A municipality defined identifier,
   "type": str - ("standard") The type of parking space this is 
   "location": dict - A Geojson object to represent the location of this parking space (Point),
   "lastUpdated": str - A UTC timestamp to show when the occupancy of this space was last updated,
   "occupied": bool - Whether or not the parking space is occupied,
   "rawScore": float - the confidence that a vehicle is in the parking space,
   "occpuancyThreshold": float - the minimum confidence level for this space to be considered occupied
}
```

- **Curbspace**

A curbspace parking spot represents a stretch of curb where multiple vehicles are parked. 

```json
{
  "uuid": str - A unique identifer for the spot in the Vade database,
  "zone": str - A unique identifier for the specific zone this spot is linked to,
  "name": str - The easy to read name of the parking space,
  "mdid": str - A municipality defined identifier,
  "type": str - ("curbspace") The type of parking space this is 
  "location": dict - A Geojson object to represent the location of this parking space (Point),
  "lastUpdated": str - A UTC timestamp to show when the occupancy of this space was last updated,
  "occupied": bool - Whether or not the parking space is occupied,
  "occpuancyThreshold": float - A property used by the vade backend,
  "curbspaceVehicleCount": int - How many vehicles are currently parked in this section of curb
}
```


We Have Libraries!
---
**Python: https://pypi.org/project/vade-api/**

    pip install vade-api
