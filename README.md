**Vade Realtime API**
---
The Vade Realtime API provides live parking data that is captured from our network of CCTV cameras and Vade Parksight cameras. 

All endpoints listed below will be added to the following base url:
**`https://realtime.beta.inf.vadenet.org/v1`**

**Authentication**
---
The realtime API requires an apiKey included in the header of your response. 
`apiKey:realtime-xxxxx-xxxxxx-xxxxxxx`

To obtain your key please contact us at team@vadepark.com

**Available Endpoints**
---
- /geo - returns a list of parking spaces and their current occupancy state within a point and radius (best for way-finding)
- /zones - returns parking spaces and their occupancy within a zone defined by Vade or a partner
- /spots - returns information and occupancy of a specific parking space



**`GET` Query By Latitude and Longitude** 
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
    **Content:** ```{ id : 12 }```
 
* **Error Response:**

  <_Most endpoints will have many ways they can fail. From unauthorized access, to wrongful parameters etc. All of those should be liste d here. It might seem repetitive, but it helps prevent assumptions from being made where they should be._>

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `{ error : "Log in" }`

  OR

  * **Code:** 422 UNPROCESSABLE ENTRY <br />
    **Content:** `{ error : "Email Invalid" }`

* **Sample Call:**

  <_Just a sample call to your endpoint in a runnable format ($.ajax call or a curl request) - this makes life easier and more predictable._> 

* **Notes:**

  <_This is where all uncertainties, commentary, discussion etc. can go. I recommend timestamping and identifying oneself when leaving comments here._>
