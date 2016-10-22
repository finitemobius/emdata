# Data Types
This file describes the data types that are universally understood by implementations of `emdata`.

## Overview
The top level of an [emdata object][2] must define the `type` of data it contains. Any implementation of the emdata format will recognize the following dataset types:
* Near Fields
* Far Fields
* Radar Cross-Section
* Currents

This document is a high-level description of each type. Details on the acceptable *quantities*, *units*, [coordinate systems][1], etc. are documented separately.

## Near Fields
*Near Fields* consist of electric and/or magnetic fields.

There must be enough [coordinate][1] columns for each sample point to be completely defined. (This is typically three [coordinates][1] for 3-space.)

There must be at least one `electric field` or `magnetic field` *quantity* column in each dataset.

Near fields are both vectors and phasors. As such, all `electric field` or `magnetic field` columns must have a `vectorComponent` and `phasorComponent` key. (In the case of time-domain data, the `phasorComponent` will almost always be `magnitude`.)

Near fields are specified at the top level of the object as:
```javascript
"type": "near field"
```

## Far Fields
*Far fields* are defined as the *electric* far field. This is also commonly known as a *radiation pattern*, *far-field pattern*, *gain*, or *directivity*.

There must be enough [coordinate][1] columns for the radiation direction of each sample point to be completely defined. This is typically two [coordinates][1], *theta* and *phi*, for 3-space, as *r* is taken to be infinity. In the case when far fields are described as electric field values (e.g., FEKO FFE files), one is not required to list *r* as a [coordinate][1] column. Instead, one should speficy *r* at the top level of the dataset.

Far fields are both vectors and phasors. As such, all gain/directivity columns must have a `vectorComponent` and `phasorComponent` key. Vector components will typically be `theta` and `phi`, though it is possible to represent far fields in other orthogonal components. (These are discussed in depth [separately][3].)

Far fields are specified at the top level of the object as:
```javascript
"type": "far field"
```

It is also possible to represent far fields as [Spherical Modes][4], discussed separately.

## Radar Cross-Section
Radar cross-sections (RCS) are very similar to far fields. However, the existence of an incident field and monostatic and bistatic RCS necessitate a separate description.

There must be enough [coordinate][1] columns for the scattered direction of each sample point to be completely defined. This is typically two [coordinates][1], *theta* and *phi*, for 3-space, as *r* is taken to be infinity. In the case when far fields are described as electric field values (e.g., FEKO FFE files), one is not required to list *r* as a [coordinate][1] column. Instead, one should speficy *r* at the top level of the dataset.

Radar cross-sections are both vectors and phasors. As such, all RCS columns must have a `vectorComponent` and `phasorComponent` key. Vector components will typically be `theta` and `phi`, though it is possible to represent far fields in other orthogonal components. (These are discussed in depth [separately][3].)

RCS datasets must have the key `rcsType` at the dataset level, with the value `monostatic` or `bistatic`. For both types, the incident field vector and phasor components must be fully defined. For bistatic RCS, the incident field direction must also be defined.

Radar cross-sections are specified at the top level of the object as:
```javascript
"type": "rcs"
```

A monostatic RCS is specified at the dataset level as:
```javascript
"rcsType": "monostatic",
"incidentField": [
  {
    "vectorComponent": "theta",
    "phasorComponent": "magnitude",
    "unit": "V/m",
    "value": 1.0
  },
  {
    "vectorComponent": "theta",
    "phasorComponent": "phase",
    "unit": "degrees",
    "value": 0.0
  },
  {
    "vectorComponent": "phi",
    "phasorComponent": "magnitude",
    "unit": "V/m",
    "value": 0.0
  },
  {
    "vectorComponent": "phi",
    "phasorComponent": "phase",
    "unit": "degrees",
    "value": 0.0
  }
]
```

A bistatic RCS is specified at the dataset level as:
```javascript
"rcsType": "bistatic",
"incidentField": [
  {
    "vectorComponent": "theta",
    "phasorComponent": "magnitude",
    "unit": "V/m",
    "value": 1.0
  },
  {
    "vectorComponent": "theta",
    "phasorComponent": "phase",
    "unit": "degrees",
    "value": 0.0
  },
  {
    "vectorComponent": "phi",
    "phasorComponent": "magnitude",
    "unit": "V/m",
    "value": 0.0
  },
  {
    "vectorComponent": "phi",
    "phasorComponent": "phase",
    "unit": "degrees",
    "value": 0.0
  }
],
"incidentDirection": [
  {
    "component": "theta",
    "unit": "degrees",
    "value": 30.0
  },
  {
    "component": "phi",
    "unit": "degrees",
    "value": 310.0
  }
]
```

A note on incident field magnitudes and RCS data: Even if one is generating an RCS that solely consists of far-field RCS quatities (_e.g._, dBsm or sm) and not fields (_e.g._, V/m), the incident field magnitude is still required, in order to properly define the field polarization. If the original incident field is unknown or undefined (_i.e._, the only data that exist are RCS data in dBsm or sm), one should use normalized or unit vector magnitudes that fully describe the incident field polarization.

## Currents
*Currents* can be electric or magnetic currents or current density (or _equivalent_ currents or current density). Whether the currents described in the file are line/wire currents, surface current density, or volume current density is determined by the units in columns describing the current magnitude. Therefore, different current types should not be combined in a single dataset.

There must be enough [coordinate][1] columns for each sample point to be completely defined. (This is typically three [coordinates][1] for 3-space.)

There must be at least one `electric current` or `magnetic current` *quantity* column in each dataset.

Currents are both vectors and phasors. As such, all `electric current` or `magnetic current` columns must have a `vectorComponent` and `phasorComponent` key. (In the case of time-domain data, the `phasorComponent` will almost always be `magnitude`.)

Currents are specified at the top level of the object as:
```javascript
"type": "current"
```

Currently (no pun intended), there is no means to map currents to geometry elements. The user may choose to add a column describing the wire segment or triangle, but this is not considered universally understood.

[1]:coordinate_systems.md
[2]:object_schema.md
[3]:vectors.md
[4]:spherical_modes.md