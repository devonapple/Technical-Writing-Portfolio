
# One Day's Forecast

The list of elements in a day's weather forecast.

|Element|Description|Type|Notes|
|-|-|-|-|
|date|date of forecast|string|format YYYY-MM-DD|
|description|description of weather|string|valid values: sunny, overcast, partly cloudy, raining, and snowing|
|maxTemp|highest temperature forecasted for the day|number|measured in degrees Celsius|
|minTemp|lowest temperature forecasted for the day|number|measured in degrees Celsius|
|windSpeed|average wind speed for the day|number|measured in kilometers per hour|
|danger|assessment of weather's threat potential|Boolean|true if weather conditions are dangerous; otherwise, false|



# Multiple-day Forecast

The list of elements in a weather forecast, in a particular location, over one or more days.

|Element|Description|Type|Notes|
|-|-|-|-|
|longitude|longitude for the location of the current weather forecast|string|two decimal places|
|latitude|latitude for the location of the current forecast|string|two decimal places|
|forecast|array of one or more days of weather forecasts|array|
|&nbsp;&nbsp;date|date of forecast|string|format YYYY-MM-DD|
|&nbsp;&nbsp;description|short description of forecast for the day|string|"sunny", "overcast", "partly cloudy", "raining", and "snowing"|
|&nbsp;&nbsp;maxTemp|highest temperature forecast for the day|integer|degrees Celsius|
|&nbsp;&nbsp;minTemp|lowest temperature forecast for the day|integer|degrees Celsius|
|&nbsp;&nbsp;windSpeed|average wind speed forecast for the day|integer|kilometers per hour|
|&nbsp;&nbsp;danger|assessment of weather's threat potential|Boolean
