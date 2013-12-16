TourConnect REST API
========================

This documentation provides basic instructions for a Contractor on how to programmatically access signed contracts on the TourConnect platform.  You will need a live TourConnect account and at least one signed test or live contract available for download.

Before accessing the API, you will need the following:

* **ContractorID** * - This is your Contractor name and it is displayed at the top left of your dashboard after login.

* **API Key** -  This is available within your TourConnect profile.  To locate this key, login to your account and then scroll down to the bottom of the 'Profile' page where you would see the value for your 'API Key'. You will use this key for all REST GET operations.

* **API Version Number** - we maintain multiple versions of the API in the event that our subscribers need additional time to make necessary changes to their integration to take advantage of newly released versions of our API.  The CURRENT VERSION = 2.  This documentation applies only to version 2.

## API Endpoint

Once you have your Key and Version number established, you will be able to determine your API Endpoint as follows:

```
https://contracting.tourconnect.com/contractors/[ContractorID]/key/[Your API Key]/version/[API Version Number]
```

Throughout the remainder of the document, we will reference the REST API URL: https://contracting.tourconnect.com/contractors/[ContractorID]/key/[YourAPIKey]/version/[APIVersionNumber] as __/TourConnectEndpoint__ .

A specific example of what an endpoint would look like with the ContractorID, API Key and Version filled using a test account using the following: 
* **API KEY** = "07823D39DCAE9F1B2765A229109C658E".
* **SUPPLIER ID** = "demo-tours".
* **API Version Number** = "2".

__your endpoint would look like:__
https://contracting.tourconnect.com/contractors/demo-ito/key/07823D39DCAE9F1B2765A229109C658E/version/2/get_contracts.xml


## Accessing Signed Contracts

TourConnect allows you to access signed contracts in a number of different ways using different function calls with different options.  You create API calls with a single:

* **FUNCTION NAME** - Based on this name, system determines what data should be provided to user.

and then using the following optional arguments to further refine the list of contracts that are retrieved from TourConnect:

*  ***SUPPLIER ID*** - A specific Supplier company name if you would like to retrieve contracts for a single, named Supplier.
*  ***START DATE & END DATE*** - Used to retrieve Contracts for a specified date range and regardless of whether the Contracts had been retrieved in prior API calls.




Note:
* User needs to pass arguments by appending them to URL as exlpained below:
  For a contractor, to get XML data of contracts **FUNCTION-NAME** is "get_contracts"
* First 3 parameters in URL (key, version & function name) are mandetory and they must be in the presribed sequence **same sequence** shown below.
* Tourconnect requires the following date encoding for all API calls: __yyyy-mm-dd__  .  Any call not formatted correctly will result in an error and no data being returned.






####Note On Dates
Tourconnect assumes the following date encoding for all API calls.  Any call not formatted correctly will result in an error and no data being returned:
__yyyy-mm-dd__



##Retrieving Contracts
There are various parameters that can be used to retrive your contract data.  You can download all contracts that have not yet been requested/transfered, you can request by date ranges, you can request by SupplierID and finally, by a combination of date range and SupplierID.

###Get All un-downloaded Contracts
This is the recommended method to accessing the contracts.  It will transmit all the contracts, for all the Suppliers that have not yet been requested by you.  

```
/TourConnectEndpoint/get_contracts.xml
```

###Get Contracts by Date
You can retrieve all contracts bound between one or two dates, either a start date only (assume today as end date) or a start date and an end date.  This will retrieve all contracts between those dates regardless of whether they have been marked as downloaded.

```
/TourConnectEndbpoint/get_contracts/start-date/<startdate>/end-date/<enddate>.xml
```
__or__
```
/TourConnectEndpoint/get_contracts/start-date/<startdate>.xml
```
the second call will assume todays date as the end date.

###Get Contracts by Supplier
You can retrieve all the contracts for a given supplier and for a given date range using the TourConnect API.  

```
/TourConnectEndpoint/supplier/<supplierID>.xml
```
where <supplierID> is the name of the Supplier for which you wish to retrieve contracts.  The suppler must be exact or an error is returned.

You can also retrieve contracts for a specified Supplier for specified date ranges.
```
/TourConnectEndpoint/supplier/<supplierID>/startdate/<startdate>.xml
```
__or__
```
/TourConnectEndpoint/get_contracts/supplier/<supplierID>/start-date/<startdate>/end-date/<enddate>.xml
```


##Return Codes
There are several general status or return codes that come back after an API call.  Please refer to the following table for the list of those codes and their associated reason.

| Code        | Reason |
| ------------- | :------------- |
| 202 | OK
| 203 | Invalid Contractor ID
| 204 | Invalid SupplierID
| 205 | Invalid Date format. Please specify date as yyyy-mm-dd
| 206 | Invalid Date Range
| 207 | Invalid API Key
| 208 | Invalid function
| 209 | Invalid API Version
| 210 | Invalid arguments: <list of invalid arguments> 


If you have questions, suggestions or any issues, please feel free to send us a note on:
http://helpdesk.tourconnect.com
We will get back to you as soon as possible!
