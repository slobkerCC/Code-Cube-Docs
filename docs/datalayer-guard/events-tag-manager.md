# Configure events via Google Tag Manager

The DataLayer Guard normally scrapes your website to retrieve all relevant dataLayer events. But for some events this is not possible. Therefore we developed this fallback method which can be implemented via for example Google Tag Manager.

For example usefull for the following interactions:
- Purchases
- Logging in
- Creating a new account
- Saving or removing favourites when logged in

## Implementation in Google Tag Manager

### 1. Create a new tag 

1. Add a new custom HTML tag to the container
    1. Give this tag a name, for example 'Code Cube - DataLayer Guard'
2. Add the script below in the empty HTML tag

```html
<script>
var data = JSON.stringify({
  "client_name": "dataset_name",
  "url": {{Page URL}},
  "timestamp": Date.now(),
  "dataLayer": {{JS - dataLayer}}
});

var xhr = new XMLHttpRequest();

xhr.addEventListener("readystatechange", function() {
  if(this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("POST", "endpoint-url");
xhr.setRequestHeader("Content-Type", "application/json");

xhr.send(data);
</script> 

```
3. There are a couple of variables that you do need to add configure.
    1. **"client_name"**: Can be found in the [configuration page](https://portal.code-cube.io/datalayer_guard_config)
    2. **url**: Make sure that you have the built-in variabele "Page URL" enabled in your container
    3. **dataLayer**: Create a new custom javaScript variabele in your tag container
        1. Give the variabele the name 'JS - dataLayer'
        2. Add the script below in the custom javaScript variabele
    4. **endpoint-url** : This is the URL of our service endpoint and will be shared with you privately.
<pre><code class="language-javascript">
function(){
var dataLayer = JSON.stringify(window.dataLayer)
return dataLayer;
 }

 </code></pre>

### 2. Add the trigger to the tag
1. Add the custom event trigger to the tag based on the dataLayer event name.
2. Firing the dataLayer monitor for 10% of the events is mostly enough.
    1. Add the following rule: Random number ends with 1

### 3. Test your changes in the preview mode and publish
Most important is to make sure the variabele {{JS - dataLayer}} contains the right dataLayer object that you would like to monitor.
