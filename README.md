#Quickstart goedle.io Custom Tag for Google Tag Manager

* This page describe the goedle.io integration via the [Google Tag Manager](https://developers.google.com/tag-manager/quickstart)
* Create a <a href="https://tagmanager.google.com">GTM Account</a> 
* After creation add a new Account. Fill in your Account name and the container name. The container name should be your website url
* Then go to the tab Admin -> choose your Account and the container you added the step before
* In the container list the link "Install Google Tag Manager" takes you to the GTM Script for your Website
* Go to your website source code and add the whole GTM script immediately after the '<body>' tag
* In the header define the `dataLayer = [];`
* Now you can push the datalayer to GTM
* To call a push, execute `dataLayer.push({datalayer})` in the '<body>' section, at positions where you want to track. (Where the DataLayer object is a JSON Object with values you want to transmit to the GTM)

## Events
The easiest way to track events is to use Built-In-Variables. You can acces the variables in the Tag with `{{BUILT_IN_VARIABLE}}`
For instances, if you want to track clicks, you can simply use the `{{Click ID}}` variable as event. 


##Add the goedle_tag as Custom HTML TAG
Open your project in the Google Tag Manager front end and go to `Container`. Then create a new Custom HTML Tag:

Name: goedle_tag
HTML without user id: 
```javascript
<script type="text/javascript" src="http://d2i4n3axvau3kk.cloudfront.net/goedle.js">
</script>
<script type="text/javascript">
var event = {{CLICK ID}}
var app_key = <YOURAPPKEY>;
var goedle_object = {{goedle}} // optional
goedleHTTPClient.track(app_key, undefined, event, goedle_object);
</script>
```

If you have access to a user id variable in GTM, you can pass it as second argument in the track call.

HTML with user id: 
```javascript
<script type="text/javascript" src="http://d2i4n3axvau3kk.cloudfront.net/goedle.js">
</script>
<script type="text/javascript">
var event = {{CLICK ID}}
var app_key = <YOURAPPKEY>;
var goedle_object = {{goedle}} // optional
goedleHTTPClient.track(app_key, {{userId}}, event, goedle_object);
</script>
```

Insert the goedle.io app-key in the field of 
`var app_key = <YOURAPPKEY>`


##Add Triggers for goedle.io Relevant Actions 
To trigger the correct events, different triggers are needed. In the Google Tag Manager `Container` under `Triggers` you can choose which kind of events you want to track. This can Page Views, Clicks, User Engagement or Custom Events. 

**Adding Triggers:**

After creating the triggers, add them under: `Tags` -> `goedle_tag`  -> choose `Fire On` -> switch to the edit mode an add the Trigger. Afterwards you can publish the goedle TAG. 

### Additional Information with a goedle.io DataLayer Object

If you want to add additional information to the tracking, you can simply create a `goedle` object in your DataLayer and add the following fields. 

**IMPORTANT** The `goedle` object is optional. 

<a name="goedle_object"></a>
```json
    'goedle': {
        'timezone': < utc offset > ,
        'locale': < language > ,
        'device_type': < DeviceTypeIdentifier e.g mobile,desktop > ,
        'user_id': < GA - CLient - ID > ,
        'uuid': < UniqueUserID > ,
        'timestamp': < UnixTimeStamp >
    }
```
`goedle` is on the first layer of the DataLayer object.

Afterwards a push should look like the following code snippet

```javascript
dataLayer.push({
    'goedle': {
        'timezone': < utc offset > ,
        'locale': < language > ,
        'device_type': < DeviceTypeIdentifier e.g mobile,desktop > ,
        'user_id': < GA - CLient - ID > ,
        'uuid': < UniqueUserID > ,
        'timestamp': < UnixTimeStamp >
    }
});
```
