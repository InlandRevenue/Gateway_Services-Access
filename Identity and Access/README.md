![IRD logo](../Images/IRlogo.gif)
![Software Dev](../Images/SoftwareDev.png)

# Identity and Access Services

We provide 3 authentication options to access our with gateway services

#### OAuth2 Authentication
This authentication option is a authorisation token implementation using OAuth 2.0. Both cloud or native (desktop) application options 
are enforced for client applications and authenticate end users using their myIR user ID and password to grant consent to the application 
access to their Inland Revenue information.

#### Machine-to-Machine (M2M) authentication / Self-Signed JWT
This authentication option uses a client signed JSON Web Token (JWT) to sign messages, which lets us identify the service provider 
or a customer of a service provider. 

> M2M authentication is only available for service providers integrating through cloud services.

#### SSH authentication / PGP Key
This authentication option requires a service provider to supply their public PGP key for file encryption. We supply our public SSH key in order to gain access to the service provider FTP server.

SSH authentication is only available for service providers integrating through Secure File Transfer Service SFTP.

## Key Documentation 


* [How to Integrate](./OAuth%20Authentication%20-%20How%20to%20Integrate.md)
* [Samples messages](./Message%20Samples.md) - requests and responses
* [Managing myIR logons for gateway services](https://www.ird.govt.nz/digital-service-providers/guides-and-docs/managing-myir-logons-for-gateway-services)
* [Manage access tokens for gateway services](https://www.ird.govt.nz/digital-service-providers/guides-and-docs/manage-access-tokens-for-gateway-services)
	
## Available authentication options for gateway services

M2M/JWT authentication is only available for service providers integrating through cloud services **and for some selected services as described in the table below**.

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
			<td>Accounting income method (AIM)</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
		<tr>
			<td>Goods and services tax (GST)</td><td>Yes</td><td>No</td><td>No</td>
		</tr>	
		<tr>
			<td>Donation tax credits</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
		<tr>
			<td>Income Tax</td><td>Yes</td><td>No</td><td>No</td>
		</tr>	
		<tr>
			<td>Investment income reporting</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
		<tr>
			<td>Payday filing (EI) - Return Service</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
		<tr>
			<td>Payday filing (ED) - Employment Service</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
		<tr>
			<td>Return Status push notifications </td><td>No</td><td>No</td><td>Yes</td>
		</tr>	
		<tr>
			<td  style="background-color:lightgrey" colspan=4> <strong>Customer and Account</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Customer-and-Account" target="_blank">view services in this repository</a></td>	
		</tr>	
		<tr>
			<td>Bill service</td><td>Yes</td><td>Yes</td><td>No</td>
		</tr>	
		<tr>
			<td>Income service</td><td>Yes</td><td>Yes</td><td>No</td>
		</tr>	
		<tr>
			<td  style="background-color:lightgrey" colspan=4> <strong>Communication</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Communication" target="_blank">view services in this repository</a></td>	
		</tr>
		<tr>
			<td>Document service</td><td>Yes</td><td>Yes</td><td>No</td>
		</tr>	
				<tr>
			<td>Notifications service</td><td>Yes</td><td>Yes</td><td>No</td>
		</tr>	
		<tr>
			<td style="background-color:lightgrey" colspan=4> <strong>Calculators</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Calculators" target="_blank">view services in this repository</a></td>	
		</tr>	
		<tr>
			<td>Prescribed investor rate (PIR) calculator</td><td>Yes</td><td>Yes</td><td>No</td>
		</tr>
				<tr>
			<td  style="background-color:lightgrey" colspan=4> <strong>Access</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Access" target="_blank">view services in this repository</a></td>	
		</tr>	
				<tr>
			<td>Intermediation Service</td><td>Yes</td><td>No</td><td>No</td>
		</tr>
				<tr>
			<td>Software intermediation</td><td>Yes</td><td>No</td><td>No</td>
		</tr>	
				<tr>
			<td  style="background-color:lightgrey" colspan=4> <strong>Transaction data services</strong> - <a href="https://github.com/InlandRevenue/Gateway_Services-Transaction-data-services" target="_blank">view services in this repository</a></td>	
		</tr>
				<tr>
			<td>Transaction Data Services (Account and Transactions)</td><td>Yes</td><td>No</td><td>No</td>
		</tr>		
						<tr>
			<td>Transaction data services (Secure FTP)</td><td>No</td><td>No</td><td>Yes</td>
		</tr>
	</tbody>
</table>



	