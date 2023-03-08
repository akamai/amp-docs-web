---
layout: techdocs-web
title: Embedding AMP
position: 1
categories: [core]
---

Embedding AMP in a HTML page is a three-step process:

1. Include the AMP JS script
2. Provide embed-time configuration (set the media to play and/or configure any features)
3. Instantiate the AMP object, associating it with a div on the page. The player will take on the size of the div in a responsive manner

```javascript
<html>
	<head>
		<script src="amp.js"></script>
	</head>
	<body>
		<div id="amp"></div>
		<script>
			var config = {
				autoplay: true,
				media: {
					src: "http://projects.mediadev.edgesuite.net/customers/akamai/video/VfE.mp4",
					type: "video/mp4"
				}
			};

			var amp = akamai.amp.AMP.create("amp", config);
		</script>
	</body>
</html>
```
