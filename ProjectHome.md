# A Java interface to the bit.ly and j.mp APIs. #

## Bitlyj 2.0: A DSL for Bitly-powered Url Shortening Services ##

This is probably all most will be interested in:

```
import com.rosaloves.bitlyj.Url;
import static com.rosaloves.bitlyj.Bitly.*;

Url url = as("bitlyapidemo", "R_0da49e0a9118ff35f52f629d2d71bf07").call(shorten("http://rosaloves.com/stories/view/13"));

// url.getShortUrl() -> http://bit.ly/fB05
```

There's more, of course :-). Check out [QuickStart](QuickStart.md) to see more usage, and [Bitlyj2AndTheScalaREPL](Bitlyj2AndTheScalaREPL.md) for even more in an interactive Scala session.

## 2.0 Noteworthies ##
  * Concise DSL syntax with obvious semantics == bitly interaction with no boilerplate.
  * Natural error handling with no checked exceptions. If you want to deal with exceptions, catch BitlyException and access the delivered message (yields bitly's status text).
  * J.mp support baked in, with the same DSL sugar.
  * Runs on Android.
  * Zero dependencies.
  * Flexible API. Bitly methods are no longer hard-wired to an interface, so evolution is possible without API breakage.
  * Extensible API. Implementing your own methods is simple: implement the functionality in an implementation of BitlyMethod. You get core error handling for free, and you can even implement specialized methods not supported by bitly.
  * Access to other bitly-powered services is simple: implement Provider (two methods).

The stable 2.0 artifacts are available in maven central.

```
<dependency>
	<groupId>com.rosaloves</groupId>
	<artifactId>bitlyj</artifactId>
	<version>2.0.0</version>
</dependency>
```

I care about your input, so please join the group to share it or file issues/feature requests as you find them.

## Maven Artifacts Now Available on Maven Central ##
Many thanks to [Sonatype](http://sonatype.com/) for providing [free artifact hosting service](http://nexus.sonatype.org/oss-repository-hosting.html) (via Nexus) for open source projects. For your mavenized open source project, I recommend it.