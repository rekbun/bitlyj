#How to roll your own methods.

# Details #

bitlyj2 uses the [native DOM APIs](http://download.oracle.com/docs/cd/E17476_01/javase/1.5.0/docs/api/org/w3c/dom/package-summary.html) of the java platform to consume XML payloads that result from bit.ly method invocations. When you implement a bitly method, your method instance receives a [Document](http://download.oracle.com/docs/cd/E17476_01/javase/1.5.0/docs/api/org/w3c/dom/Document.html) instance.

## An Example: v3/validate ##
Here's how you roll your own method. The following example would add support for bitly's  [validate](http://code.google.com/p/bitly-api/wiki/ApiDocumentation#/v3/validate) method.

```
public class Validate extends MethodBase<Boolean> {
	public Validate(String user, String apiKey) {
		super("validate", Pair.p("x_login", user), Pair.p("x_apiKey", apiKey));
	}

	public Boolean apply(Provider provider, Document document) {
		String valid = Dom.getTextContent(
			document.getElementsByTagName("valid").item(0));
		return Integer.parseInt(valid) == 1;
	}
}
```

If you want to avoid subclassing, you can implement `BitlyMethod<A>` at the cost of a bit more code:

```
public class Validate implements BitlyMethod<Boolean> {
	public String getName() {
		return "validate";
	}

	public Iterable<Pair<String, String>> getParameters() {
		return Arrays.asList(Pair.p("x_login", user), Pair.p("x_apiKey", apiKey));
	}

	public Boolean apply(Provider provider, Document document) {
		String valid = Dom.getTextContent(
			document.getElementsByTagName("valid").item(0));
		return Integer.parseInt(valid) == 1;
	}
}
```

Now that you have your own method, you can call it like any other:

```
Validate validate = new Validate("notbilytapi", "not_apikey");
boolean isValid = as("bitlyapidemo", "R_0da49e0a9118ff35f52f629d2d71bf07").call(validate);
```

**Important:** Note the use of `Dom.getTextContent` instead of calling [Node#getTextContent](http://download.oracle.com/docs/cd/E17476_01/javase/1.5.0/docs/api/org/w3c/dom/Node.html#getTextContent()). This isn't a requirement, but it's strongly recommended as it ensures interoperability with android. Android's dalvik vm carries an older version of the DOM API that lacks this method.

Note that you don't need to do any error checking. In bitlyj 2, it's the provider implementation's job to invoke the remote method, parse its payload, and do basic error checking before ever calling your method implementation. If an I/O error occurs, or bitly responds with and error message (or even garbled data), your method won't be called and the shortener will have thrown and informative exception.