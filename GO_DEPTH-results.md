# GO-PEG Use case results for GO-DEPTH

## 1. Use case description
The subsurface is considered the new frontier of our continent: it holds natural resources and storage capacity (so-called geo-potentials - e.g., geothermal heat, raw materials, groundwater) to be managed carefully in order to preserve a natural and safe environment for European citizens. 
To date, each country handles subsurface data following its own models, often based on specific software solutions, and this makes it very difficult to create cross-border / pan-European data. 

The overall goal of this use case is to provide both a methodology and a common data model to conceptualize, organize and deliver easy-to-use, high-quality, interoperable subsurface information for sustainable planning and use of natural resources. 

### 1.1 Objectives and stakeholders
The use case elaborates on various outcomes and lessons learnt from  GeoMol and HotLime projects, relying on expertise and thematic domain knowledge of the Italian Institute for Environmental Protection and Research (ISPRA), at the same time a stakeholder of this use case and a partner in the GeoMol and HotLime projects.

The use case aimed to develop an efficient approach to manage and deliver interoperable subsurface geological data. To achieve this goal an INSPIRE-extended data model and GeoPackage INSPIRE alternative encoding were used.
The developed approach (and related models) fulfills the institutional mandates of the Geological Survey of Italy and underlays the ongoing design and implementation of the “Geological 3D subsurface models database” related to the National Geological Mapping Programme.

The achieved results so enthused the stakeholder, especially pertaining to the GeoPackage encoding of INSPIRE data, that, in consultation with the technical partner, it was decided to make a further effort to ensure that the obtained results would also be of maximum use for the INSPIRE community and the Geological Survey of Italy.

It was therefore decided to extend the original scope of the use case, which focused on subsurface INSPIRE-extended concepts, - i.e., geologic unit boundaries and faults, to include:
 *	comprehensive modelling of surface geology data (core INSPIRE Geology data model)
 *	contribution to [INSPIRE Good Practice](https://inspire.ec.europa.eu/portfolio/good-practice-library) on [GeoPackage encoding of INSPIRE datasets](https://github.com/INSPIRE-MIF/gp-geopackage-encodings/blob/main/spec/GeoPackage_Good_Practice_initiation_fiche.md).

The work done is a reference implementation of the INSPIRE Good Practice on GeoPackage encoding and was illustrated during the INSPIRE Good Practice – GeoPackage and implementation practice outreach webinar. 


### 1.2 Spatial Coverage
The approach has been successfully applied and different input datasets were successfully harmonised and integrated in the target data model for Italy and Austria. 
Because each country handles subsurface data following its own model, often based on specific software solutions, intensive contributions of local experts is needed to correctly map these local data models to the harmonised target model. This was  feasible only for Italy and Austria within the timespan of the project.

## 2. Delivery Data Model
In the implementation of this use case, the full harmonization of 3D geological information was prioritazed.
In agreement with the stakeholder, the development of the target data model for energy resources layers was postponed (aware of the risk of not developing it at all, as in fact happened) to the completion of the harmonisation activities for geological data. This was agreed in view of fostering the development of methodologies and procedures for 3D data and acquiring knowledge of tools that can be reused in other contexts. 

### 2.1 Selection and Design
Data model design activities were carried out in close collaboration with ISPRA stakeholder (as domain expert) and through several iterations.
Analysing the use case requirements, it was decided that geological information would have been modelled extending the INSPIRE GE data specifications, since these already provide a common model for most of the concepts and data objects needed by the GO-DEPTH use case.
Geologic Units and Faults are the addressed INSPIRE GE spatial objects. 

### 2.2 Conceptual Mapping
It was decided that the GO-DEPTH data model would have extended the INSPIRE Geology core application schema:  
1. adding:
   * the “Boundary” and the “Isoline” spatial objects 
   * the “BoundaryInfo” data type, a complex data type providing the geometry of the points belonging to a boundary surface. In the sake of the ease of use and interoperability, it was decided to operate a simplification for the geometry representation of the Geologic Units (in 3D model described by volumes), i.e., not directly deal with ‘real’ volumes but provide subsurface geometry information of the Geologic Units through related “full” surfaces of Geologic Unit Boundaries.
This means that a discretization is operated of the Geologic Unit Boundary surfaces so that they are collections of points (i.e., they are “full” surfaces). Each point of these surfaces is a spatial object characterized by x, y, z values plus a thickness (t) value.
    * the “3D_Fault” feature type 

2.	extending: 
    * the GeologicUnit spatial object by the “stratigraphicBoundary” association 
    * the ShearDisplacementStructure spatial object adding more attributes.

A UML model was produced and both XSD (XML Schema Definition) and GeoPackage template physical schemas were derived.

### 2.3 Data transformation
Pre-processing needed on source GeoMol and HotLime data (mostly to interconnect the different sources - via IDs - in view of data integration activities)
A hale studio project was created  to transform and integrate all input sources according to the target data model and in GeoPackage encoding format. 

### 2.4 Challenges

Major challenges faced are linked to the design of the target data models, and can be summarised as follows:
1. The geometry representation of the Geologic Unit represented the major challenge faced. The reason is that in 3D models a Geologic Unit should be described by a volume, and this is not adequately represented in the INSPIRE GE models. The INSPIRE models are more focused on 2D Geological Maps. Moreover, the variety of approaches and data structures used by the different countries, mostly connected to the specific software used, made it difficult to find a common model. 

To solve this issue, in GO-DEPTH it was decided to:
* develop the data model looking for a common starting point i.e., provide only basic information
* operate a simplification of volumes represented through a ‘full’ surface - i.e., a collection of points characterized by (x,y,z) triplets plus a thickness values.

2. huge file sizes of the output layers. 

To solve this issue it was decided to create output layers in GeoPackage format, because it is particularly suitable for data consumption in GIS environments and delivery of large datasets. Related work has been aligned and contributed to the creation of the INSPIRE Good Practice on GPKG encoding of INSPIRE datasets: https://github.com/INSPIRE-MIF/gp-geopackage-encodings/blob/main/spec/GeoPackage_Good_Practice_initiation_fiche.md

## 3. Tools used

### 3.1	Analysis
hale studio and QGIS.

### 3.2	Transformation
hale studio

### 3.3	Publication
The harmonised GeoPackage dataset was also published through GeoServer to assess whether it could be easily published and queried via APIs. The possibility of content negotiation - i.e., option to serve different representations of the resource to the same URI – as well as the possibility to serve data in different CRSs was tested as well.

### 3.4	Metadata

GeoNetwork

### 3.5	Issues with the tools and Feedback on tools

## References and Links
