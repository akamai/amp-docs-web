---
layout: techdocs-web
title: Loading Media
categories: [core]
position: 3
---

Media can be supplied to the player in one of two ways:

1. Set the {@link akamai.amp.Player#media} property of the AMP instance.
```javascript
amp.media = {
	src: "http://projects.mediadev.edgesuite.net/customers/akamai/video/VfE.mp4",
	type: "video/mp4"
};;
```
2. Add a media property to the player's configuration object.
```javascript
var config = {
	media: {
		src: "http://projects.mediadev.edgesuite.net/customers/akamai/video/VfE.mp4",
		type: "video/mp4",
		autoplay: true,
		startTime: 0
	}
};
var amp = akamai.amp.AMP.create("amp", config);
```

In both cases, the object must adhere to the {@link akamai.amp.Media} interface.
To ensure the best playback experience on all devices and platforms it is suggested that multiple stream formats be provided per media item.
This can be done by using the `source` property instead of the `src` and `type` properties:
```javascript
var config = {
	media: {
		title: "VOD Sample",
		poster: '../resources/images/hd_world.jpg',
		source: [{
			src: "http://multiplatform-f.akamaihd.net/z/multi/april11/hdworld/hdworld_,512x288_450_b,640x360_700_b,768x432_1000_b,1024x576_1400_m,1280x720_1900_m,1280x720_2500_m,1280x720_3500_m,.mp4.csmil/manifest.f4m",
			type: "video/f4m"
		}, {
			src: "http://multiplatform-f.akamaihd.net/i/multi/april11/hdworld/hdworld_,512x288_450_b,640x360_700_b,768x432_1000_b,1024x576_1400_m,1280x720_1900_m,1280x720_2500_m,1280x720_3500_m,.mp4.csmil/master.m3u8",
			type: "application/x-mpegURL"
		}]
	}
};
var amp = akamai.amp.AMP.create("amp", config);
```
