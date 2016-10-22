# emdata
Electromagnetic Data Interchange Format

The **emdata** format is a standard format for flexible data interchange. The format is designed to be self-describing, extensible, open, and freely available. An emdata file is a valid JSON file.

The emdata format was born of [Jason R. Miller][9]'s presentation and accompanying paper for the 2016 IEEE [ICWITS][11]-[ACES][10] conference, titled *[A Proposed Common Format for Electromagnetics Data Interchange][1]*.

This project contains the specification for the emdata format, as well as some example emdata files. A separate project will be maintained with a sample implementation.

## Contents
1. [Background][1]
1. [Object Schema][2]
1. [Data Types][3]
1. [Coordinate Systems][4]
1. [Vector Components][5]
1. [Phasor Components][6]
1. [Units][7]
1. [Spherical Modes][12]

## License
This project is licensed under [The MIT License][8].

[1]:aces_paper.md
[2]:object_schema.md
[3]:data_types.md
[4]:coordinate_systems.md
[5]:vectors.md
[6]:phasors.md
[7]:units.md
[8]:LICENSE
[9]:https://goo.gl/24F3OA
[10]:http://www.aces-society.org/
[11]:http://www.ieeeaps.org/
[12]:spherical_modes.md