#Bitlyj 2 quickstart.

# Introduction #

## Basic Use ##

First off, imports:

```
import com.rosaloves.bitlyj.*;
import static com.rosaloves.bitlyj.Bitly.*;
```

The first will expose, among other things, all types that will result from the core methods (those supported directly in bitlyj). The static import brings in support for the DSL. You don't have to use it like this, but it's quite nice.

The quickest way to shorten a URL:

```
as("bitlyapidemo", "R_0da49e0a9118ff35f52f629d2d71bf07").call(shorten("http://rosaloves.com/"));
```

Breaking it down, `as` is a factory method for retrieving a Provider instance.

```
Provider bitly = as("bitlyapidemo", "R_0da49e0a9118ff35f52f629d2d71bf07");
```

It's static so as to support a nice DSL-like interface. If you prefer verbosity, you can qualify it more fully:

```
Provider bitly = Bitly.as("bitlyapidemo", "R_0da49e0a9118ff35f52f629d2d71bf07");
```

Once you have a provider, you can call methods on it:

```
bitly.call(shorten("http://rosaloves.com/"));
```

Like `as`, `shorten` is also part of the DSL interface. Peruse [Methods.java](http://code.google.com/p/bitlyj/source/browse/#svn/trunk/src/main/java/com/rosaloves/bitlyj) for an accurate list of DSL methods.

## Bulk Methods ##
Some bitly methods support multiple arguments. `info` and `clicks` for example can take an arbitrary number of `hash` or `shortUrl` arguments. You can do this in bitlyj just like you'd expect:

```
for(UrlInfo info : bitly.call(info("http://tcrn.ch/a4MSUH", "http://bit.ly/1YKMfY"))) {
	// do something with info
}
```

## Working With j.mp ##

Working with j.mp is exactly the same as working with bit.ly, with the exception of the imports:

```
import com.rosaloves.bitlyj.*;
import static com.rosaloves.bitlyj.Bitly.*;
import static com.rosaloves.bitlyj.Jmp.*;
```

Notice import of `com.rosaloves.bitlyj.Jmp.*`. This brings in a version of the `as` function that yields Provider instances pointing to the j.mp endpoint. Everything else is the same.