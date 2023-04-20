# GO-PEG Online resources and assessments for POPImpact

## 1. Online Resource
### 1.1 Download Services
OGC API: http://csgs002.westeurope.cloudapp.azure.com/geoserver/ogc/features/?f=application%2Fjson

WFS  http://csgs002.westeurope.cloudapp.azure.com/geoserver/PopImpact/wms?service=WFS&request=GetCapabilities
 ### 1.2 View Services
 WMS: http://csgs002.westeurope.cloudapp.azure.com/geoserver/PopImpact/wms?service=WMS&request=GetCapabilities
 ### 1.3 Metadata
Spanish Data Portal:  https://www.idee.es/csw-inspire-idee/srv/api/records/ES.GOPEG.BU/formatters/xml
EDP:<https://data.europa.eu/api/hub/repo/datasets/es-gopeg-bu.rdf?useNormalizedId=true>
### 1.4 Portals
Spanish Data Portal: https://www.idee.es/csw-inspire-idee/srv/spa/catalog.search#/metadata/ES.GOPEG.BU
![image](https://user-images.githubusercontent.com/94920015/229062531-b6a59dff-48bb-4d69-9836-66369fb9c37a.png)

EDP: https://data.europa.eu/data/datasets/es-gopeg-bu?locale=es
![image](https://user-images.githubusercontent.com/94920015/229059519-c211b473-c54b-4919-8a2e-c56efa6b9e8c.png)
![image](https://user-images.githubusercontent.com/94920015/229059562-10847571-e93b-4884-ba8c-4376226c8e7d.png)
 
## 2. Assessment of resources
### 2.1 INSPIRE evaluation report
![image](https://user-images.githubusercontent.com/94920015/229059701-7d53e202-6b44-4571-acd8-8e3c95fa3a0d.png)

### 2.2 MQA evaluation report
https://www.itb.ec.europa.eu/shacl/dcat-ap/upload

Test April 2023: The metadata is DCAT-AP compliant.


### 2.3 FAIR evaluation report
URL: <https://fair-enough.semanticscience.org/evaluations/223c57f3cfb6e6116adc3e4696c1f596ac3319d7>

Result:10/16

![image](https://user-images.githubusercontent.com/94920015/229061199-1ca91137-f1ce-47d9-a481-a1b891284e1b.png)
 
### 2.4 Summary
A total of 6 out of 16 tests failed the evaluation, the related error messages were analysed and a brief explanation of the detected issues is provided in the table below.
 | FAIR     | Metrics tests                                    | Issues                                                                                                                          |
| -------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| Findable | F1_2M                                            | Resource identifier is persistent                                                                                               | Necessary to have persistent urls of the metadata (purl, doi, w3id, identifiers.org). |
| |A2 \_ 1M | Metadata is persistent                           |
| |F3_1M    | Metadata identifier explicitly in metadata       | Need for unique urls using GUID                                                                                                 |
|| F4_1M    | The resource is indexed in a searchable resource | It is necessary to index metadata in search engines: DuckDuckGo search engine, Google custom search API and Bing search engine. |
| Reusable | R1_1M                                            | Metadata includes a License                                                                                                     | This data is lost in the transformation between INSPIRE Metadata to Geo-DCAT. |
|| R1_2M    | Metadata includes a standard License             |
