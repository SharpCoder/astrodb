# Astrodb
This collection of celestial objects is built on a number of datasets. What I aim to provide with this project is a normalized set of identifiable objects which you can easily  integrate into apps and software projects. It's easy to find a bunch of datasets, but they are all defined in different formats. I wanted to bring together many common datasets, normalize them, and create one dataset to rule them all.

It is wroth noting that the information contained within this dataset is probably not up-to-par for any scientific endeavor. The normalization process is fast and loose, but will provide a great starting point for projects which are not "mission critical".

## The data
All celestial databases are stored in the `data` folder. It is comprised of many different catalogs of various types and features. Each catalog is included with its respective input as well as a readme which defines the shape of the data. 

## The output
The final, sanitized output can be found in the file `stardb.pipe`

## The files
There are two primary notebooks.
 - Astro Databases
 - Normalization
 
### Astro Databases
This notebook defines the normalized shape of data. Each catalog has some common fields associated as well as some nuanced fields. Some catalogs even share the same nuacned field. in an effort to bring it all together in roughly the same shape, that's what the `Astro Databases` notebook is all about.
 
### Normalization
This is the notebook which normalizes all data into a final format. It includes logic for deduplicating entries, normalizing constellation information, selecting the best-fit name candidate across enteries, and so on.
 
## Concepts
In astronomy, celestial objects are encoded based on their position relative to grenwich at a particular instant. These numbers are stored as arc degrees and time units - specifically called Right Ascension and Declination. Every celestial catalog will have various ways to represent `ra` and `dec`. Sometimes it is `ra hours, ra minutes, ra seconds` and `dec degrees, dec minutes, dec seconds`. Sometimes it is just `ra` and `dec`. Sometimes the sign will be in its own column, sometimes not. There are many different ways to encode the position. Normalization of this data happens in `Astro Databases`.
 
In order to de-dupe all databases with each other, I've devised a `dup_id` field. If two or more rows share the same `dup_id` then they are effectively duplicates no matter what the numbers say specifically.
 
| Field              | Description                                                 |
|--------------------|-------------------------------------------------------------|
| ra_h               | Right ascension hours (positional coordinate)               |
| ra_m               | Right ascension minutes (positional coordinate)             |
| ra_s               | Right ascension seconds (positional coordinate)             |
| dec_deg            | Declination degrees (positional coordinate)                 |
| dec_m              | Declination minutes (positional coordinate)                 |
| dec_s              | Declination seconds (positional coordinate)                 |
| names              | Comma separated list of name candidates                     |
| designation        | The object type (galaxy, star, etc)                         |
| catalog            | The catalog which the information comes from                |
| source             | The exact uri which has the original data                   |
| mag                | visual spectrum magnitude                                   |
| ngc_id             | the NGC catalog id (if applicable)                          |
| surface_brightness | The brightness of the object compensated for size           |
| b_mag              | b_u magnitude (brightness indicator)                        |
| v_mag              | visual spectrum magnitude                                   |
| j_mag              | another kind of brightness indication                       |
| M                  | Messier catalog id (if applicable)                          |
| NGC                | duplicate of ngc_id                                         |
| IC                 | IC catalog id                                               |
| dup_id             | Unique identifier grouping together duplicate entries       |
| constellation      | The constellation which the object is found (if applicable) |
| classifiers        | Additional labels applied to some objects                   |
| descriptors        | Visual descriptors applied to some objects                  |
| notes              | Any notes on the object                                     |
| remnant_type       | unknown                                                     |
| HD_ID              | Harvard catalog ID                                          |
| SAO_ID             | SAO catalog ID                                              |
| FK5_ID             | FK5 ID (sometimes includes common names)                    |
| DM Ident           | Additional notes from one specific catalog                  |
| bv_mag             | blue light spectrum magnitude                               |
| ub_mag             | ultraviolet light spectrum magnitude (I think)              |

## Known Bugs
I am aware of at least one "bug". My sanitization step which tries to reconcile abbreviations with the constellations mis-categorized at least one named celestial object. As a result, we are presented with the lovely naming convention of NGC 6357 which ends up becoming "The War Andromeda Peace Nebula". There are probably other examples of this which I have not yet discovered. Work to mitigate that is in the works.

## Databases

The following databases are used to create this derivative work.

### OpenNGC Catalog
The OpenNGC catalog is a lovely selection of celestial objects. It is licensed under the Attribution-ShareAlike 4.0 International license and was compiled by Mattia Verga. You can find the full source of the original catalog here: https://github.com/mattiaverga/OpenNGC

### IAU Star Database
This collection of named stars provides a great resource for reconiling named candidates. Many stars have silly numerical names, but the IAU Star Database was instrumental in identifying the common colloquialisms. The original source can be found here: http://www.pas.rochester.edu/~emamajek/WGSN/IAU-CSN.txt and is released under the Creative Commons Attribution license.

### SAC81
These folks are amazing and have created a truly wonderful collection of celestial objects. I am not sure what license they release their data under, however, you can view the original source on their website: https://www.saguaroastro.org/sac-downloads/

### SNRS
The supernova remnant dataset comes from an FTP server that I found through google. Upon inspecting their folder structure more closely, I was unable to find much information about who compiled this list. But the original source can be found here: ftp://cdsarc.u-strasbg.fr/0/cats/VII/284

### Yale Bright Stars Catalog
The well-known Yale Bright Stars Catalog is the source of many stars and their magnitudes. This particular project utilizes the bsc5 catalog and you can find the original source here: http://tdc-www.harvard.edu/catalogs/bsc5.html


## License

In an effort to propagate the most restrictive downstream license, I have chosen to adopt the Attribution-ShareAlike 4.0 International license.