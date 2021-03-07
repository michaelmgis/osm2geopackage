![osmdata.xyz logo](https://github.com/michaelmgis/osmdata.xyz/blob/master/logos/osmdata_logo_power_wide_300dpi.png)

# osmdata.xyz | global osm extracts
This project provides global data extracts based on [OpenStreetMap data](https://planet.openstreetmap.org/) as [GeoPackages](https://www.geopackage.org/). Each extract represents its related [primary feature](https://wiki.openstreetmap.org/wiki/Map_Features) respectively key value regarding the [OpenStreetMap project](https://www.openstreetmap.org/). Every GeoPackage contains the three types of geometries: point, line and polygon. For each primary feature all prepared tags are always contained in the same way.

## Extracts are available on
https://download.osmdata.xyz/

In a monthly cycle new extracts are provided. The first Planet Dump of each month from openstreetmap.org will be available 10 days later as it takes a while for the data to be processed. Every odd month, Buildings will be updated.

Projection of the geodata: WGS 84 | EPSG 4326 | https://spatialreference.org/ref/epsg/4326/

## Why
OpenStreetMap (OSM) offers an amazing collection of data. The information contained provides many possibilities to better understand the whole world, e.g. with the use of a geographic information system (GIS). There are many tools to create small extracts from the OSM data: overpass-turbo (API) or other tools in QGIS/ArcGIS. A bigger challenge is the creation of ready to use GIS-compatible data sets from OSM, which cover whole countries, continents or even the whole world.

osmdata.xyz is my hobby and absolutely non-commercial. I'm happy to share open data, knowledge and insights.

## Utilized tools to create extracts
Workflow: https://github.com/michaelmgis/osmdata.xyz/tree/master/workflow_scripts

- osmium --> https://osmcode.org/osmium-tool/
- gdal / ogr2ogr --> https://gdal.org/programs/ogr2ogr.html

Archive | old [workflows](https://github.com/michaelmgis/osmdata.xyz/tree/master/archive)
- imposm3 --> https://github.com/omniscale/imposm3 (see since 20190805)
- PostGIS / PostgreSQL --> https://postgis.net/
- osm2pgsql --> https://wiki.openstreetmap.org/wiki/Osm2pgsql)

## Data basis
- primary (map) features --> https://wiki.openstreetmap.org/wiki/Map_Features
- planet file as osm.pbf --> https://planet.openstreetmap.org/

## Recent improvements and changes

- 03.2021
  - BIG UPDATE will be implemented in March - adressing [Issue #25](https://github.com/michaelmgis/osmdata.xyz/issues/25): Switching from imposm/PostgreSQL to gdal/ogr2ogr for processing. Data model stays the same.
  - Adding hstore field "other_tags" which contains all keys and tags who are related to the primary mapfeatues but not listed as main keys/tags.
- 02.2021
  - adressing [Issue #16](https://github.com/michaelmgis/osmdata.xyz/issues/16) --> adding tents
- 01.2021
  - adressing [Issue #23](https://github.com/michaelmgis/osmdata.xyz/issues/23)
  - adding a new extract to the [workflow](https://github.com/michaelmgis/osmdata.xyz/blob/master/workflow_scripts/99_public_transport_with_relations)  [public_transport_with_relations_EPSG4326.zip](https://download.osmdata.xyz/data/public_transport_with_relations_EPSG4326.zip)
- 10.2020
  - adding osm_id as key [Issue 21](https://github.com/michaelmgis/osmdata.xyz/issues/21); more information at [imposm docs](https://imposm.org/docs/imposm3/latest/mapping.html#id)
- 05.2020
  - Providing ZIP-Files as Downloads. Switching back from 7zip to ZIP for better compatibility and usability.
- 04.2020
  - Adressing [Issue 18](https://github.com/michaelmgis/osmdata.xyz/issues/18) for more compatibility
  - colon (:) to underline in attribute names and renaming "natural" to "natural_attribute".
  - ~~Adressing [Issue 19](https://github.com/michaelmgis/osmdata.xyz/issues/19) by swithing to [7zip-archive](https://www.7-zip.org/download.html) format.~~
- 01.2020
  - [docker workflow](https://github.com/michaelmgis/osmdata.xyz/tree/master/docker)
- 10.2019
  - definition of geometrytype improve reading the content of a GeoPackage with QGIS
  - new tags: internet_access, wifi
- 08.2019
  - all geometries of each map feature are stored in one GeoPackage
  - new processing chain - imposm3 is used since the extracts from 20190805 - see [workflow_scripts](https://github.com/michaelmgis/osmdata.xyz/tree/master/workflow_scripts).

## Approach and statistics
The [processing chain](https://github.com/michaelmgis/osmdata.xyz/tree/master/workflow_scripts) published here is designed to reduce storage consumption as much as possible. Each extract based on the primary map feature (e.g. building) is created individually. Intermediate products are deleted to save storage space.

**Example 1 - current workflow: "building" as extract with the highest storage usage**: A maximum of 608 GB of storage space is required to create the largest data set "building". All other primary map features require significantly less storage. 

|Type|Size|
| ------------- | ------------- |
|all PBF files|50,00 GB|
|impcache|33,50 GB|
|PostGIS database|234,40 GB|
|Building GPKG|290,00 GB|
|**Sum**|**607,90 GB**|


**Example 2 - entire global data set is stored in a database - extract of buildings**: A maximum of 924 GB of storage is required to create the largest data set "building".

|Type|Size|
| ------------- | ------------- |
|PBF|47,00 GB|
|impcache|92,00 GB|
|PostGIS database|495,00 GB|
|Building GPKG|290,00 GB|
|**Sum**|**924,00 GB**|


**Conclusion**: If storage space plays a role, then the approach published here is recommended. If there is enough memory, you can skip the step of splitting the PBF files (03_osm_filter) and just transfer everything to the database.

## Copyright and License 
OpenStreetMap© is open data, licensed under the [Open Data Commons Open Database License](https://opendatacommons.org/licenses/odbl/) (ODbL) by the [OpenStreetMap Foundation](https://osmfoundation.org/) (OSMF). 
https://www.openstreetmap.org/copyright/en

## Happy about feedback
Let me know, if you are happy or what could be improved.
Please post an issue or write to hello@osmdata.xyz
