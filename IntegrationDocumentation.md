_Note_: You will need an AdMob publisher id. If you do not have an AdMob publisher id, please create a site of type Mobile Web on http://www.admob.com.

  * Include admob.js in your sources.json file, in the following example I've placed admob.js in a directory called app/utils/. Also there is no scene attached so AdMob.ad interface is available from anywhere in my app.
```
  [
      {"source": "app\/assistants\/stage-assistant.js"},
      {"source": "app\/utils\/admob.js"},
    {
        "scenes": "main",
        "source": "app\/assistants\/main-assistant.js"
      }
  ]
```
  * In your main scene first initialize AdMob with:
```
  AdMob.ad.initialize({
  		pub_id: 'YourPubId', // your publisher id
  		bg_color: '#ccc', // optional background color, defaults to #fff
  		text_color: '#333', // optional background color, defaults to #000
  		test_mode: true // optional, set to true for testing ads, remove or set to false for production
  });
```
  * **_Note_** you can change the parameters of the current AdMob instance by calling this function again eg.
```
  AdMob.ad.initialize({
  		pub_id: 'YourPubId-bottom-ad-position', // your publisher id for bottom ad position
  		bg_color: '#ccc', // optional background color, defaults to #fff
  		text_color: '#333' // optional background color, defaults to #000
  });
```
  * To request the ad call AdMob.ad.request. In the following example I've placed a `<div id='admob_id'></div>` somewhere in the scene's .html.
```
  	AdMob.ad.request({
  		onSuccess: (function (ad) { // successful ad call, parameter 'ad' is the html markup for the ad
 			this.controller.get('admob_ad').insert(ad); // place mark up in the the previously declared div
  		}).bind(this),
  		onFailure: (function () { // no ad was returned or call was unsuccessful
 			// do nothing? 
  		}).bind(this),
    
  	});
```
  * Anytime you want a new ad, call AdMob.ad.request again. '''Only request ads that you intend to show''' or your site's revenue potential will be severely impacted.