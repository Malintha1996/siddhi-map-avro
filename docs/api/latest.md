# API Docs - v2.0.2

## Sinkmapper

### avro *<a target="_blank" href="https://siddhi.io/en/v5.0/docs/query-guide/#sink-mapper">(Sink Mapper)</a>*

<p style="word-wrap: break-word">This extension is a Siddhi Event to Avro Message output mapper.Transports that publish  messages to Avro sink can utilize this extension to convert Siddhi events to Avro messages.<br>&nbsp;You can either specify the Avro schema or provide the schema registry URL and the schema reference ID as parameters in the stream definition.<br>If no Avro schema is specified, a flat Avro schema of the 'record' type is generated with the stream attributes as schema fields.</p>

<span id="syntax" class="md-typeset" style="display: block; font-weight: bold;">Syntax</span>
```
@sink(..., @map(type="avro", schema.def="<STRING>", schema.registry="<STRING>", schema.id="<STRING>")
```

<span id="query-parameters" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">QUERY PARAMETERS</span>
<table>
    <tr>
        <th>Name</th>
        <th style="min-width: 20em">Description</th>
        <th>Default Value</th>
        <th>Possible Data Types</th>
        <th>Optional</th>
        <th>Dynamic</th>
    </tr>
    <tr>
        <td style="vertical-align: top">schema.def</td>
        <td style="vertical-align: top; word-wrap: break-word">This specifies the required Avro schema to be used to convert Siddhi events to Avro messages.<br>The schema needs to be specified as a quoted JSON string.</td>
        <td style="vertical-align: top"></td>
        <td style="vertical-align: top">STRING</td>
        <td style="vertical-align: top">No</td>
        <td style="vertical-align: top">No</td>
    </tr>
    <tr>
        <td style="vertical-align: top">schema.registry</td>
        <td style="vertical-align: top; word-wrap: break-word">This specifies the URL of the schema registry.</td>
        <td style="vertical-align: top"></td>
        <td style="vertical-align: top">STRING</td>
        <td style="vertical-align: top">No</td>
        <td style="vertical-align: top">No</td>
    </tr>
    <tr>
        <td style="vertical-align: top">schema.id</td>
        <td style="vertical-align: top; word-wrap: break-word">This specifies the ID of the avro schema. This ID is the global ID that is returned from the schema registry when posting the schema to the registry. The specified ID is used to retrieve the schema from the schema registry.</td>
        <td style="vertical-align: top"></td>
        <td style="vertical-align: top">STRING</td>
        <td style="vertical-align: top">No</td>
        <td style="vertical-align: top">No</td>
    </tr>
</table>

<span id="examples" class="md-typeset" style="display: block; font-weight: bold;">Examples</span>
<span id="example-1" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">EXAMPLE 1</span>
```
@sink(type='inMemory', topic='stock', @map(type='avro',schema.def = """{"type":"record","name":"stock","namespace":"stock.example","fields":[{"name":"symbol","type":"string"},{"name":"price","type":"float"},{"name":"volume","type":"long"}]}"""))
define stream StockStream (symbol string, price float, volume long);
```
<p style="word-wrap: break-word">The above configuration performs a default Avro mapping that generates an Avro message as an output ByteBuffer.</p>

<span id="example-2" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">EXAMPLE 2</span>
```
@sink(type='inMemory', topic='stock', @map(type='avro',schema.registry = 'http://localhost:8081', schema.id ='22',@payload("""{"Symbol":{{symbol}},"Price":{{price}},"Volume":{{volume}}}"""
)))
define stream StockStream (symbol string, price float, volume long);
```
<p style="word-wrap: break-word">The above configuration performs a custom Avro mapping that generates an Avro message as an output ByteBuffer. The Avro schema is retrieved from the given schema registry (localhost:8081) using the schema ID provided.</p>

## Sourcemapper

### avro *<a target="_blank" href="https://siddhi.io/en/v5.0/docs/query-guide/#source-mapper">(Source Mapper)</a>*

<p style="word-wrap: break-word">This extension is an Avro to Event input mapper. Transports that accept Avro messages can utilize this extension to convert the incoming Avro messages to Siddhi events.<br>&nbsp;The Avro schema to be used for creating Avro messages can be specified as a parameter in the stream definition.<br>&nbsp;If no Avro schema is specified, a flat avro schema of the 'record' type is generated with the stream attributes as schema fields.<br>The generated/specified Avro schema is used to convert Avro messages to Siddhi events.</p>

<span id="syntax" class="md-typeset" style="display: block; font-weight: bold;">Syntax</span>
```
@source(..., @map(type="avro", schema.def="<STRING>", schema.registry="<STRING>", schema.id="<STRING>", fail.on.missing.attribute="<BOOL>")
```

<span id="query-parameters" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">QUERY PARAMETERS</span>
<table>
    <tr>
        <th>Name</th>
        <th style="min-width: 20em">Description</th>
        <th>Default Value</th>
        <th>Possible Data Types</th>
        <th>Optional</th>
        <th>Dynamic</th>
    </tr>
    <tr>
        <td style="vertical-align: top">schema.def</td>
        <td style="vertical-align: top; word-wrap: break-word">This specifies the schema of the Avro message. The full schema used to create the Avro message needs to be specified as a quoted JSON string.</td>
        <td style="vertical-align: top"></td>
        <td style="vertical-align: top">STRING</td>
        <td style="vertical-align: top">No</td>
        <td style="vertical-align: top">No</td>
    </tr>
    <tr>
        <td style="vertical-align: top">schema.registry</td>
        <td style="vertical-align: top; word-wrap: break-word">This specifies the URL of the schema registry.</td>
        <td style="vertical-align: top"></td>
        <td style="vertical-align: top">STRING</td>
        <td style="vertical-align: top">No</td>
        <td style="vertical-align: top">No</td>
    </tr>
    <tr>
        <td style="vertical-align: top">schema.id</td>
        <td style="vertical-align: top; word-wrap: break-word">This specifies the ID of the Avro schema. This ID is the global ID that is returned from the schema registry when posting the schema to the registry. The schema is retrieved from the schema registry via the specified ID.</td>
        <td style="vertical-align: top"></td>
        <td style="vertical-align: top">STRING</td>
        <td style="vertical-align: top">No</td>
        <td style="vertical-align: top">No</td>
    </tr>
    <tr>
        <td style="vertical-align: top">fail.on.missing.attribute</td>
        <td style="vertical-align: top; word-wrap: break-word">If this parameter is set to 'true', a JSON execution failing or returning a null value results in that message being dropped by the system.<br>If this parameter is set to 'false', a JSON execution failing or returning a null value results in the system being prompted to send the event with a null value to Siddhi so that the user can handle it as required (i.e., by assigning a default value.</td>
        <td style="vertical-align: top">true</td>
        <td style="vertical-align: top">BOOL</td>
        <td style="vertical-align: top">Yes</td>
        <td style="vertical-align: top">No</td>
    </tr>
</table>

<span id="examples" class="md-typeset" style="display: block; font-weight: bold;">Examples</span>
<span id="example-1" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">EXAMPLE 1</span>
```
@source(type='inMemory', topic='user', @map(type='avro', schema .def = """{"type":"record","name":"userInfo","namespace":"user.example","fields":[{"name":"name","type":"string"}, {"name":"age","type":"int"}]}"""))
define stream UserStream (name string, age int );

```
<p style="word-wrap: break-word">The above Siddhi query performs a default Avro input mapping. The input Avro message that contains user information is converted to a Siddhi event.<br>The expected input is a byte array or ByteBuffer.</p>

<span id="example-2" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">EXAMPLE 2</span>
```
@source(type='inMemory', topic='user', @map(type='avro', schema .def = """{"type":"record","name":"userInfo","namespace":"avro.userInfo","fields":[{"name":"username","type":"string"}, {"name":"age","type":"int"}]}""",@attributes(name="username",age="age")))
define stream userStream (name string, age int );

```
<p style="word-wrap: break-word">The above Siddhi query performs a custom Avro input mapping. The input Avro message that contains user information is converted  to a Siddhi event.<br>&nbsp;The expected input is a byte array or ByteBuffer.</p>

<span id="example-3" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">EXAMPLE 3</span>
```
@source(type='inMemory', topic='user', @map(type='avro',schema.registry='http://192.168.2.5:9090', schema.id='1',@attributes(name="username",age="age")))
define stream UserStream (name string, age int );

```
<p style="word-wrap: break-word">The above Siddhi query performs a custom Avro input mapping. The input Avro message that contains user information is converted to a Siddhi event via the schema retrieved from the given schema registry(localhost:8081).<br>The expected input is a byte array or ByteBuffer.</p>

