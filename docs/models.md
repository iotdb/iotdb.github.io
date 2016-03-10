# Models

Models are a **semantic description** of the JSON data / [state](state) in
the **istate** and **ostate** [bands](bands).

## Vocabulary

The [vocabulary](vocab) for Models uses [linked data](https://en.wikipedia.org/wiki/Linked_data) 
which effectively provides us an unlimited vocabulary.

The main namespaces we use are:

* [schema.org](http://schema.org/) - core vocabulary
* [iot](https://iotdb.org/pub/iot.html) - core IoT vocabulary
* [iot-purpose](https://iotdb.org/pub/iot-purpose.html) - what terms mean
* [iot-unit](https://iotdb.org/pub/iot-unit.html) - weights and measures
* [iot-facet](https://iotdb.org/pub/iot-facet.html) - what things can do
* [wikipedia](htt://en.wikipedia.org/wiki/Main_Page) - other terms

You can contribute to the IOTDB vocabulary:

* https://github.com/dpjanes/iotdb-vocabulary

## Models

The vocabulary for all the Things defined by IOTDB can
be found in the **models** folder of each [module](module).
For example:

* https://github.com/dpjanes/homestar-wemo/tree/master/models

## Writing Models

### IoTQL

    CREATE MODEL WeMoSocket WITH
        schema:name = "WeMo Socket",
        schema:description = "Belkin WeMo Socket",
        iot:facet = iot-facet:plug,
        iot:facet = iot-facet:switch
    ATTRIBUTE on WITH
        schema:name = "on",
        iot:purpose = iot-purpose:on,
        iot:type = iot:type.boolean,
        iot:read = true,
        iot:write = true,
        iot:sensor = true,
        iot:actuator = true,
    ;

IoTQL models are compiled to JSON-LD by the command (install iotql globally to get this).

    $ iotql-model WeMoSocket.iotql

### JSON

The **istate** and **ostate** [bands](bands) for this model look like this:

    {
        "on": true
    }

Where the key "on" corresponds to <code>ATTRIBUTE on</code> and the 
fact that a boolean value is by <code>iot:type = iot:type.boolean</code>.


### JSON-LD

This is the corresponding JSON-LD for the IoTQL

    {
      "@context": {
        "@base": "file:///we-mo-socket",
        "@vocab": "file:///we-mo-socket#",
        "iot": "https://iotdb.org/pub/iot#",
        "schema": "http://schema.org/",
        "iot-purpose": "https://iotdb.org/pub/iot-purpose#",
        "iot-facet": "https://iotdb.org/pub/iot-facet#",
        "iot:facet": {
          "@id": "https://iotdb.org/pub/iot#facet",
          "@type": "@id"
        },
        "iot:purpose": {
          "@id": "https://iotdb.org/pub/iot#purpose",
          "@type": "@id"
        },
        "iot:type": {
          "@id": "https://iotdb.org/pub/iot#type",
          "@type": "@id"
        }
      },
      "@id": "",
      "@type": "iot:Model",
      "schema:name": "WeMo Socket",
      "schema:description": "Belkin WeMo Socket",
      "iot:facet": [
        "iot-facet:plug",
        "iot-facet:switch"
      ],
      "iot:attribute": [
        {
          "@type": "iot:Attribute",
          "@id": "#on",
          "schema:name": "on",
          "iot:purpose": "iot-purpose:on",
          "iot:type": "iot:type.boolean",
          "iot:read": true,
          "iot:write": true,
          "iot:sensor": true,
          "iot:actuator": true
        }
      ]
    }

