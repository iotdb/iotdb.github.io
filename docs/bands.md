# Bands

This is really one my favorite insights into how Things and APIs work together. I gave two presentations on Global IoT Day in Vienna about this

* [Interoperability with Standardless IoT](http://www.slideshare.net/dpjanes/2015-04-global-io-t-day-wien-interoperability-with-stanardless-iot)
* [What a Thing API Should Look Like](http://www.slideshare.net/dpjanes/what-a-thing-api-should-look-like-global-iot-day)

So building on the previous message, we have the same definitions for controlling a thing as reading values of a Thing. How do we differentiate between these various aspects? Add into the picture that we also have to deal with _metadata_ and we have to deal with the _model_ (in JSON-LD), how does this fit?

So here's the key insight: a "Thing" is _not_ JSON dictionary that we manipulate. Instead a Thing, identified by some Thing ID, is a jumping off point to a cloud of related but independent JSON dictionaries. These are (at least):

* istate - the Input State: the actual state of thing
* ostate - the Output State: the state we want the thing to become
* meta - the Thing's metadata
* model - the Thing's JSON-LD Model

The entire IoT / Web of Things can - and _should_ -  be seen as just reading an manipulating these four JSON dictionaries! The back end is just shuffling the data around to the proper point to be actioned!

I'm just going to show this in a slightly different way, because I'm absolutely in love with this and once you get it it opens up tons of possibilities for different implementations. The entire "Web of Things" can just be seen as a table that looks like this

	Thing ID | istate | ostate | meta | model

You want to change a Thing? 

	SET ostate={something} WHERE ThingID={thingid}

You want to set the state of a Thing?

	GET istate WHERE ThingID={thingid}

You want to set the metadata?

	SET meta={something} WHERE ThingID={thingid}

You want to get the metadata?

	GET meta WHERE ThingID={thingid}

You want to know what the istate or ostate actually means?

	GET model WHERE ThingID={thingid}

I almost peed myself with excitement once I got this concept. It clarifies everything.
