# another-json2xml
 
## What is another-json2xml

another-json2xml is another JavaScript package for converting json to xml. We do usually use it when we access a soap service.

For more information, refer to 
https://www.npmjs.com/package/another-soap

## Install

``` CMD
npm install another-json2xml --save
```

## Usage

``` Typescript
import { XmlDef } from 'another-json2xml'

const xmlDef = new XmlDef()
xmlDef.method = "GetData"
// anotherSoap.defaultEnt = ""
// anotherSoap.tem = ""
// anotherSoap.methodNs = "m"
// anotherSoap.methodNsUrl = "http://tempurl.org/"
xmlDef.bodyEntities = [
  {
    name: "sessionId",
    object: "XXXXX",
    // ns: "ent2",
    // nsUrl: "http://tempurl.org/"
  },
  {
    name: "requestData",
    // ns: "Foo",
    // nsUrl: "http://schemas.datacontract.org/2004/07/Foo.Entities",
    object: {
      foo: "foo",
      bar: "bar>",
      empty: "",
      tata: null,
      bars: ["bar1", ""],
      numbers: [1, 2],
      booleans: [true, false],
      cars: [
        {
          car: {
            name: "car1",
            brand: "Volkswagen"
          },
        },
        {
          car: {
            name: `car2<>&\"'<>&\"'`,
            brand: "BMW"
          },
        },
      ],
    },
  },
]

const xml = xmlDef.toXML()

console.log(xml)
```


Output

``` XML
<?xml version="1.0" encoding="UTF-8" ?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:tem="http://tempurl.org/"
  xmlns:ent="http://schemas.datacontract.org/2004/07/ent.Entities"
  xmlns:arr="http://schemas.microsoft.com/2003/10/Serialization/Arrays">
  <soapenv:Header/>
  <soapenv:Body>
    <tem:GetData >
      <tem:sessionId>XXXXX</tem:sessionId>
      <tem:requestData>
        <ent:foo>foo</ent:foo>
        <ent:bar>bar&gt;</ent:bar>
        <ent:empty/>
        <ent:tata i:nil="true"/>
        <ent:bars>
          <arr:string>bar1</arr:string>
          <arr:string/>
        </ent:bars>
        <ent:numbers>
          <arr:number>1</arr:number>
          <arr:number>2</arr:number>
        </ent:numbers>
        <ent:booleans>
          <arr:boolean>true</arr:boolean>
          <arr:boolean>false</arr:boolean>
        </ent:booleans>
        <ent:cars>
          <ent:car>
            <ent:name>car1</ent:name>
            <ent:brand>Volkswagen</ent:brand>
          </ent:car>
          <ent:car>
            <ent:name>car2&lt;&gt;&amp;&quot;&apos;&lt;&gt;&amp;&quot;&apos;</ent:name>
            <ent:brand>BMW</ent:brand>
          </ent:car>
        </ent:cars>
      </tem:requestData>
    </tem:GetData>
  </soapenv:Body>
</soapenv:Envelope>
```
