# Object Schema
This file describes the JSON schema of *emdata*.

## EMData Object
The entire EMData data set is contained in a single JSON object.

The EMData object must have a type. Each EMData object should only contain one type of data. (*e.g.*, Near fields should not be mixed with far fields.)

Universally understood types are documented [separately][2]. Other, custom types can be used, but they will not be universally recognized. In these cases, data sets will not necessarily be able to be validated or operated on by CEM software.

The EMData object must contain a `data` array. This array is a set of one or more *dataset* objects.

```javascript
// EMData object example
{
  "type": "near field",
  "data": [
    // dataset objects
  ],
  "source": "measured at our outdoor range"
}
```

The EMData object can contain any number of other arbitrary keys and values. If these are not understood by software, they will simply be ignored. Useful examples of these might include:
* name - The name of the antenna
* platform - The name of the platform the antenna was measured or simulated on
* date
* author
* frequency - If all data sets share a frequency, it could be defined here
* position - The 3-D [coordinate][1] position of the antenna center point (useful for 3-D plotting)
* orientation - A quaternion (for example) describing how the source was oriented
* source - Where the data were acquired or how they were generated

## Dataset Object
A *dataset* object contains one entire set of data for one scenario — for example, at a specific frequency or time.

A dataset must contain a key that uniquely identifies it from all other datasets in the EMData object — for example, `frequency` or `time`. This key should contain either a primitive identifier or an array of key-value pairs. If the value is a physical quantity (like a frequency or time), it should be an object containing `unit` and `value` keys.

A dataset must contain a `data` array. This array is a set of one or more *column* objects.

```javascript
// dataset object example
{
  "frequency": {
    "unit": "MHz",
    "value": 100.0
  },
  "data": [
    // column objects
  ]
}
```

## Column Object
A *column* object must contain a `quantity` key. This is what the column is describing. Universally-understood quantities are documented separately.

A column object must contain a `data` array. This array is a set of one or more primitives, almost always numeric. All columns in a dataset must have the same data length. Each column’s data array is ordered such that the *n*th element corresponds to the *n*th element in all the other columns in the data set. Not every dataset needs to have matching columns, but algorithms tend to behave more predictably when they do.

Depending on the quantity, certain other keys may be required.

Independent variables — such as spatial [coordinates][1], time, *ωt* phase — typically only need a `component` and `unit`.

Dependent variables are typically vectors and/or phasors, so they require more keys to describe the components. The keys required for different quantities are documented separately.

```javascript
// column object example: independent variable
{
  "quantity": "coordinate",
  "component": "x",
  "unit": "meters",
  "data": [
    // numerics
  ]
}
// column object example: dependent variable
{
  "quantity": "electric field",
  "vectorComponent": "x",
  "phasorComponent": "magnitude",
  "unit": "V/m",
  "data": [
    // numerics
  ]
}
```
[1]:coordinate_systems.md
[2]:data_types.md