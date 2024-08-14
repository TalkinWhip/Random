### Create a rest template
1. Create a new BPMN Diagram
2. Add a service task and set it as a REST Connector
3. Use `https://api.openweathermap.org/data/2.5/weather` as URL with GET as Method
4. Use the follwing as Query Parameters
```java
{ 
    q: location,
    appid: "97d11ad6685bf5d608de3cc4fb00acf6",
    units: "metric",
    lang: language
}
```
5. Use the following as a Result experession
```java
{
    temperatur: response.body.main.temp,
    gefuehlteTemperatur: response.body.main.feels_like,
    wetter: response.body.weather[1].main
}
```
6. Test Connector in Play mode and if it works, switch back to Implement and click on the "Save as" button in the top right corner of the Connector Properties. Name the connector "My Open Weather Map Connector" and click on the "View Connector Template" link at the bottom of the screen.

### Customize Connector Template
1. In the connector editor view (JSON), scroll down to properties and then to the property with `"id": "authentication.type"`. Replace the `"type": "Dropdown"` with `"type": "Hidden"`
2. Scroll down (a lot further) and do the same for `"id": "method"`. Notice that the default value is "GET", as we defined it in the process. This is sufficient. Remove the list of "choices"
3. Set `"id": "url"`'s type to "Hidden" as well. An error is thrown because we have `"feel": "optional"`, remove this line and the error should disappear.
4. Hide `"id": "headers"`, `"id": "queryParameters"`, `"id": "connectionTimeoutInSeconds"` , `"id": "readTimeoutInSeconds"`, `"id": "resultVariable"`, `"id": "resultExpression"`, `"id": "errorExpression"`, `"id": "retryCount"`, `"id": "retryBackoff"` and remove the "feel" parameter on each.
5. Scroll back to the top of the properties list and add 2 new properties for language and location:
```java
{
    "label": "Location",
    "description": "Your City (e.g. Berlin)",
    "group": "endpoint",
    "optional": false,
    "type": "String",
    "feel": "optional",
    "value": "",
    "binding": {
        "type": "zeebe:input",
        "name": "location"
        }
},
{
    "label": "Language",
    "group": "endpoint",
    "type": "Dropdown",
    "optional": false,
    "value": "en",
    "choices": [
        {
        "name": "English",
        "value": "en"
        },
        {
        "name": "Deutsch",
        "value": "de"
        },
        {
        "name": "Français",
        "value": "fr"
        }
    ],
    "binding": {
    "type": "zeebe:input",
    "name": "language"
    }
},
```
6. Rename the group "HTTP endpoint" to something that fits.
7. (optional) Add an icon to your connector. Consider using an icon from https://github.com/amedia/meteo-icons/tree/master?tab=readme-ov-file or use your own SVG
8. Publish your connector
9. Go back to your bpmn, replace the REST connector with your custom connector and test it with Play (either by hard-coding a city or by using a variable)