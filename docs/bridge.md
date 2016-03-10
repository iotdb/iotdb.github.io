# Bridges

The IOTDB Node.JS codebase has a concept of a "Bridge", which is like a device driver. It has the following duties, and provides a standard pattern for doing these:

* discover new Things
* assign repeatable / persistent ID numbers to Things
* send data / commands to Things (and report whether it finished)
* asynchronously receive data when available
* get "inherent" metadata (for example, a WeMo Switch has a name which can be set in software)
* asynchronously monitor reachability
* asynchronously monitor metadata changes
* handle disconnects

Bridges have no real IOTDB dependency, except for some helper code. If you're doing a NodeJS IoT project and you want to talk to Things, you should be able to pick these up and use them.

Bridges do follow the IOTDB pattern of "The IoT is moving JSON dictionaries around". They do not have any concept of semantics: this is something that get layered on top.

Most of the projects here named homestar-* are Bridges. All have sample code. Not all have been tested, this is noted in the documentation. Maybe you can help!

* [https://github.com/dpjanes?tab=repositories](https://github.com/dpjanes?tab=repositories)

Master list:

* [https://github.com/dpjanes/iotdb-homestar/blob/master/docs/modules.md](https://github.com/dpjanes/iotdb-homestar/blob/master/docs/modules.md)
