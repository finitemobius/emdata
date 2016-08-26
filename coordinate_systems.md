# Coordinate Systems
[emdata][1] files use the Cartesian, cylindrical, and spherical coordinate systems as used by [Harrington][2], [Hayt and Buck][3], and others. Software that implements [emdata][1] will recognize these coordinate systems according to the following descriptions. These coordinate systems apply to _coordinate_ and _vector component_ columns.

Please note that vector components are not limited to coordinate system references. For example, right-hand and left-hand circular are valid vector components that are not valid coordinate components. (They are related to the spherical components, but are not themselves coordinates.) Vector components are discussed [separately][7].

## Cartesian
The Cartesian, or _rectangular_, coordinate system is defined by the _x_, _y_, and _z_ axes.

This system is right-handed, in that the following unit-vector cross-products are valid:
* **_x_** × **_y_** = **_z_**
* **_z_** × **_x_** = **_y_**
* **_y_** × **_z_** = **_x_**

These are referenced in the emdata file as:
* `x`
* `y`
* `z`

See [Wikipedia][4] for more details.

## Cylindrical
The cylindrical coordinate system is defined by the _ρ_ (_rho_), _φ_ (_phi_), and _z_ axes. _Phi_ is constrained between 0° and 360° (0ʳ and 2πʳ). 

This system is right-handed, in that the following unit-vector cross-products are valid:
* **_ρ_** × **_φ_** = **_z_**
* **_z_** × **_ρ_** = **_φ_**
* **_φ_** × **_z_** = **_ρ_**

These are referenced in the emdata file as:
* `ρ` or `rho`
* `φ` or `phi`
* `z`

See [Wikipedia][5] for more details.

## Spherical
The spherical coordinate system is defined by the _r_, _θ_ (_theta_), and _φ_ (_phi_) axes. _Phi_ is constrained between 0° and 360° (0ʳ and 2πʳ). _Theta_ is constrained between 0° and 180° (0ʳ and πʳ).

This system is right-handed, in that the following unit-vector cross-products are valid:
* **_r_** × **_θ_** = **_φ_**
* **_φ_** × **_r_** = **_θ_**
* **_θ_** × **_φ_** = **_r_**

These are referenced in the emdata file as:
* `r` or `ρ` or `rho`
* `θ` or `theta`
* `φ` or `phi`

See [Wikipedia][6] ("as commonly used in physics") for more details.

## Other Systems
Other coordinate systems may be supported by software utilities, but the systems above shall be understood universally.

## Coordinates and Vector Components
Coordinate and vector components for a single dataset don't necessarily need to use the same coordinate systems. For example, a far-field pattern expressed in spherical coordinates may have columns defining _x_, _y_, or _z_ polzarizations.

[1]:https://github.com/finitemobius/emdata
[2]:https://www.amazon.com/Time-Harmonic-Electromagnetic-Fields-Roger-Harrington/dp/047120806X
[3]:https://www.amazon.com/Engineering-Electromagnetics-William-Hayt/dp/0073380660
[4]:https://en.wikipedia.org/wiki/Cartesian_coordinate_system#Three_dimensions
[5]:https://en.wikipedia.org/wiki/Cylindrical_coordinate_system
[6]:https://en.wikipedia.org/wiki/Spherical_coordinate_system
[7]:vector_components.md