# Flume Headers To Avro Serializer

This flume serializer use the Event Headers to build an Avro Event File, using a provided Avro schema

Compilation and packaging
----------
```
  $ mvn package
```

Deployment
----------

Copy headerToAvroSerializer-<version>.jar in target folder into flume plugins dir folder
```
  $ mkdir -p $FLUME_HOME/plugins.d/headers-to-avro-serializer/lib
  $ cp headerToAvroSerializer-0.0.3.jar $FLUME_HOME/plugins.d/headers-to-avro-serializer/lib
```

Configuration
----------

| Property name | Default value | Description
| ----------------------- | :-----: | :---------- |
| compressionCodec| null | Avro compression codec. "snappy", "deflate" or "null"
| syncIntervalBytes | 2048000 | Avro sync interval, in approximate bytes

Providing the Avro Schema
------
<p>Avro schema information must be set in the flume Event Headers.</p>
<p>One of the following two fields must exists in the header.</p>
> <b>flume.avro.schema.url</b>: location of the Avro Schema File. e.g ```hdfs:///user/flume/avroSchemas/exampleSchema.avsc```
> <b>flume.avro.schema.literal</b>: complete avro schema (not recommended)



Configuration example
---------------------
```
a1.channels = c1
a1.sinks = k1
a1.sinks.k1.type = hdfs
a1.sinks.k1.hdfs.path = /user/flume/rawData
a1.sinks.k1.hdfs.fileSuffix = .avro
a1.sinks.k1.serializer = org.keedio.flume.serializer.HeaderToAvroSerializer$Builder
a1.sinks.k1.serializer.compressionCodec = snappy
```
