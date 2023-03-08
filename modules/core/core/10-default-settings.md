---
layout: techdocs-web
title: Settings defaults
categories: [core]
position: 10
---

The default value of the player's user settings can be set via the configuration object:

```javascript
var config = {
	settings: {
		defaults: {
			captions: {
				visible: true,
				fontFamily: "monospacedSerif",
				fontSize: "large",
				fontColor: "white",
				fontOpacity: "100%",
				edgeType: "rightShadow",
				edgeColor: "black",
				edgeOpacity: "50%"
				backgroundColor: "black",
				backgroundOpacity: "50%",
				windowColor: "black",
				windowOpacity: "50%",
				scroll: "popout"
			}
		}
	}
};
```
