# BMVI Data-Run Datasets
Event Homepage: [BMVI Data-Run](https://www.bmvi.de/SharedDocs/DE/Termine-mFUND/bmvi-data-run.html)
Date: 22-23 March 2019

This repository contais multiple datasets prepared for the BMVI Data-Run to be used by the participants. 

Single Dataset Download: https://uni-bonn.sciebo.de/s/IGcOi2vy1lSyihE/download (63mb, 454,835 triples)

# Linked Data
![alt text](https://uni-bonn.sciebo.de/index.php/apps/files_sharing/ajax/publicpreview.php?x=1920&y=644&a=true&file=extended_lod_cloud.png&t=K7gmxdrRBIvwsFN&scalingup=0)


# Dataset Information

| Dataset  | Legal | Found via Portal   |  Data Provider | 
| ------------- | ------------- | ------------- | ------------- |
| alkis_liegenschaften.nt  |  [dl-de/by-2-0](https://www.govdata.de/dl-de/by-2-0) | [govdata.de](https://www.govdata.de/)   |  City of Hamburg | 
| bahnhoefe.nt  | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) OR [ODbL](https://opendatacommons.org/licenses/odbl/index.html)  | [linkedgeodata.org](http://linkedgeodata.org/)   |  [OpenStreetMap Contributers](http://openstreetmap.org/) | 
| bahnhoefe_rni.nt  | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) OR [ODbL](https://opendatacommons.org/licenses/odbl/index.html)  | [data.deutschebahn.com](https://data.deutschebahn.com/)   |  [Deutsche Bahn](https://www.deutschebahn.com/) | 
| betriebsstelle.nt  | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) OR [ODbL](https://opendatacommons.org/licenses/odbl/index.html)  | [data.deutschebahn.com](https://data.deutschebahn.com/)   |  [Deutsche Bahn](https://www.deutschebahn.com/) | 
| betriebsstellen_geocoordinates.nt  | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) OR [ODbL](https://opendatacommons.org/licenses/odbl/index.html)  |  [data.deutschebahn.com](https://data.deutschebahn.com/)   |  [Deutsche Bahn](https://www.deutschebahn.com/) | 
| elektrotankstelle.nt | (asap) To Be Determined  | ?   |  ? | 
| graph_bahnsteige.nt  | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) OR [ODbL](https://opendatacommons.org/licenses/odbl/index.html)  |  [data.deutschebahn.com](https://data.deutschebahn.com/)   |  [Deutsche Bahn](https://www.deutschebahn.com/) | 
| graph_rni_bahnsteig.nt  | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) OR [ODbL](https://opendatacommons.org/licenses/odbl/index.html)   |  [data.deutschebahn.com](https://data.deutschebahn.com/)   |  [Deutsche Bahn](https://www.deutschebahn.com/) | 
| haltestellen.nt  |  [ODbL](https://opendatacommons.org/licenses/odbl/index.html)  |  [data.deutschebahn.com](https://data.deutschebahn.com/)   |  [Deutsche Bahn](https://www.deutschebahn.com/) | 
| highway_roadconstruction_bremen.nt  | [dl-de/by-2-0](https://www.govdata.de/dl-de/by-2-0)  | [Mobilit Data Market Place](https://service.mdm-portal.de/mdm-portal-application/)   |  City of Bremen | 
| tankstellen.nt   | (asap) To Be Determined  | ?   |  ? | 
| weather_prediction_poi.nt   | GeoNutzV [de](http://www.geodatenzentrum.de/docpdf/geonutzv.pdf) / [en](http://www.geodatenzentrum.de/docpdf/geonutzv_eng.pdf)   |  [opendata.dwd.de](https://opendata.dwd.de/)   |   [German Meteorological Office (de: Deutscher Wetter Dienst, DWD)](https://www.dwd.de/EN/Home/home_node.html) | 
| weather_station.nt   |  GeoNutzV [de](http://www.geodatenzentrum.de/docpdf/geonutzv.pdf) / [en](http://www.geodatenzentrum.de/docpdf/geonutzv_eng.pdf) |  [opendata.dwd.de](https://opendata.dwd.de/)   |   [German Meteorological Office (de: Deutscher Wetter Dienst, DWD)](https://www.dwd.de/EN/Home/home_node.html) | 
| wetterbericht_poi.nt   | GeoNutzV [de](http://www.geodatenzentrum.de/docpdf/geonutzv.pdf) / [en](http://www.geodatenzentrum.de/docpdf/geonutzv_eng.pdf)  |  [opendata.dwd.de](https://opendata.dwd.de/)   |  [German Meteorological Office (de: Deutscher Wetter Dienst, DWD)](https://www.dwd.de/EN/Home/home_node.html) | 

### Sample Query - Road construction sites

```sparql
PREFIX alertc: <https://portal.limbo-project.org/dataset/alertCLocation/>
PREFIX rc: <https://portal.limbo-project.org/dataset/roadconstruction/>
PREFIX mv: <http://schema.mobivoc.org/>
PREFIX wgs: <http://www.w3.org/2003/01/geo/wgs84_pos#> 

SELECT (SAMPLE(?publicComment) as ?comment)
                        ?roadConstruction
                        ?startTime
                        ?endTime
                        ?speedLimit
                        ?fromLat
                        ?fromLon
                        ?fromName
                        ?toLat
                        ?toLon
                        ?toName
WHERE 
{ 
  ?roadConstruction a mv:SituationRecord .
  OPTIONAL {?roadConstruction mv:validity ?validity . } 
  OPTIONAL { ?roadConstruction mv:generalPublicComment ?publicComment .}
  OPTIONAL { ?validity mv:startTimeOverall ?startTime . }
  OPTIONAL { ?validity mv:endTimeOverall ?endTime . }
  OPTIONAL { ?roadConstruction mv:situationSpeedLimit ?speedLimit . }
  ?roadConstruction mv:primaryLocation ?primaryLocation .
  OPTIONAL { ?primaryLocation mv:locationName ?toName . }
  OPTIONAL { ?primaryLocation wgs:lat ?toLat . }
  OPTIONAL { ?primaryLocation wgs:long ?toLon . }
  ?roadConstruction mv:secondaryLocation ?secondaryLocation .
  OPTIONAL { ?secondaryLocation mv:locationName ?fromName . }
  OPTIONAL { ?secondaryLocation wgs:lat ?fromLat . }
  OPTIONAL { ?secondaryLocation wgs:long ?fromLon . }
} GROUP BY ?roadConstruction  ?startTime ?endTime ?speedLimit ?fromLat ?fromLon ?fromName ?toLat ?toLon ?toName
```


Provided by: [LIMBO-Projekt](https://www.limbo-project.org/)
Created by: [Niklas Petersen](http://np00.github.io/)
