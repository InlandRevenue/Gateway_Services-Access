![IRD logo](../Images/IRlogo.gif)
![Software Dev](../Images/SoftwareDev.png)

# Identity and access services

We provide 3 authentication options to access our with gateway services and secure file transfer services.

#### OAuth2 authentication
This authentication option is a authorisation token implementation using OAuth 2.0. Both cloud or native (desktop) application options 
are enforced for client applications and authenticate end users using their myIR user ID and password to grant consent to the application 
access to their Inland Revenue information.

#### Machine-to-Machine (M2M) authentication / Self-Signed JWT
This authentication option uses a client signed JSON Web Token (JWT) to sign messages, which lets us identify the service provider 
or a customer of a service provider. 

> M2M authentication is only available for service providers integrating through cloud services.

#### SSH authentication / PGP Key
This authentication option requires a service provider to supply their public PGP key for file encryption. We supply our public SSH key in order to gain access to the service provider FTP server.

> SSH authentication is only available for service providers integrating through a secure file transfer (SFTP) service.

---------------
## Key documentation 

- Build pack 
	- [Download the Identity and Access  build pack](Build%20pack%20-%20Identity%20and%20Access%20Services.pdf) to view authorisation and authentication details for the OAuth, M2M/JWT and SSH/PGP authorisation types
	
#### OAuth2 authentication
* [How to Integrate - OAuth2](./OAuth%20Authentication%20-%20How%20to%20Integrate.md)
* [How to Integrate - M2M JWT](./M2M%20JWT%20Authentication%20-%20How%20to%20Integrate.md)
* [Samples messages](./Message%20Samples.md) - requests and responses
* [Managing myIR logons for gateway services](https://www.ird.govt.nz/digital-service-providers/guides-and-docs/managing-myir-logons-for-gateway-services)

#### OAuth2 and M2M authentication	
* [Manage access tokens for gateway services](https://www.ird.govt.nz/digital-service-providers/guides-and-docs/manage-access-tokens-for-gateway-services)

----------------------------	
## Available authentication options for gateway services and file transfer services

> M2M/JWT authentication is only available for Digital Service Providers (DSP) integrating through cloud services **and for some services as listed below**.

<table>
	<thead>
		<th>Service</th>
		<th>OAuth2</th>
		<th>M2M/JWT</th>
		<th>SSH/PGP</th>
	</thead>
	<tbody>
		<tr>
			<td  style="background-color:lightgrey" colspan=4> <strong>Returns and Information</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Returns-and-Information" target="_blank">view services in this repository</a></td>	
		</tr>
		<tr>
			<td>Accounting Income Method (AIM)</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
		<tr>
			<td>Goods and Services Tax (GST)</td><td>Yes</td><td>No</td><td>No</td>
		</tr>	
		<tr>
			<td>Donation Tax Credits (REB)</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
		<tr>
			<td>Income Tax (INC)</td><td>Yes</td><td>No</td><td>No</td>
		</tr>	
		<tr>
			<td>Investment Income Reporting (AIL, DWT, IPS, NRT, PIE and RWT)</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
		<tr>
			<td>Payday Filing Return Service (EI)</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
		<tr>
			<td>Payday Filing Employment Service (ED/ES) </td><td>Yes</td><td>No</td><td>No</td>
		</tr>
		<tr>
			<td>Return Status Push Notifications (Secure FTP)</td><td>No</td><td>No</td><td>Yes</td>
		</tr>	
		<tr>
			<td  style="background-color:lightgrey" colspan=4> <strong>Customer and Account</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Customer-and-Account" target="_blank">view services in this repository</a></td>	
		</tr>	
        <tr>
		    <td>Customer Service Suite:
			   <ul>
			   <li>Account API</li>
			   <li>Address API</li>
			   <li>Bank API</li>
			   <li>Contact API</li>
			   <li>Customer API</li>
			   <li>Name API</li>
			   <li>Period API</li>
			   </ul>
			</td>
			<td>Yes</td>
			<td>Yes</td>
			<td>No</td>
        </tr>
		<tr>
			<td>Bill API</td><td>Yes</td><td>No</td><td>No</td>
		</tr>	
		<tr>
			<td>Income API</td><td>Yes</td><td>Yes</td><td>No</td>
		</tr>	
		<tr>
			<td>IRD Number Validation API</td><td colspan=3>Only requires Mutual TLS</td>
		</tr>
		<tr>
			<td  style="background-color:lightgrey" colspan=4> <strong>Communication</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Communication" target="_blank">view services in this repository</a></td>	
		</tr>
		<tr>
			<td>Document API</td><td>Yes</td><td>Yes</td><td>No</td>
		</tr>	
				<tr>
			<td>Notifications API</td><td>Yes</td><td>Yes</td><td>No</td>
		</tr>	
		<tr>
			<td style="background-color:lightgrey" colspan=4> <strong>Calculators</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Calculators" target="_blank">view services in this repository</a></td>	
		</tr>	
		<tr>
			<td>Prescribed Investor Rate (PIR) calculator</td><td>No</td><td>Yes</td><td>No</td>
		</tr>
				<tr>
			<td  style="background-color:lightgrey" colspan=4> <strong>Access</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Access" target="_blank">view services in this repository</a></td>	
		</tr>	
				<tr>
			<td>Intermediation Service</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
				<tr>
			<td>Software Intermediation Service</td><td>Yes</td><td>No</td><td>No</td>
		</tr>	
				<tr>
			<td  style="background-color:lightgrey" colspan=4> <strong>Transaction data services</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Transaction-data-services" target="_blank">view services in this repository</a></td>	
		</tr>
				<tr>
			<td>Transaction Data Services (Account & Transactions SOAP Service)</td><td>Yes</td><td>No</td><td>No</td>
		</tr>		
						<tr>
			<td>Transaction Data Services (Secure FTP)</td><td>No</td><td>No</td><td>Yes</td>
		</tr>
	</tbody>
</table>

## URL endpoints for SOAP services 

### Cloud

| Gateway Service | Environment | URL Endpoint |
| --- | --- | --- | 
| <ul><li> AIM</li><li>GST</li><li>Income Tax/Donation Tax Credits</li><li>Employment Information</li><li>Investment Income Reporting</li></ul> | Production |```http://services.ird.govt.nz:4046/gateway/gws/returns/```|
| <ul><li> AIM</li><li>GST</li><li>Income Tax/Donation Tax Credits</li><li>Employment Information</li><li>Investment Income Reporting</li></ul> | Testing |```http://test5.services.ird.govt.nz:4046/gateway/gws/returns/```|
| Employment Service | Production| ```http://services.ird.govt.nz:4046/gateway/gws/employemnt/```|  
| Employment Service | Test | ```http://test5.services.ird.govt.nz:4046/gateway/gws/employemnt/```| 
| Employment Service V2 |Production | ```http://services.ird.govt.nz:4046/gateway/gws/employemnt/v2/``` | 
| Employment Service V2| Test| ```http://test5.services.ird.govt.nz:4046/gateway/gws/employemnt/v2/```| 
| Intermediation | Test |```https://test5.services.ird.govt.nz:4046/secure/gateway/GWS/Intermediation/```|
| Intermediation | Production | ```https://services.ird.govt.nz:4046/secure/gateway/GWS/Intermediation/```|
| Software Intermediation | Test | ```https://test5.services.ird.govt.nz:4046/Gateway/GWS/SoftwareIntermediation/``` |
| Software Intermediation | Production | ```https://services.ird.govt.nz:4046/Gateway/GWS/SoftwareIntermediation/``` |
| Account | Test | ```https://test5.services.ird.govt.nz:4046/Gateway/GWS/Account/``` |
| Account | Production | ```https://services.ird.govt.nz:4046/Gateway/GWS/Account/``` |
| Transactions | Test | ```https://test5.services.ird.govt.nz:4046/Gateway/GWS/Transactions/```|
| Transactions | Production | ```https://services.ird.govt.nz:4046/Gateway/GWS/Transactions/```|


	
	
### Native Desktop	
| Gateway Service | Environment | URL Endpoint | 
| --- | --- | --- | 
| <ul><li> AIM</li><li>GST</li><li>Income Tax</li><li>Employment Information</li><li>Investment Income Reporting</li></ul> | Production | ```http://services.ird.govt.nz/gateway2/gws/returns/``` |
| <ul><li> AIM</li><li>GST</li><li>Income Tax</li><li>Employment Information</li><li>Investment Income Reporting</li></ul> | Testing | ```http://test5.services.ird.govt.nz/gateway2/gws/returns/``` |
| Employment Service | Production|  ```http://services.ird.govt.nz/gateway2/gws/employemnt/```| 
| Employment Service | Test |  ```http://test5.services.ird.govt.nz/gateway2/gws/employemnt/```| 
| Employment Service V2 |Production |  ```http://services.ird.govt.nz/gateway2/gws/employemnt/v2/```| 
| Employment Service V2| Test|  ```http://test5.services.ird.govt.nz/gateway2/gws/employemnt/v2/```| 	
	