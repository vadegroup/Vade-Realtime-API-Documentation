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
        "spots": [
            {
                "uuid": "9950f9dc-8a0e-41c6-93da-68189a2e727f",
                "zone": "N/A",
                "name": "parksight-60-spot-3",
                "mdid": "N/A",
                "location": {
                    "type": "Point",
                    "coordinates": [
                        -78.637818729,
                        35.778177839
                    ]
                },
                "timeUpdated": "2021-05-20T21:39:59.531676Z",
                "occupied": true,
                "rawScore": 0.9609332672620956,
                "occpuancyThreshold": 0.8
            },
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
                "timeUpdated": "2021-05-20T21:42:44.408191Z",
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
            {
                "uuid": "9950f9dc-8a0e-41c6-93da-68189a2e727f",
                "zone": "N/A",
                "name": "parksight-60-spot-3",
                "mdid": "N/A",
                "location": {
                    "type": "Point",
                    "coordinates": [
                        -78.637818729,
                        35.778177839
                    ]
                },
                "timeUpdated": "2021-05-20T21:39:59.531676Z",
                "occupied": true,
                "rawScore": 0.9609332672620956,
                "occpuancyThreshold": 0.8
            },
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
                "timeUpdated": "2021-05-20T21:42:44.408191Z",
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
        "timeUpdated": "2021-04-14T13:56:01Z",
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

We Have Libraries!
---
**Python: https://pypi.org/project/vade-api/**

    pip install vade-api
