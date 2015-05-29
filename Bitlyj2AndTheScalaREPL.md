#Using bitlyj 2 in the Scala REPL

# A Session in the Scala REPL #

The DSL in bitlyj 2 makes it feel quite natural in Scala. What's more, the library is strict about quality toString overrides, as you can see in this example REPL session:

```
scala> import com.rosaloves.bitlyj._                                                            
import com.rosaloves.bitlyj._

scala> import Bitly._                                                                           
import Bitly._

scala> val bitly = as("bitlyapidemo", "R_0da49e0a9118ff35f52f629d2d71bf07")
bitly: com.rosaloves.bitlyj.Shortener = Shortener [endPoint=http://api.bit.ly/v3/]

scala> bitly.call(clicks("http://bit.ly/H4HnM"))                        
res0: com.rosaloves.bitlyj.UrlClicks = UrlClicks [globalClicks=99, userClicks=99, url=Url [globalHash=40rYlN, hash=null, longUrl=null, shortUrl=http://bit.ly/H4HnM]]

scala> res0.getTotalClicks
res1: Long = 198
```

Of course, you could do it in one go:

```
as("bitlyapidemo", "R_0da49e0a9118ff35f52f629d2d71bf07").call(clicks("http://bit.ly/H4HnM")).getTotalClicks
res1: Long = 198
```

Watch out! Using that demo account will get you limited!

```
com.rosaloves.bitlyj.BitlyException: RATE_LIMIT_EXCEEDED
	at com.rosaloves.bitlyj.Shortener.filterErrorResponse(Shortener.java:77)
	at com.rosaloves.bitlyj.Shortener.call(Shortener.java:40)
	at .<init>(<console>:9)
	at .<clinit>(<console>)
	at RequestResult$.<init>(<console>:3)
	at RequestResult$.<clinit>(<console>)
	at RequestResult$result(<console>)
	at sun.reflect.NativeMethodAcces...
```

Other errors:

```
scala> as("aintnobody", "fakekey").call(shorten("http://google.com"))
com.rosaloves.bitlyj.BitlyException: INVALID_LOGIN
	at com.rosaloves.bitlyj.Shortener.filterErrorResponse(Shortener.java:77)
	at com.rosaloves.bitlyj.Shortener.call(Shortener.java:40)
	at .<init>(<console>:9)
	at .<clinit>(<console>)
	at RequestResult$.<init>(<console>:3)
	at RequestResult$.<clinit>(<console>)
	at RequestResult$result(<console>)
	at sun.reflect.NativeMethodAccessorImp...
scala> as("aintnobody", "").call(shorten("http://google.com"))    
com.rosaloves.bitlyj.BitlyException: MISSING_ARG_APIKEY
	at com.rosaloves.bitlyj.Shortener.filterErrorResponse(Shortener.java:77)
	at com.rosaloves.bitlyj.Shortener.call(Shortener.java:40)
	at .<init>(<console>:9)
	at .<clinit>(<console>)
	at RequestResult$.<init>(<console>:3)
	at RequestResult$.<clinit>(<console>)
	at RequestResult$result(<console>)
	at sun.reflect.NativeMethodAccess...
```

Yay! Nice error handling!