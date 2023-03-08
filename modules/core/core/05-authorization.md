---
layout: techdocs-web
title: Token Protected Streams
categories: [core]
position: 5
---

Here is a basic example of how to step up AMP for use with tokenized streams:
```javascript
var config = {
  media: {
    src: "http://url-of-stream-without-token-appended"
    status: {
      // this tells the player the media needs to be authorized
      state: "blocked"
    }
  }
};
var amp = akamai.amp.AMP.create("akamai-media-player", config);
amp.addEventListener("authorize", function () {
  // do token generation / retrieval
  amp.authorize({
    token: "TOKEN_STRING",
    // optional timestamp. If provided the player will fire the
    // "authorize" event when expiration has occurred
    expiration: 1479319024356
  });
});
```

If the authorization needs to be provided upfront, pass the token separately instead of appending it to the url:
```javascript
var config = {
  media: {
    src: "http://url-of-stream-without-token-appended"
    authorization: {
      token: "TOKEN_STRING",
      // optional timestamp. If provided the player will fire the
      // "authorize" event when expiration has occurred
      expiration: 1479319024356  
    }
  }
};
var amp = akamai.amp.AMP.create("akamai-media-player", config);
```

In cases where the expiration is not known, `amp.authorize` can be called at any time and the player will use the latest authorization block when reattaching the stream.
