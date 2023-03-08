---
layout: techdocs-web
title: Creating an instance of AMP
categories: [core]
position: 2
---

To create an instance of amp, use the function {@link akamai.amp.AMP.create}. You must pass the function an HTML DOM element or a valid CSS selector to a DOM element:
```javascript
var amp = akamai.amp.AMP.create("#amp");
```

Optionally you can pass a configuration object to function to set the player's default settings:

```javascript
var config = {
	media: {
		src: "http://projects.mediadev.edgesuite.net/customers/akamai/video/VfE.mp4",
		type: "video/mp4",
		autoplay: true
	}
};
var amp = akamai.amp.AMP.create("amp", config);
```

Sometimes it is necessary to run additional code to set up the player. To ensure this code is run after the player if fully initialized, pass a function as the third argument:

```javascript
var config = {
	media: {
		src: "http://projects.mediadev.edgesuite.net/customers/akamai/video/VfE.mp4",
		type: "video/mp4",
		autoplay: true
	}
};
var amp = akamai.amp.AMP.create("amp", config, function (event) {
	console.log(event);
});
```