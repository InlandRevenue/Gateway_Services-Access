![IRD logo](../Images/IRlogo.gif)
![Software Dev](../Images/SoftwareDev.png)

# Software Intermediation Service

## About the service

The Software Intermediation service provides the ability for software providers to link to their Tax Agency clients 
or directly to their Customers in order to be provided an initial full data load and daily bulk file updates of their transaction data. 

The Software Intermediation service allows these links to be established, queried, or removed. 

There is a separate Intermediation service that addresses the links between business intermediaries like tax agents and their client lists and their customer accounts. 
The actual dataset resulting in bulk files from a software intermediation link will be impacted by those intermediation links but the links themselves are maintained separately. 

[View the TDS Overview](https://github.com/InlandRevenue/Gateway_Services-Transaction-data-services) to find out more details. 

--------------------
## Key documentation

* Schemas and WSDLs
	* View and download the [Common v1 xsd](../../Common%20XSD/Common.v1.xsd)
	* View and download the [Software Intermediation v1 xsd](SoftwareIntermediation.v1.xsd)
	* View and download the [Software Intermediation v1 developer wsdl](SoftwareIntermediationDevWSDL.v1.wsdl)
	
* View and download [Build Pack](Gateway%20Services%20Build%20Pack%20-%20Software%20Intermediation%20Service.pdf)	
* [Message Samples](./Sample%20Messages/)	
	
Products using this service:
-------------
* [Transaction Data Services](https://github.com/InlandRevenue/Gateway_Services-Transaction-data-services)

Supporting services
-------------
* [Identity and Access](../Identity%20and%20Access/)
* [Service - Intermediation](../Service%20-%20Intermediation)

-----------------
## Test environment information:

* Test scenarios
	- [Download test scenarios report template](Software%20Intermediation%20Service%20-%20Test%20Scenarios%20Report%20Template.docx)

* Test environment URL endpoints

	* Gateway service: https://test5.services.ird.govt.nz:4046/Gateway/GWS/SoftwareIntermediation/
	* SOAP WSDL: https://test5.services.ird.govt.nz:4046/Gateway/GWS/SoftwareIntermediation/?wsdl
	
	-----------------
## Production environment information:

* Production URL endpoints

	- Gteway service: https://services.ird.govt.nz:4046/Gateway/GWS/SoftwareIntermediation/
	- Cloud SOAP WSDL: https://services.ird.govt.nz:4046/Gateway/GWS/SoftwareIntermediation/?wsdl