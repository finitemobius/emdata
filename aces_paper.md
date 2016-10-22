# A Proposed Common Format for Electromagnetics Data Interchange
Jason R. Miller

DOI: [10.1109/ROPACES.2016.7465399](http://dx.doi.org/10.1109/ROPACES.2016.7465399)

## Abstract
The lack of a common data interchange format for CEM is hampering progress, causing duplicate workloads and opening the door for error. We propose a standard format based on JSON for flexible data interchange. The format is designed to be self-describing, extensible, open, and freely available.

## Background
The computational electromagnetics (CEM) software landscape is vast and variegated. Rapid advances in algorithms and implementations have made processing more efficient. More attention is given to the user experience and front-end design. However, one facet of our profession has been ignored for quite some time: exchanging data between different software packages.

The lack of a common data interchange format is hampering progress. Developers are relegated to writing import routines for every software package and file format that their users can imagine. On the other side, users are relegated to waiting until a sufficient portion of a software’s user base requests a particular file format importer before they get their wish. Often, this results in users writing their own conversion scripts.

In each of these cases, the onus is on the developer or user to make sure the import and conversion routines keep up with changes to both the input and output software packages. All of this duplicated development makes for an inefficient use of everyone’s time. This also results in N-squared software conversion and import routines. Overall, this limits productivity and increases the opportunity for errors.

Software developers often produce tutorials describing how to use data from one software package in another software package. There are actually two problems being addressed in these tutorials: how to import a certain data type from another software package and how to use that data type in this software package. Again, we see unnecessary work on the part of the user. The user and the software vendor should only have to focus on proper usage of an imported data type, not the import methodology itself.

Take the example of using measured EM field data as a Huygens source in a simulation package. No matter where the field data came from, they are still field data. What matters is the proper usage of that field data to create a valid source. That is what we want our users and vendors to focus on, rather than learning and troubleshooting the data import routine.

## Historical Solutions
This author is not the first to propose a solution to this problem. However, past solutions have suffered from three main drawbacks. First, these formats have generally not been extensible. Second, these formats have not been self-describing or flexible. Third, these formats have not been broadly accepted.

Extensibility is key for any data interchange format. In the past, proposed common formats have typically been a rigidly-defined set of delimited columns. Comma-delimited, space-delimited, and column-width-delimited text files are very popular. Extensibility for these formats has been limited to header rows and keywords. The result has been confusing headers that define column and sort orders, with narrow flexibility. Every new design deviation results in a new header line, which quickly becomes unsustainable.

In addition to being extensible, a data interchange format should be self-describing and flexible. The user should not need a priori knowledge of the data file structure and contents to make use of the file. The importing software should be able to tell what data are in the file, where the data begins and ends, what units are in use, etc. More automation and fewer opportunities for error are necessary for efficient handling of large datasets.

Partly as a consequence of a lack of extensibility and self-description, each software package or user organization has its own preferred “common” data format. Deviations between preferred formats include sort order, units, and [coordinate references][3]. If one user’s “common” data format does not support another user’s preferred data type, unit, etc., both users will end up choosing different formats. It is clear that broad acceptance requires buy-in from both users and software developers.

## Proposed Solution
A truly useful common data format must adhere to five criteria.
*	It must be self-describing.
*	It must be extensible.
*	It must be machine-readable.
*	It must be human-readable, either directly or through a simple act such as decompression.
*	It should be based on an existing, open format.

The last point is perhaps not self-evident. By starting a well-known format, most of the work is already done for us. This includes import and export functionality. Using an open format frees us from licensing concerns.

There are a few formats that meet the above criteria. The most popular are XML (Extensible Markup Language), JSON (JavaScript Object Notation), and YAML (YAML Ain't Markup Language).

After much research and experimentation, we settled on JSON as the best candidate for a common format. It requires very little in the way of annotation, with simple marks used to represent objects, arrays, etc. JSON is also designed for serializing data structures. This makes it very easy to represent arrays of objects, nested structures, and arbitrary data structures.

JSON is [well-documented][1], and there are [implementations for over 60 programming and scripting languages][2]. It can also be used as object literals in JSON and dictionary literals in Python, and it resembles table constructors in Lua and anonymous types in C#. Anyone familiar with these languages will be able to quickly understand and begin using JSON.

## Using JSON for CEM
The essential idea that we are promoting in using JSON for CEM is providing each column as a key-value pair, with the value being a one-dimensional array. Each column’s array is ordered such that the nth element corresponds to the nth element in all the other columns in the data set.

Column keys are parse-able and describe, at a minimum, the column name, type, and unit. A simple regular-expression parser can determine what type of data, in what units, are in each column.

Perhaps the best means to explain how JSON would be used in this context is an example. The following code block shows a sample of a data structure for a near-field data set. Note that this is not a complete data set in a finalized format; it is an example of using JSON for CEM.

```
{
  "type": "near field",
  "data": [
    {
      "frequency": {
        "unit": "MHz",
        "value": 100.0
      },
      "data": [
        {
          "quantity": "coordinate",
          "component": "x",
          "units": "meters",
          "data": [0.1, 0.2, 0.3, 0.4, …]
        }, {
          "quantity": "electric field",
          "vector_component": "x",
          "phasor_component": “amplitude",
          "units": "V/m",
          "data": [12.7, 10.3, 13.2, 11.5, …]
        }, …
      ]
    }, …
  ],
  "source": "measured at our outdoor range"
}
```

Here, we see how columns are notionally defined. We also see how parameters can be defined. Column names, units, and other metadata can be arbitrary. For example, we could add a ‘meets threshold’ column, containing ‘true’ and ‘false’ entries. We could also add a ‘source’ key, with the value describing whether these data were simulated, measured, calculated, etc.

Even though names and values are arbitrary, there must be a common lexicon for commonly-used data types, units, etc. in order for the data to truly be useful when exchanged between disparate software and organizations. The purpose of defining a standard format for CEM above and beyond the JSON specification itself is to define this universally-agreed-upon lexicon. Any column that adheres to the standard should be available in any software package that imports the file. Custom columns and parameters may not be understood by the software, but they can still be available for the user to view and manipulate.

Further, we can extend this format to store multiple data sets in a single file, by placing data sets within arrays. The user would ultimately be presented with a list of data sets to choose from for processing, referred to by unique, human-readable parameters rather than, for example, line numbers.

## Promoting Adoption
In an effort to promote adoption of this new format, we are sharing the format description with the community using an open license and invite community participation in its development. The format description consists primarily of a grammar and a universal lexicon. It may also consist of example files and parsers, if the community wishes to contribute these.

It is our hope that allowing all the stakeholders to participate in the formation of this standard results in something useful for the entire community. The computer science community has made incredible progress in this arena, and it is time for our community to reap the benefits.

[1]:http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf
[2]:http://www.json.org/
[3]:coordinate_systems.md