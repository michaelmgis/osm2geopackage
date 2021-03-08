# Readme
The files are supposed to run on docker. build, run and exec

This workflow refers to the old scripts before march 2021. See archive: [https://github.com/michaelmgis/osmdata.xyz/tree/master/archive/Version_2_imposm](https://github.com/michaelmgis/osmdata.xyz/tree/master/archive/Version_2_imposm)

## building the docker container:

```
docker build -t eg_postgresql12 .
 ```
## starting the container
We run it with a local volume to store the resulting files in. the port number might be interesting if you want to use postgis afterwards. But be aware: the data in Postgis will be gone after the execution of getting osmdata and exporting it as gpkg:

```
docker run --volume aLocalPath:/home/osmdata/gpkg --rm -P -p 0.0.0.0:55432:5432 -d --name pg_osmdata eg_postgresql12
```
## running the osmdata process
This script will extract osmdata from a desired path. Currently it runs with "Bremen" latest. Just change the strings in the file Dockerfile and in the import_osm.sh file accordingly your desired output.

```
docker exec -it pg_test /home/osmdata/pbf/import_osm.sh
```

if you want to push the gpkg to a ftp server use:
```
docker exec -it pg_test /home/osmdata/pbf/import_osm.sh USERNAME FTPSERVER password
```
