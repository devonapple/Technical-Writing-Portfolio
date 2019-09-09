
# One Day's Forecast
The list of elements in a day's weather forecast.
|Element|Description|Type|Notes|
|-|-|-|-|-|
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
|&nbsp;date|date of forecast|string|format YYYY-MM-DD|
|&nbsp;description|short description of forecast for the day|string|"sunny", "overcast", "partly cloudy", "raining", and "snowing"|
|&nbsp;maxTemp|highest temperature forecast for the day|integer|degrees Celsius|
|&nbsp;minTemp|lowest temperature forecast for the day|integer|degrees Celsius|
|&nbsp;windSpeed|average wind speed forecast for the day|integer|kilometers per hour|
|&nbsp;danger|assessment of weather's threat potential|Boolean


# Meeting Request
The list of elements in a new meeting request for an online calendar.
|Element|Description|Type|Required|Notes|
|-|-|-|-|-|
|meeting|top level; list of details for a new meeting request|meeting data objects|required|
|&nbsp;time|start time of new meeting requested|string|required|format YYYY-MM-DD HH:MM; Timezone is Greenwich Mean Time|
|&nbsp;duration|length of new meeting requested|number|required|measured in minutes|
|&nbsp;description|title of new meeting requested|string|required|
|&nbsp;location|location of new meeting requested|number|optional|default is "" 
|&nbsp;reminder|amount of time specified for a reminder|number|optional|measured in minutes; default is 10 minutes|
|&nbsp;invitees|list of meeting guests|array of string|optional|invitees are referred to by strings which correspond to valid email addresses; default is ""|
