# Playgrounds

##Data Representation and Querying Project 2015

###Patrick Griffin

##Introduction

This is a project provides the design and documentation for the dataset "Playground" which is available at [Click here](https://data.gov.ie/dataset/playgrounds-county-galway) this data is based on playgrounds within **Co.Galway.** It provides useful information on:
* Parking
* location
* equipment

Which I think will be very beneficial for the community and others around Co.Galway. 

## About the data
This dataset was received in Comma Separated Values (CSV) format, and was downloaded from [*data.gov.ie*](https://data.gov.ie/dataset/playgrounds-county-galway).
The CSV file contains 63 rows, the first being a header row with the names of each field.
There are 16 values on each line, which are as follows:

Heading | Description  
---------|-----------
"X" | A X gps position. 
"Y" | A Y gps position. 
"FID" | An ID given to each park. 
"OBJECTID" | An ID given to each park. 
"LOCATION" | A Location of each park e.g "Roundstone".
"AREA" | Area of each park e.g "West Galway".
"MANAGED_BY" | Who manages the playgrounds.
"PLAYGROUND" | A more specific location of the playgrounds.
"AGE_GROUP" | The age group of the park.
"List_of_Eq" | List of equipment in the parks eg slide,swings etc.
"Liosta_Tre" | List of equipment in the parks in irish.
"List_of_00" | List of extra equipment for juniors e.g Junior Swing.
"PUBLIC_TOI" | Is there public toilets.
"OPENING_HO" | Opening times for the parks. 
"PARKING" | Is there parking available.
"PHOTO" | A Picture link of the park. 

An example of json format with all information:

```json
{   
        "X": "-1104192",
        "Y": "7056858",
        "FID": "1",
        "ID": "1",
        "Location_o": "Roundstone (Cloch na Ron)",
        "Area_": "West Galway - Conamara",
        "Managed_By": "Roundstone Playground Committee",
        "Playground": "Roundstone Village, Connemara",
        "AGE_GROUP": "0 to 16 Years",
        "List_of_Eq": "Climber and Slide, Climber with Rope, Flat Swings, Cradle Swings, Crazy Goose, Springer, Spring SeeSaw, Platform & Slide",
        "Liosta_Tre": "Dreapadóir le Sleamhnán, Luascán Cothrom,  Luascán Cliabháin , Lingeadan, Maide Corrach, srl.",
        "List_of_00": "Toddler swings",
        "PUBLIC_TOI": "NO",
        "OPENING_HO": "Daylight Hours",
        "PARKING": "YES",
        "PHOTO": "http://www.galway.ie/gis/playgrounds/1.jpg"
}   
```       


###Designing a set of API's URLs that I think would be useful for querying the dataset.
###1 - Parking
I believe Parking availability would be a popular for parents with children and who need to travel, this is appropriate to the audience who seek information on parking.

You can get a list of playgrounds with parking availability using the GET method at the following URL:
*http://playgrounds.ie/parking/[parking]*
where you replace [parking] with either yes or no.
For example, the URL:
*http://playgrounds.ie/parking/yes*
will return a list of playgrounds with parking.
The data will be returned in JSON format, with the following properties for each playground which I believe is necessary for parents to know and also added extra info which I believe that they need:

Heading | Description  
---------|-----------
"PARKING" | Is there parking available.
"LOCATION" | A Location of each park e.g "Roundstone".
"AGE_GROUP" | The age group of the park.
"List_of_Eq" | List of equipment in the parks eg slide,swings etc.
"PUBLIC_TOI" | Is there public toilets.
"OPENING_HO" | Opening times for the parks. 
"PHOTO" | A Picture link of the park.

An example of a response would be *http://playgrounds.ie/parking/yes*:
```json
{   
        "PARKING": "YES",
        "Location_o": "Moylough (Maigh Locha)",
        "AGE_GROUP": "0 to 12 years",
        "List_of_Eq": "Cable Runway, Basket Swing, Cradle Swings,  Toddlers Multiplay and Slide",
        "PUBLIC_TOI": "Yes",
        "OPENING_HO": "Daylight Hours",
        "PHOTO": "http://www.galway.ie/gis/playgrounds/12.jpg"
}   
```       

###2 - Playgrounds around a certain location
I believe that many users would use this API for finding out the location of a local playground in Co.Galway. The target audience would be recently moved in residents or tourists with children.

You can get a list of Playgrounds near you or in a specific area, based on the location (Location_o) using a GET method at the following URL:
*http://playgrounds.ie/location/[Location_o]*

From the URL above, [Location_o] is where the user could enter in the location of where they want to be able to find a playground, Eg: Roundstone. The user would then be provided with a list of playgrounds with relevant data, in or close to that area. 

The data will be returned in JSON format, with the following properties for each Playground:

Heading | Description  
---------|-----------
"LOCATION" | A Location of each park e.g "Roundstone".
"AGE_GROUP" | The age group of the park.
"List_of_Eq" | List of equipment in the parks eg slide,swings etc.
"PUBLIC_TOI" | Is there public toilets.
"OPENING_HO" | Opening times for the parks. 
"PARKING" | Is there parking available.
"PHOTO" | A Picture link of the park.


An example of a response from the URL: *http://playgrounds.ie/location/Roundstone* would be:
```json
{
    "Location_o": "Roundstone (Cloch na Ron)",
    "Playground": "Roundstone Village, Connemara",
    "AGE_GROUP": "0 to 16 Years",
    "List_of_Eq": "[Climber and Slide, Climber with Rope, Flat Swings, Cradle Swings, Crazy Goose, Springer]",
    "Liosta_Tre": "[Dreapadóir le Sleamhnán, Luascán Cothrom,  Luascán Cliabháin , Lingeadan, Maide Corrach]",
    "PUBLIC_TOI": "No",
    "OPENING_HO": "Daylight Hours",
    "PARKING": "YES",
    "PHOTO": "http://www.galway.ie/gis/playgrounds/1.jpg"
}
```

###3 - Playgrounds equipment

It is important to show a playgrounds equiment as some people would like to know what the park contains for example slides,swings etc.

You can get a list of a Playgrounds equipment, based on what equipment the playground contains(List_of_Eq) using a GET method at the following URL:
*http://playgrounds.ie/equipment/[List_of_Eq]*

From the URL above, [List_of_Eq] is where the user could enter in the equipment of what they want, Eg: Springer,. The user would then be provided with a list of playgrounds that have a Springer or other equipment.

The data will be returned in JSON format, with the following properties for each Playground:

Heading | Description  
---------|-----------
"List_of_Eq" | List of equipment in the parks eg slide,swings etc.
"Liosta_Tre" | List of equipment in the parks in irish.
"List_of_00" | List of extra equipment for juniors e.g Junior Swing.
"LOCATION" | A Location of each park e.g "Roundstone".
"AGE_GROUP" | The age group of the park.
"PUBLIC_TOI" | Is there public toilets.
"OPENING_HO" | Opening times for the parks. 
"PARKING" | Is there parking available.
"PHOTO" | A Picture link of the park.

An example of a response from the URL: *http://www.playgrounds.ie/equipment/Springer* would be:
```json
{
    "List_of_Eq": "[Climber and Slide, Climber with Rope, Flat Swings, Cradle Swings, Crazy Goose, Springer]",
    "Liosta_Tre": "[Dreapadóir le Sleamhnán, Luascán Cothrom,  Luascán Cliabháin , Lingeadan, Maide Corrach]",
    "List_of_00": "[List of extra equipment for juniors e.g Junior Swing]",
    "Location_o": "Roundstone (Cloch na Ron)",
    "AGE_GROUP": "0 to 16 Years",
    "PUBLIC_TOI": "No",
    "OPENING_HO": "Daylight Hours",
    "PARKING": "YES",
    "PHOTO": "http://www.galway.ie/gis/playgrounds/1.jpg"
}
```

### Breakdown of each sub part of a sample URL
Here is an example of a breakdown of a link 
 ``` http://www.galway.ie/gis/playgrounds/1.jpg ```

|  URL Section     | Explanation  |
|:----------------:|:--------------------------:|
| http  | Protocol being used |
| www        | SubDomain |
| galway.ie | Domain | 
| /gis/playgrounds/ | Path |  
| 1.jpg | The Search Criteria |


