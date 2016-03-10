# IOTDB

Before we dive into the semantic "hows / whys" of IOTDB, I'd like to show you how it looks from a Node.JS programmer perspective.

First:

    iotdb = require('iotdb')

## Connecting to Things

Now we can start doing stuff. This command "connects to everything that we can automatically connect to":

    things = iotdb.connect()

or we can connect to a specific **Model** (the type of a Thing):

    things = iotdb.connect('WeMoSwitch')
    
Some devices cannot be automatically connected to, as they require some sort of configuration (*this is from [homestar-johnny-five](https://github.com/dpjanes/homestar-johnny-five)*):

    var things = iotdb.connect('GroveMoistureSensor', {
        pin: "A0"
    });

You can call <code>connect</code> multiple times:

	wemos = iotdb.connect('WeMoSocket')
	hues = iotdb.connect('HueLight')
	things = iotdb.things()
	
	
You can dot-chain <code>connect</code>s:

	things = iotdb
				.connect('WeMoSocket')
				.connect('HueLight')
				
_How do you get the <code>WeMoSocket</code>, <code>HueLight</code>, etc. Models? You have to install the appropriate HomeStar Modules: [instructions here](https://homestar.io/about/things)._
				
## Things vs a Thing

You'll note that the <code>connect</code> commands are going into a variable called **things** not **thing**.
Why?
Because - theoretically at least - each of these commands has the capability of connecting to more than one Thing.

For example, if you have five WeMo Sockets on your network, <code>connect('WeMoSocket')</code> will eventually connect to all of them and all of them will be available in the <code>things</code> Array.

### Commands

Some commands, such as <code>set</code>, <code>update</code> and <code>on</code> can be issued **even before Things show up**. For example, let's say you did:

	iotdb.connect('WeMoSocket').set(':on', true)
	
and then plugged in the WeMo afterwards. 
Once IOTDB discovers the WeMo, it will turn it on.

### Getting Individual Things

If you want to access an individual Thing, the recommended way to do it is:

	things.on("thing", function(thing) {
	});
	
which will invoke the callback for every Thing that is discovered (and has been previously discovered).

## Manipulating Things

IOTDB is all about representing a Thing's **multiple** states as JSON-like dictionaries, and then allowing users to **semantically** manipulate the Things. 

### Semantic Manipulation

This is the preferred way of manipulating the state of a Thing.

#### Set

Here's how to turn everything on using IOTDB semantically:

    things.set(':on', true)
    
The colon in front of <code>:on</code> indicates that we want to use the _semantic_ concept of **on**, which is actually a shorthand for 
<code>iot-purpose:on</code> which in turn is actually the URL
<code>[https://iotdb.org/pub/iot-purpose#on](https://iotdb.org/pub/iot-purpose.html#on)</code>. 

The following statements are all equivalent:

    things.set(':on', true)
    things.set('iot-purpose:on', true)
    things.set('https://iotdb.org/pub/iot-purpose#on', true)

The reason we use URLs to represent how Things work is:

* this is core concept of [Linked Data](https://en.wikipedia.org/wiki/Linked_data), use URLs rather than "IDs"
* this gives us open-ended unlimited possibilities for vocabularies

#### On / Events

Things will tell us when they have changed. The following
code will trigger whenever the Thing is turned on or off:

	things.on(":on", function(thing, attribute, value) {
		console.log("the Thing is on=" + value);
	});

#### Get

You can also explicitly get the state of a Thing:

	things[0].get(":on")
	
Note that <code>get(...)</code> doesn't make sense in the context of an Array of Things, it has to be done on an individual Thing.

In general you'll probably be mostly using the <code>on(...)</code> method to get state updates.

### Band Manipulation

There are many times when you'll need to access the underlying data of a Thing. 
IOTDB assumes this data is JSON-like and calls them [bands](https://homestar.io/about/state).

There are four different kinds of bands for a Thing, called **meta**, **model**, **istate** and **ostate**.

#### istate

A Thing's **istate** - the "input" state - the actual current state of the Thing.

You retrieve the **istate** of a Thing with the following command:

    thing.state("istate");
    
And you can update it with this:

	thing.update("istate", {
		"powered": true
	});

If you want to see updates to the **istate**, do

    thing.on("istate", function(thing_inner) {
        console.log("updated istate", 
        	"\n ", thing_inner.thing_id(), 
        	"\n ", thing_inner.state("istate"));
    });

IMPORTANT:
The **istate** band **is not semantic**. 
It is described by the **model** band (below). 

You can get the semantic description of Thing this way:

	## get a complete description of the Thing, in
	## terms of the semantic keys
	thing.describe()
	
	## get a complete description of the Thing, in
	## terms of the semantic keys
	thing.describe({ code: true })
	
	## describe what the semantic key ":on" means
	thing.describe(":on")
	
	## describe what the dictionary key "powered" means
	thing.describe("powered")

#### ostate

The **ostate** band - the output state - is commands we are sending
to a Thing.

This returns the current ostate. Note however that usually everything in the ostate has a value of <code>null</code> unless there is a command currently executing.

    thing.state("ostate");
    
You can update the **ostate** using <code>update(...)</code>, but the preferred way to do this is using the <code>set(...)</code> method.

#### meta

This is the thing's metadata. Metadata includes items such as it's name, is it reachable, what does it do (called *facets*), where it is (called *zones*), and so forth:

    thing.state("meta");

If you want to e.g. change the name of a Thing

	thing.update("meta", {
		"schema:name": "My New Thing Name",
	});

#### model

This is the Thing's model (i.e. the full Semantic description):

    thing.state("model");
    
Generally you will not need to look at this, and you never <code>update</code> it.

