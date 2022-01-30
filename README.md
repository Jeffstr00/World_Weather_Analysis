# WeatherPy with Python APIs

## Overview

At PlanMyTrip, Jack of the user interface team initially asked us to help users find their ideal travel destination and hotel based on user preferences.  When given users' preferred travel temperatures, we used OpenWeather and Google APIs to find locations and hotels which fit their criteria.  While that worked, he has now asked us for further updates: weather descriptions provided for the suggested locations, data filtered based on users' preferred temperatures, and an itinerary created and mapped out for the user.

## Weather Database

This was mostly the same as the previous project, only weather description was added.  We started off by selecting 2000 random latitude/longitude coordinates using `np.random.uniform(low=-90.000, high=90.000, size=2000)`.  A list of cities was then created using `for coordinate in coordinates: city = citipy.nearest_city(coordinate[0], coordinate[1]).city_name`
`if city not in cities: cities.append(city)`.  This left us with an ample sample of 743 cities for potential vacationers to end up at.  Our OpenWeather API request was mostly the same as before but with `city_desc = city_weather["weather"][0]["description"]` added to retrieve a description of each location's current weather.  While a few locations were too remote, we would up with 684 cities and their respective latitude, longitude, current maximum temperature, humidity, cloudiness, wind speed, and current weather conditions.

![City Weather Database](https://github.com/Jeffstr00/World_Weather_Analysis/blob/main/Weather_Database/weather_db.png)

## Vacation Search

## Vacation Itinerary
