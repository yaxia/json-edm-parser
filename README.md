# json-edm-parser
This is a JSON streaming parser for node.js. It will handle the Entity Data Model (EDM) types to be compatitable with odata.

When you use JSON to represent an odata entity, a number without a decimal point in the JSON will have Edm.Int32 by default and 
will have Edm.Double if there are non-zero digits after the decimal point. However, if the value is set to *.0, 
Most JSON parsers will take it as an integer. To keep the type information, this parser will add an additional member "<property>@odata.type": "Edm.Double" 
to the object.

## Install

```shell
npm install json-edm-parser
```

## Usage

```Javascript
var Parser = require('json-edm-parser');

var p = new Parser();
p.write('{ "doubleNumber": 1.0 }');

// You will get {doubleNumber: 1, 'doubleNumber@odata.type': 'Edm.Double'}
p.onValue = function (value) {
  // Deal with the value
};
```