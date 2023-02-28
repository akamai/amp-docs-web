---
layout: techdocs-web
title: Captioning
categories: [core]
position: 12
---

This tutorial shows how to properly add close captions when using AMP.

The topics covered in this page are:

* 1 Adding captions.
* 2 Adding captions for multiple laguages.
* 3 Using embedded captions.
  * 3.1 Auto text tracks mode.
  * 3.2 Hand-picking text tracks.
* 4 Custom rendering.
* 5 Using cue point transformation.
<br>
<br>

#### 1. Adding Captions

AMP supports the following captioning formats by default:
- VTT
- TTML
- 608
- 708

To include caption tracks in media playback, provide a `track` array to the media object. Each item in the array should have the following properties:
- `src`: The path to the caption file
- `type`: The mime type of the file
- `kind`: The kind of text track. For captions, use the string `"captions"`
- `srclang`: Language code of the given track

Below there's an example.

```javascript
var config = {
  media: {
    src: "http://video.xyz.com/master.m3u8",
    type: "application/x-mpegURL",
    track: [{
      kind : "captions",
      type: "application/ttml+xml",
      src: "captioning.xml",
      srclang: "en"
    }]
  }
};
```

For further information please check:
* {@link akamai.amp.Track}
* {@link akamai.amp.Media}
* {@link akamai.amp.PlayerConfig}
<br>

#### 2. Adding Captions for Multiple Languages

Tracks for individual languages can be set using the `srclang` property of the track items with an ISO 639-1 language code. The player will choose the track based on the player's `language` setting (see {@tutorial 11-localization} for more details):

```javascript
var config = {
  media : {
    src : "http://video.xyz.com/master.m3u8",
    type : "application/x-mpegURL",
    track : [{
      kind : "captions",
      type : "text/vtt",
      src : "captioning-en.vtt",
      srclang : "en"
    }, {
      kind : "captions",
      type : "application/ttml+xml",
      src : "captioning-es.xml",
      srclang : "es"
    }]
  }
};
```
<br>

#### 3. Using Embedded Captions

When using embedded captions with AMP, is no longer required to set the tracks alongside the configuration object, AMP automatically exposes the available text tracks on player UI.
However, tracks can still be manipulated through player configuration in case of miss-labeling or hand-picking.

##### 3.1. Auto text tracks mode

The absence of the `track` property indicates the player to expose all the text tracks available in the given media source such as captions, subtitles and descriptions.

```javascript
var config = {
  media : {
    src : "https://devstreaming-cdn.apple.com/videos/streaming/examples/bipbop_adv_example_hevc/master.m3u8",
    type : "application/x-mpegURL",
    track : []
  }
};
```

##### 3.2. Hand-picking text tracks

The player may perform text track mapping for 608, 708, or vtt captions by providing the `track` setting. For embedded types, the `src` property is not needed, since the text tracks are provided as part of the stream data. When mapping text tracks client must provide the proper kind, mime type, and language tag.

The mime types for embedded format types are:
- 608: `"text/cea-608"`
- 708: `"text/cea-708"`
- WebVTT (sidecar): `"text/vtt"`

```javascript
var config = {
  media : {
    src : "http://video.xyz.com/master.m3u8",
    type : "application/x-mpegURL",
    track : [{
      kind : "captions",
      type : "text/cea-608",
      srclang: "en"
    }]
  }
};
```
<br>

#### 4. Custom Rendering

Certain scenarios require specific handling of the caption rendering. AMP provides two rendering engines for captions:
- `html`: Captions are rendered in a HTML overlay
- `native`: Captions are rendered natively by the video tag

By default the player will automatically choose which renderer is best for the platform. To override this behavior, provide the `renderer` config option.

```javascript
var config = {
  captioning: {
    renderer: "native"
  }
};
```
<br>

#### 5. Using Cue Point Transformation

Sometimes there is a need to alter a cue point before rendering it on-screen. This can be accomplished by using the transform API. Similar to media transforms, each cue can be run through a function to alter it's contents:

```javascript
amp.addTransform(akamai.amp.TransformType.CUE_CHANGE, function (cues) {
  cues.forEach(function (cue) {
    cue.html += "<p>Transformed!</p>"
  });
  return cues;
});
```

> For more information on media transforms please check {@tutorial 06-media-transforms}.