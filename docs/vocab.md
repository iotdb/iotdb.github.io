# Vocabulary

Next, I'd like to introduce to the actual JSON-LD semantic definitions. 
Where possible, we build from [schema.org](https://schema.org)'s definitions.

There is a fully browsable definition set here, as well as the GitHub source:

* [https://iotdb.org/pub/](https://iotdb.org/pub/)
* [https://github.com/dpjanes/iotdb-vocabulary](https://github.com/dpjanes/iotdb-vocabulary)

The vocabulary is divided into four different sections:

1) iot: [https://iotdb.org/pub/iot.html](https://iotdb.org/pub/iot.html)

These are the core definitions, including our major types

2) iot-attribtue: [https://iotdb.org/pub/iot-attribute.html](https://iotdb.org/pub/iot-attribute.html)

These definite our semantic definitions of how things are manipulated / how sensors report data.

3) iot-facet: [https://iotdb.org/pub/iot-facet.html](https://iotdb.org/pub/iot-facet.html)

Facets are how we "duck type" Things. Consider a WeMo Switch. Independent of it's Model, _what it is_ depends on what it's connected to. If it's connected to a light bulb, we can attach "iot-facet:lighting" to the metadata. If it's a space heater, perhaps "iot-facet:climate.heating"

4) iot-unit: [https://iotdb.org/pub/iot-unit.html](https://iotdb.org/pub/iot-unit.html)

This is our "units / weights / measure" definitions. Now you are probably asking yourself "why the heck do we need a new weights and measure system?". When I started this project, the issues are:
copyright / non-open definitions
not responding to emails
moribund project
I believe this much to be the state of the world right now. 

One important characteristic of these definitions is the words we use are _colloquial_ and not obsessively formal. One long term issue I've noticed with semantic projects is they get into "how many angels can dance on the head of a pin" type issues. These definitions are meant to be recognizable and understandable by programmers and modellers. And the underlying definitions are rock sold.
