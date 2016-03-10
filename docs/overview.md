# Overview

I'd thought I'd summarize my / IOTDB's beliefs as shared in the previous pages.

**JSON-Dictionary / Thing Manipulation Equivalency**

Manipulating Things, reading sensors, etc can entirely be modelled by reading, writing and observing changes to JSON Dictionaries. 

**REST mapping**

Manipulating Things using web services only requires GET, PUT and PATCH operations on a URL representing a Thing. This is basically a Lemma of 1). 

**Multiple Dictionaries per Thing**

Things have multiple JSON Dictionaries associated with them, namely for the State, for the Metadata, and Model. The State frequently changes, the Metadata less frequently, and the Model is essentially static. These Dictionaries are independent of each other, but obviously all work well together.

**Introspection**

We should be able to understand the State of a Thing by introspecting the Model. The Model is a semantic description of all the attributes of the State, written in JSON-LD. Entire user interfaces should and can be written simply through introspection.

**Interstitial State Must Be Modelled**

Interstitial state is the time between when we say "do something" and when we find out it is actually done. Real Things have a real human noticeable interstitial time lag.

**Parallel Attributes**

With most manipulable Things, Attributes almost always come in pairs: one for controlling a particular aspect of a Thing, and one for reading actual value of that Aspect. They are almost semantically identical, except for this one differentiation. Having to double all descriptions and attributes is incredibly annoying and mentally taxing.

**IState and OState**

The Parallel Attributes issue can be cleanly swept away by saying Things have to different types of states: one for holding the actual state of a Thing (the istate) and one for holding
