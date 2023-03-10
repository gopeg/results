# GO-PEG fair-port use case results

## 1. Use case description

### 1.1 Objectives and stakeholders
In the last 5 years, the German drone market has experienced an exponential growth. Currently there are around 455.000 drones in use, of which 19.000 are for commercial purposes. It is estimated that until 2023 the number of drones will further increase at an annual growth rate of 14% to approximately 850.000, cumulating in a drone market volume of €3 billion [[1]](#1).

With the usage of drones increasing, there is an urgent need for detailed air space and traffic planning based on highly precise and up-to-date geo spatial data to establish UAV geo zones. Such zones define flight corridors and flight restrictions. 

The main aim of the fAIRport use case is to provide a complete, high-quality geo-dataset of geo-zones as outlined in §21 of the German air space regulation for drones based on already harmonised spatial reference data. This reference data is enhanced with relevant geo-objects such as heliports and industrial plants, derived from aerial photos using artificial intelligence-based analysis algorithms. Consequently, the fAIRport use case will not only add value to the air space and traffic planning, but it will contribute to air space safety, too. 

While the majority of the base data will be provided by Deutsche Flugsicherung (DFS), further information on obstacles such as wind power plants, heliports, railway and road networks, industrial plants, will be automatically derived from very high resolution aerial photos based on artificial intelligence. In addition to this, the system will allow users such as public authorities, to add information on temporary no-fly zones such as marketplaces or fair grounds.

The central part of the fAIRport use case is the development of an open standard-based geo-data platform for public authorities that enables to automatically derive drone no-fly zones for Germany based on a variety of input datasets. The platform will allow users to visualize the data (2D and 3D-Visulization) as well as to add additional information to the dataset. 

The city of Langen (Germany) has agreed to participate in the use case as a stakeholder providing valuable input to develop the concept of the platform as well as to provide feedback to the platform requirements and functionality. 

### 1.2 Spatial Coverage

The fAIRport project itself is a project focused at the German airspace. Within the GO-PEG project, we expanded this focus to create cross-border datasets.

Within Germany, three pilot areas (AOIs) were identified based on the following criteria: 
-	Sufficient number of geoobjects with at least 100 objects for each object class and 
-	Small AOI as to reduce the amount of data

A total of three AOIs were chosen including (see Figure 1): 

1.	Greater Frankfurt metropolitan area 
2.	Border triangle of the Netherlands, Belgium and Germany 
3.	City area of the city of Langen 

![fAIRport areas of interest (AOI)](https://user-images.githubusercontent.com/54665693/224310202-09d91665-c85b-4d1e-ac2f-804e58d540d2.png)

_Figure 1: fAIRport areas of interest (AOI)_

While the focus of the use case is on no-fly zones in Germany, the potential of harmonising geo-data outside of the German territory should be evaluated. As such cross-border beyond visual line of sights (BVLOS) flights have been undertaken in the border triangle of the Netherlands, Belgium and Germany to simulate the harmonization of the drone no-fly zones across borders. In the GO-PEG context, we also created a cross-border dataset derived from INSPIRE protected sites data then encompasses five countries (DE, AT, NL, BE, parts of CZ). The reason for this was that we wanted to show the re-useability of INSPIRE data, but also because this data would be available to share as open data without any constraints. Unfortunately, for the full UTM data sets, public sharing as open data is not yet possible.

## 2. Delivery Data Model

### 2.1 Selection and Design
The data model developed in the project is to form the basis for the high-quality geodata set for UAV (“drones”) no-fly zones. The Fairport data model is based on the European ED-269 standard “Minimum Operational Performance Standard for UAS Geo-Fencing” (June 2020), which has been expanded to include components from the German DFS-GeoDM model. In addition, user requirements, which were determined in national stakeholder workshops, were integrated into the model.

### 2.2 Conceptual Mapping
The fAIRport conceptual model was designed as a UML class model. It consists of a total of seven classes (see Figure 2):

-	The central class is "UASRegulationZone", which summarizes the main properties (for example geometry, lower and upper limit, legal basis) of the no-fly zone.
-	The "ObjectDefinition" class contains the information on the geo-object on the basis of which the no-fly zone was established.
-	The time definition of the no-fly zone is regulated in the "TemporalDefinition" class.
-	The "Condition" class provides information about the respective type of drone (CE class, weight) to which the no-fly zone applies.
-	The "Authority" class summarizes the most important information about the authority that is responsible for the respective no-fly zone.
-	In the "Metadata" class, important information about the data set itself is also recorded so that changes can be traced.
-	The abstract UML class "UASZone (abstract)" specifies the code for the respective country and a unique identifier.

![Figure 2: Explanations to the fAIRport data model main types](https://user-images.githubusercontent.com/54665693/224311035-d828fd42-433a-4a30-b966-a186561a8076.png)

_Figure 2: Explanations to the fAIRport data model main types_

Semantic harmonisation is specifically complex for the codelists. Within the fairport model we handle with the following codelists. Final agreement upon codelist values is partly still ongoing within the process of iterative data harmonisation.

-	CodeAuthorityRole – Type of authorization role of the authority
-	CodeAuthorityHierarchy – regional level of the authority (nationwide, regional etc)-

-	CodeEquipment – code equipment the UAS can carry
-	CodeUsageCondition – possible usage conditions for the UAS
-	CodeSpeedClass – UAS speed classes
-	CodeWeightClass – UAS weight classes
-	CodeEmissionType – UAS emission types

-	CodeZoneReason – reasons for geofencing resp. UAS flight regulation
-	CodeZoneType – restriction zone type
- CodeRestriction – type of restriction condition

-	CodeWeekDayType 

__Encoding based operational/logical data model__

As the ED-269 standard requests GeoJSON as the file format for the output, the decision upon the encoding was easy. GeoJSON is an open format for geospatial data which represent entities based on the OGC Simple Feature Access specification.

A first version of the GeoJSON logical model has been modelled in JSON Schema language and hale»studio schema definition language.

### 2.3 Data transformation
During the project, multiple transformation workflows were implemented. All of these were implemented using hale studio (versions 4.1.0 and 5.0) and were run using the cloud transformation service hale cloud:

__INSPIRE Protected Sites to fAIRport and INSPIRE AreaManagement¬And-RestrictionZones__

This was the first pair of transformation projects we created in the scope of the project. The objective was to create a cross-border fAIRport UASZone dataset that would span at least 5 countries, and that would show the usefulness of accessible INSPIRE data in that context.

We thus integrated INSPIRE harmonised datasets on Protected Sites from Germany, the Czech Republic, Belgium, the Netherlands and from Austria and derived fAIRport data from these, as well as INSPIRE AM data. The details of each UASZone were derived from the type of protected site, using ancillary data on responsible authorities and the actual regulations in each country about operations of UAVs in these protected sites.

This transformation project could be implemented without changes to hale studio.

__GeoDM to fAIRport__

The DFS GeoDM dataset contains all information on UAS Zones and other data relevant for UAS Traffic Management for the whole of Germany. It is managed in a database and can be exported to various formats, such as GeoPackage. The schema itself is relatively flat, as it only consists of two simple relational tables.

As such, the mapping itself was also quite straightforward. The only aspect of the mapping that was complex was the creation of the ED-269 ID. Since only 5 characters in base64 were effectively available for the ID, a method needed to be developed that made sure that this limited number space is well used and that there are no collisions. Developing this method required several iterations with the full data sets.

In terms of conceptual mapping, there were no major mismatches since the target data model had been specifically designed to match the GeoDM model where it was important. As mentioned in the section before, this design process also included mapping code lists, where some matches are not equivalent, but most are OK and do not result in degraded data usefulness.

The specific challenge in this project was the size of the full data set, which was more than 7GB, delivered as a GeoPackage. The transformation project needed to be carefully optimised to run with less than 5GB of RAM (the current limit of the cloud transformation service for a single transformation process). Furthermore, we encountered an issue in the GeoJSON writer that made it hard to write very large GeoJSON files (in this case, 17GB to 20GB). In any case, GeoJSON files of such a size are hard to process with downstream software.

__fAIRport to ED-269__

The fAIRport model is closely aligned to ED-269, but includes more information, such as on the process of creating a UASZone, and is more structured than ED-269 to give more flexibility. However, due to the close alignment, creating a transformation project that goes from fAIRport to ED-269 has been relatively easy, and there are no real conceptual or structural mismatches that would degrade the usefulness of the ED-269 output.

This transformation project required some changes and bugfixes to hale studio, e.g. to the GeoJSON writer.

__fAIRport to INSPIRE AreaManagementAndRestrictionZones__

In addition to the direct mapping between INSPIRE PS and INSPIRE AM, we also created a transformation project that derives INSPIRE AM GML from data present in the fAIRport GeoJSON/GeoPackage.

Obviously, a lot of specific data such as the timetables gets lost in this case. However, the timetables are only important for a small subset of the UASZone objects, even though we expect them to become more important in the future. One option might be to look into an extension of the INSPIRE model in the future.

This transformation project could be implemented without changes to hale studio.

### 2.4 Challenges

#### Challenges on data model design
There are several existing data models (DFS GEODM, ED-269, ALKIS, etc) that had to be aligned and taken into account for the fAIRport data model. The data model needs to fulfil the requirements defined by the stakeholders and they must agree upon it. Thus, the fairport conceptual model has been designed & aligned to the existing models in more than 3 iterations within the conceptual phase. Each phase also included a review by the stakeholders. 

The decision on the encoding was easy as the standard ED-269 requires GeoJSON encoding.

But some use-case scenarios are underdefined because the related legal processes are not yet clear, even on national level. As a result, it is unclear whether parts of the data model are expressive enough. 

The agreement on the exact meaning of classes and codelists was challenging as two quite mature standards were involved that partly differ.

A general challenge is to decide when a conceptual model can be considered „good enough“ to be released and proceed with the implementation based on logical models. In our approach, we test conceptual models through their extension, i.e. through actually filling the model with data, and then using such data sets for the intended purposes. In this way, we usually get feedback that we can apply again at the conceptual level to derive an improved implementation model. Specific issues that we look for are mismatches, as well as over- and underspecifications. Such overspecifications can be identified e.g. by analysing which parts of a conceptual model are actually covered, and which parts have a high feature dependency, or large structural overhead.

#### Challenges on data transformation

We did several data transformation tests with national test data (e.g. GeoDM) as well as with cross-border data involving Germany, the Netherlands, Belgium, Luxembourg and Austria. For the model alignment and data mapping we use our open source ETL tool hale»studio.  A specific issue was the handling of IDs, because each of the standards that we had to align to has different requirements for persistent identifiers.

## 3. Online Resources
### 3.1 Download Services
### 3.2 View Services
### 3.3 Metadata
### 3.4 Portals

## 4. Assessment of resources
### 4.1 INSPIRE evaluation report
### 4.2 MQA evaluation report
### 4.3 FAIR evaluation report
### 4.4 Summary

## 5. Tools used
### 5.1 Data model design
For data model design hale studio 4.2 was used. The corresponding UML have been created with ARGO UML.

### 5.1	Analysis
For data analysis, [hale studio](https://wetransform.to/halestudio/) and [QGIS](https://www.qgis.org/) was used.

### 5.2	Transformation
For the transformation, [hale studio](https://wetransform.to/halestudio/) was used.

### 5.3	Publication
For the publication as network services, [hale connect](https://wetransform.to/haleconnect/) was used.

### 5.4	Metadata
For the creation and publication of metadata, [hale connect](https://wetransform.to/haleconnect/) was used.

### 5.5	Issues with the tools and Feedback on tools
Specific issues were documented in the [hale studio repository](https://github.com/halestudio/hale/issues).

## Links and References
<a id="1">[1]</a> 
Information is derived from BDL (2021) https://www.bdl.aero/de/
