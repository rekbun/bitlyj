# Bitlyj 1.0 #

This page is about bitlyj 1.0, which is tied to the deprecated bitly api version 2.0.1. It is kept here for historical reference.

As of the 1.0.0 release, I'm calling bitlyj stable. It's seen a good deal of usage for bit.ly and j.mp without any new issue reports, so for the current bit.ly API version (2.0.1), the library is stable.

```
// Get an instance using the API demo credentials.
Bitly bitly = BitlyFactory.newInstance("bitlyapidemo", "R_0da49e0a9118ff35f52f629d2d71bf07");

// Shorten the URL to the Hope Transfusion story.
BitlyUrl bUrl = bitly.shorten("http://rosaloves.com/stories/view/13");
// bUrl.getShortUrl() -> http://bit.ly/fB05

// Expand a shortened URL by its hash (or short name/keyword).
URL url = bitly.expandHash("hopetransfusion");
// url -> http://rosaloves.com/stories/view/13

// Grab the aggregated data of a shortened URL by its hash (or short name/keyword).
BitlyUrlInfo info = bitly.info("hopetransfusion");
// info.getUrl() -> http://rosaloves.com/stories/view/13
```

The j.mp API is effectively the same, differing only in the shortened link URL and API endpoint. This congruency is exploited by the library, and so using j.mp is exactly the same as using bit.ly. The only difference is the factory method:

```
Bitly bitly = BitlyFactory.newJmpInstance("bitlyapidemo", "R_0da49e0a9118ff35f52f629d2d71bf07");
```