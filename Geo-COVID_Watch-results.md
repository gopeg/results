# GO-PEG Use case results for Geo-COVID_Watch

## 1. Use case description
As the world started struggling with the COVID-19 pandemic, it became increasingly evident how dependent we are on reliable sources of data and how often the approach to data management is not fit for purpose. At the same time the lack of agreements on statistical metrics and data aggregation processes contribute to the current unclarity about available data.The geo-COVID Watch use case intends to contribute to a shared understanding of the COVID-19 pandemic by using mechanisms for direct access to measurement data developed in the environmental sector in recent years. 

### 1.1 Objectives and stakeholders
In cooperation with the 'DataCove' (Austrian IT company) stakeholder, the geo-COVID Watch Use Case aims to investigate to what extent the direct access mechanisms to measurement data successfully applied in the environmental field can be applied to enhance timely availability and interoperability of COVID-19 pandemic data. In particular, the use case investigates the suitability of using OGC standards (Features and SensorThings API) and related technologies for sharing and searching COVID-19 data on the web. 


### 1.2 Spatial Coverage
The approach has been successfully applied to sources with EU-wide scope.
For demo purposes, however, only Italian data are currently exposed.

## 2. Delivery Data Model
Initiative database (exposed via API Feature service) underlaying model
![image](https://user-images.githubusercontent.com/13329248/229091272-d6ba33c7-2962-47e2-98d3-97cb977a7d70.png)

Case and country measures data (exposed via STA (SensorThings API) service) follow OGC STA Model
![image](https://user-images.githubusercontent.com/13329248/229091389-60582422-d4d6-41c2-bedc-dcc12725466e.png)


### 2.3 Data transformation
Initiative data is inserted manually in the database. Likewise, codelist values in the registry are also updated manually. An importer (script) ingests case and country measures data into STA service. The data sources that have been mapped to target data models are as follows:
Cases:
* JRC: https://github.com/ec-jrc/COVID-19/blob/master/data-by-country/jrc-covid-19-countries-latest.csv  
* ECDC: https://www.ecdc.europa.eu/en/publications-data/data-daily-new-cases-covid-19-eueea-country


## 3. Tools used
### Data storage
PostGIS databases

### Publication
Initiative dataset was published through GeoServer OGC API Features.
Case and measures data was published via FROST STA
