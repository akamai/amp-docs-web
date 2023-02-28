---
layout: techdocs-web
title: Loading remote configurations
categories: [core]
position: 8
---

There are some scenarios where there is a need to load a player configuration from a remote location. Here are a few methods to achieve this goal:

1. Load the configuration client side using XMLHttpRequest:
	- config.json:
	<pre class="prettyprint">
	{"autoplay":true}
	</pre>
	- html page:
	<pre class="prettyprint">
	var xhr = new XMLHttpRequest();
	xhr.open("GET", "config.json");
	xhr.onload = function (event) {
		var config = JSON.parse(xhr.responseText);
		// override page specific values
		config.media = {
			src: "http://projects.mediadev.edgesuite.net/customers/akamai/video/VfE.mp4",
			type: "video/mp4"
		};
		var amp = akamai.amp.AMP.create("amp", config);
	};
	xhr.onerror = function (event) {
		console.log("Could not load player config", event.error);
	};
	</pre>
	- Using AMP's Promise based request functionality:
	<pre class="prettyprint">
	akamai.amp.AMP.requestJson("config.json")
		.then(function (config) {
			// override page specific values
			config.media = {
				src: "http://projects.mediadev.edgesuite.net/customers/akamai/video/VfE.mp4",
				type: "video/mp4"
			};
			var amp = akamai.amp.AMP.create("amp", config);
		})
		.catch(function (error) {
			console.log("Could not load player config", event.error);
		});
	</pre>
2. Load the configuration client side using JSONP:  
	- config.json:
	<pre class="prettyprint">
	jsonp({autoplay:true});
	</pre>
	- html page:
	<pre class="prettyprint">
	&lt;script>
	function jsonp(config) {
		// override page specific values
		config.media = {
			src: "http://projects.mediadev.edgesuite.net/customers/akamai/video/VfE.mp4",
			type: "video/mp4"
		};
		var amp = akamai.amp.AMP.create("amp", config);
	}
	&lt;/script>
	&lt;script src="config.js">&lt;/script>
	</pre>
3. Embed the configuration statically in the page using server side script:
	- config.json:
	<pre class="prettyprint">
	{"autoplay":true}
	</pre>
	- html page:
	<pre class="prettyprint">
	var config = &lt;?php include("config.json"); ?>;
	// override page specific values
	config.media = {
		src: "http://projects.mediadev.edgesuite.net/customers/akamai/video/VfE.mp4",
		type: "video/mp4"
	};
	var amp = akamai.amp.AMP.create("amp", config);
	</pre>
