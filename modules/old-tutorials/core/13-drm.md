---
layout: techdocs-web
title: Digital Rights Management (DRM)
categories: [core]
position: 13
---

This tutorial shows how to properly configure DRM when using AMP.

1. Supported Providers.
2. Adding a Key.
3. Using Multiple Keys.
4. Using Multiple Sources.
5. Custom Request Headers.
6. Using Custom Fairplay Handlers
<br>
<br>

#### 1. Supported Providers

AMP supports DRM content from the following providers:
- Widevine
- PlayReady
- FairPlay
<br>

#### 2. Adding a Key

To enable DRM content in the player is required to provide both the source and a key for the source as shown in the following example:

```javascript
var config = {
	media : {
		src: "https://willzhanmswest.streaming.mediaservices.windows.net/609f4f57-1e5b-4898-90b1-81c574b2e8e3/VfE.ism/manifest(format=mpd-time-csf)",
		type: "application/dash+xml",
		keys: {
			"com.widevine.alpha": {
				"serverURL": "https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=4c241420-4ec4-42cb-9551-e9eb988d2911"
			}
		}
	}
}
```
<br>

#### 3. Using Multiple Keys

In some cases to support browsers that lack compatibilty of some drm providers, it is required to provide multiple keys. In order to do so multiple key objects should be provided:

```javascript
var config = {
	media : {
		src: "https://willzhanmswest.streaming.mediaservices.windows.net/609f4f57-1e5b-4898-90b1-81c574b2e8e3/VfE.ism/manifest(format=mpd-time-csf)",
		type: "application/dash+xml",
		keys: {
			"com.widevine.alpha": {
				"serverURL": "https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=4c241420-4ec4-42cb-9551-e9eb988d2911"
			},
			"com.microsoft.playready": {
				"serverURL": "https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/"
			}
		}
	}
}
```
<br>

#### 4. Using Multiple Sources

For more information on how to use multiple sources read {@tutorial 03-load-media}. When dealing with multiple sources, the keys for all sources should be provided in the keys object.

```javascript
var config = {
	media : {
		source:[{
			// FIRST SOURCE
			src : "https://willzhanmswest.streaming.mediaservices.windows.net/609f4f57-1e5b-4898-90b1-81c574b2e8e3/VfE.ism/manifest(format=mpd-time-csf)",
			type : "application/dash+xml",
		}, {
			// SECOND SOURCE
			src : "https://willzhanmswest.streaming.mediaservices.windows.net/609f4f57-1e5b-4898-90b1-81c574b2e8e3/VfE.ism/manifest(format=m3u8-aapl)",
			type : "application/x-mpegURL",
		}],
		keys: {
			// KEY FOR FIRST SOURCE
			"com.widevine.alpha": {
				"serverURL": "https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=4c241420-4ec4-42cb-9551-e9eb988d2911"
			},
			// ALTERNATIVE KEY FOR FIRST SOURCE
			"com.microsoft.playready": {
				"serverURL": "https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/"
			},
			// KEY FOR SECOND SOURCE
			"com.apple.fps.1_0": {
				"serverURL": "https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=58ba906b-c94d-4d26-9403-905b6d6760d1",
				"cert": "FPSAC.cer"
			}
		}
	}
}
```
<br>

#### 5. Custom Request Headers

Some license requests require custom headers or credentials. These headers can be provided by passing a `httpRequestHeaders` object as part of each key objects.

```javascript
var config = {
	media : {
		src : "https://willzhanmswest.streaming.mediaservices.windows.net/609f4f57-1e5b-4898-90b1-81c574b2e8e3/VfE.ism/manifest(format=mpd-time-csf)",
		type : "application/dash+xml",
		keys: {
			"com.widevine.alpha": {
				"serverURL": "https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=4c241420-4ec4-42cb-9551-e9eb988d2911",
				"withCredentials": true
			},
			"com.microsoft.playready": {
				"serverURL": "https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/",
				"httpRequestHeaders": {
					"http-header-CustomData": "eyJ1c2VySWQiOiIxMjM0NSIsInNlc3Npb25JZCI6ImV3b2dJQ0p3Y205bWFXeGxJaUE2SUhzS0lDQWdJQ0p3ZFhKamFHRnpaU0lnT2lCN0lIMEtJQ0I5TEFvZ0lDSnZkWFJ3ZFhSUWNtOTBaV04wYVc5dUlpQTZJSHNLSUNBZ0lDSmthV2RwZEdGc0lpQTZJR1poYkhObExBb2dJQ0FnSW1GdVlXeHZaM1ZsSWlBNklHWmhiSE5sTEFvZ0lDQWdJbVZ1Wm05eVkyVWlJRG9nWm1Gc2MyVUtJQ0I5TEFvZ0lDSnpkRzl5WlV4cFkyVnVjMlVpSURvZ1ptRnNjMlVLZlFvSyIsIm1lcmNoYW50IjoiY2FibGVsYWJzIn0K"
				}
			}
		}
	}
}
```
<br>

#### 6. Using Custom Fairplay Handlers

Some advanced use cases for FairPlay require special handling of the license request. Custom FairPlay handlers can be provided by passing the `fps` object as part of the config object.
For example, to use an octet stream instead of the default form encoded message payload, the config might look like the next example:

```javascript
var config = {
	media: {
		src : "https://willzhanmswest.streaming.mediaservices.windows.net/609f4f57-1e5b-4898-90b1-81c574b2e8e3/VfE.ism/manifest(format=m3u8-aapl)",
		keys: {
			"com.apple.fps.1_0": {
				"serverURL":"https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=58ba906b-c94d-4d26-9403-905b6d6760d1",
				"cert": "FPSAC.cer"
			}
		}
	},
	fps: {
		requestLicense: function(message, contentId, serverUrl, keys) {
			var request = {
				url: serverUrl,
				method: "POST",
				responseType: "arraybuffer",
				headers: {
					"Content-Type": "application/octet-stream",
					"utoken-drm": "fp"
				},
				data: new Uint8Array(message)
			};

			return akamai.amp.Utils.request(request).then(function (xhr) {
				return new Uint8Array(xhr.response);
			})
			.catch(function (error) {
				throw "The license request failed.";
			});
		}
	}
};
```

The full list of FairPlay overridable functions are:

```javascript
var config = {
	fps: {
		extractServerUrl: function (initData, keys) {
			return // String. The server url
		},
		extractContentId: function (initData, keyData) {
			return // String. The content id
		},
		requestCertificate: function (keys) {
			return // Promise.<Uint8Array>
		},
		concatInitDataIdAndCertificate: function (initData, id, cert) {
			return // Uint8Array
		},
		requestLicense: function (message, contentId, serverUrl) {
			return // Promise.<Uint8Array>
		}
	}
}
```
