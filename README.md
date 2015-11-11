# Playgrounds

##Data Representation and Querying Project 2015

###Patrick Griffin

##Introduction

This is a project provides the design and documentation for the dataset "Playground" which is available at [Click here](https://data.gov.ie/dataset/playgrounds-county-galway) this data is based on playgrounds within **Co.Galway.** It provides useful information on:
* Location
* Equipment
* Parking

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

###Designing a set of API's URLs that I think would be useful for querying the dataset.
###1 - Parking
I believe Parking availability would be a popular for parents with children and who need to travel.

You can get a list of playgrounds with parking availability using the GET method at the following URL:
*http://playgrounds.ie/parking/[parking]*
where you replace [parking] with either yes or no.
For example, the URL:
*http://playgrounds.ie/parking/[yes]*
will return a list of playgrounds with parking.
The data will be returned in JSON format, with the following properties for each playground which I believe is necessary for parents to know and also added extra info which I believe that they need:

Heading | Description  
---------|-----------
"LOCATION" | A Location of each park e.g "Roundstone".
"AGE_GROUP" | The age group of the park.
"List_of_Eq" | List of equipment in the parks eg slide,swings etc.
"PUBLIC_TOI" | Is there public toilets.
"OPENING_HO" | Opening times for the parks. 
"PARKING" | Is there parking available.
"PHOTO" | A Picture link of the park.

An example of a response would be *http://playgrounds.ie/parking/[yes]*:
   
    ```json     
     {   
        "Location_o": "Moylough (Maigh Locha)",
        "AGE_GROUP": "0 to 12 years",
        "List_of_Eq": "Cable Runway, Basket Swing, Cradle Swings,  Toddlers Multiplay and Slide",
        "PUBLIC_TOI": "Yes",
        "OPENING_HO": "Daylight Hours",
        "PARKING": "YES",
        "PHOTO": "http://www.galway.ie/gis/playgrounds/12.jpg"
    }    
    ```       



