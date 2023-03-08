This tutorial shows how to properly configure DVR playback on AMP.

1. Fast Playback Startup
2. Playback Bitrate Ceiling

#### 1. Fast Playback Startup
Startup time can be adjusted by lowering the initial rendition quality. Player's ABR mechanism performs upswitching for higher renditions if user agent bandwidth permits it. 

```javascript
    const config = {
		autoplay: true,
		autoplayPolicy: "muted",
		hls: {
			quality: {
					startLevel: 0 // use the lowest 
			}
		}
	}
```
Hls `startLevel` allows the following `number` type values:
  - `0` Starts from Lowest rendition available in the manifest.
  - `-1` Player will start from rendition matching download bandwidth.
  - Upper values represents the available renditions in the manifest bitrate ladder, the higher the value is the better the initial quality is.

#### 2. Playback Bitrate Ceiling
Player allows limiting the maximum bitrate selectable by the ABR mechanism. This might be useful for scenarios like browser's memory flooding, small viewport players, live background playback and others...

``` javascript
    const config = {
		autoplay: true,
		autoplayPolicy: "muted",
		hls: {
			maxBitrate: 500000 // 0.5 Mbps
		}
	}
```
Dash and Hls `maxBitrate` represents the bitrate ceiling value in bits per second `bps`, this can be adjusted through whether player configuration or runtime as follows.

``` javascript
amp.maxBitrate = 2000000 // 2.0 Mbps
```

Player ignores the ceiling value when there is no matching renditions with the given value; user's manually select a rendition through player's quality selector or API.
