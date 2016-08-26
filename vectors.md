# Vector Components
[emdata][1] files make use of several vector component systems, as used by [Harrington][2], [Hayt and Buck][3], and others.

All vector components used by emdata must be unambiguous. Wherever possible, first-class components are preferred (_i.e._, those components that correspond to coordinate systems). Some widely-used second-class components, such as _circular_ and _Ludwig III_ are considered to be universally understood, but they do not lend themselves to mathematical manipulation and transformation.

## Cartesian
The Cartesian coordinate system is discussed in [Coordinate Systems][4].

A fully-defined set of Cartesian vector data must contain the **x**, **y**, and **z** components.

## Cylindrical
The Cylindrical coordinate system is discussed in [Coordinate Systems][4].

A fully-defined set of Cylindrical vector data must contain the **ρ**, **φ**, and **z** components.

## Spherical
The Spherical coordinate system is discussed in [Coordinate Systems][4].

Except for far-field data, a fully-defined set of Spherical vector data must contain the **r**, **θ**, and **φ** components.

For far-field data, there is no **r** component, so far-field data must include the **θ** and **φ** components. However, if a set of far-field data contains _field_ values (_e.g._, fields in `V/m` rather than directivity in `dBi`), the effective _r_ coordinate must be defined within the dataset, as follows.

```javascript
// dataset object example
{
  "r": {
    "unit": "meter",
    "value": 100.0
  },
  ...
}
```

The actual magnitude must be used, not a statement describing how **r** was normalized.

## Circular
Circular vector components are unique to far-field data. They are related to the spherical vector components. Where possible, one should prefer spherical components.

_Equations to go here_

A fully-defined set of Circular vector data must include the **right-handed** and **left-handed** components (a.k.a. polarizations). These are defined in the emdata file as:
* `right`
* `left`

See [Wikipedia][99] for more details.

Another approach to cirular polarization is to describe attributes such as _axial ratio_, _semi-major_ and _semi-minor axes_, _ellipticity_, _handedness_, etc. Because these digress far from the first-class vector components, fully defining the quantity in a self-describing manner using this approach is overly complicated. Therefore, the emdata format does not define these as univerally understood.

## Ludwig III
Ludwig III components are unique to far-field data. They are described in depth in [Someone's IEEE paper][99]. They are related to the spherical vector components. Where possible, one should prefer spherical components.

_Equations to go here_

A fully-defined set of Ludwig III data must include the **co** and **cross** components  (a.k.a. polarizations). These are defined in the emdata file as:
* `l3Co`
* `l3Cross`

We do not use simply `co` and `cross` for Ludwig III, as we want users to be able to define their own (non-universal) references for these.

See [Wikipedia][99] for more details.

## Spherical Modes
Spherical modes are a valid way to represent far-field data, and are treated as vector components for the purposes of the emdata format. Spherical modes are discussed in depth in [Someone's IEEE paper][99].

A fully-defined set of spherical mode data must include _TBD_. These are defined in the emdata file as:
* _TBD_

See [Wikipedia][99] for more details.

# Transforms
It is possible to transform the vector component system to a local reference. For example, a far-field dataset in spherical coordinates may be rotated such that the poles are not aligned to the global _z_ axis. In this case, we require a means to specify the orientation of the vector data.

The emdata format uses quaternions to specify the orientation of vectors that do not align with the global axes. Quaternions are discussed in detail on [Wikipedia][99]. They are specified in the emdata file, within the dataset, as follows:
_TBD_


[1]:https://github.com/finitemobius/emdata
[2]:https://www.amazon.com/Time-Harmonic-Electromagnetic-Fields-Roger-Harrington/dp/047120806X
[3]:https://www.amazon.com/Engineering-Electromagnetics-William-Hayt/dp/0073380660
[4]:coordinate_systems.md
[5]:phasors.md
[99]:TBD