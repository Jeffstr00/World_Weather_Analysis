# WeatherPy with Python APIs

## Overview

At PlanMyTrip, Jack of the user interface team initially asked us to help users find their ideal travel destination and hotel based on user preferences.  When given users' preferred travel temperatures, we used OpenWeather and Google APIs to find locations and hotels which fit their criteria.  While that worked, he has now asked us for further updates: weather descriptions provided for the suggested locations, data filtered based on users' preferred temperatures, and an itinerary created and mapped out for the user.

## Weather Database

This was mostly the same as the previous project, only weather description was added.  We started off by selecting 2000 random latitude/longitude coordinates using `np.random.uniform(low=-90.000, high=90.000, size=2000)`.  A list of cities was then created using `for coordinate in coordinates: city = citipy.nearest_city(coordinate[0], coordinate[1]).city_name`
`if city not in cities: cities.append(city)`.  This left us with an ample sample of 743 cities for potential vacationers to end up at.  Our OpenWeather API request was mostly the same as before but with `city_desc = city_weather["weather"][0]["description"]` added to retrieve a description of each location's current weather.  While a few locations were too remote, we would up with 684 cities and their respective latitude, longitude, current maximum temperature, humidity, cloudiness, wind speed, and current weather conditions.

![City Weather Database](https://github.com/Jeffstr00/World_Weather_Analysis/blob/main/Weather_Database/weather_db.png)

## Vacation Search

Once we had the list of cities and their weather, we were able to match them up with user preferences.  To get those preferences, we asked them using `min_temp = float(input("What is the minimum temperature you would like for your trip? "))` (and likewise for maximum).  We were then able to filter the data to meet their criteria using `preferred_cities_df = city_data_df.loc[(city_data_df["Max Temp"] <= max_temp) & (city_data_df["Max Temp"] >= min_temp)]`.  When creating the Gmaps figure, we were able to dispaly our newly found weather description by adding `<dt>Current Weather</dt><dd>{Current Description} and {Max Temp} °F</dd>` to the info box template.

![Vacation Map](https://github.com/Jeffstr00/World_Weather_Analysis/blob/main/Vacation_Search/WeatherPy_vacation_map.png)

## Vacation Itinerary

Once the users were presented with all of those options, they were able to pick out some hotels which met their preferred criteria.  In our case, they chose four locations in South America's French Guiana.  

![Travel Itinerary Map](https://github.com/Jeffstr00/World_Weather_Analysis/blob/main/Vacation_Itinerary/WeatherPy_travel_map_markers.png)

From here, dataframes were created for each of those locations using `vacation_start = vacation_df.loc[vacation_df.City == "Iracoubo"]`.  Latitude/longitude coordinates were extracted and formed into a list using `start = vacation_start[["Lat","Lng"]].to_numpy()` `start = map(tuple, start)` `start = tuple(start)[0]`.  (The same was also done for stops 1-3 and the ending point, which is the same as the starting point).  We were then able to use those coordinate lists to create a Gmaps directions map by using the following code: `gf_trip = gmaps.directions_layer(start, end, waypoints=[stop1,stop2,stop3], travel_mode='DRIVING')`, which provided us with the following itinerary map:

![Travel Itinerary Map](https://github.com/Jeffstr00/World_Weather_Analysis/blob/main/Vacation_Itinerary/WeatherPy_travel_map.png)
