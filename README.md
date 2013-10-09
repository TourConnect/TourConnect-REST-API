# TourConnect REST API

TourConnect provides a REST API to retrieve signed contracts from the TourConnect servers.  This API is provided to registered users of TourConnect free of charge.  More information on TourConnect can be found at http://www.tourconnect.com.

## General

The primary endpoint for the TourConnect API is hosted at:

https://contracting.tourconnect.com

Before accessing the API, you will need the following:
1.  **ContractorID** -  This is the name of your account and is normally the name of your company.
2.  **Your API Key** -  This is available within your TourConnect profile.  To locate this key, login to your account and then scroll down to the bottom of the 'Profile' page where you would see the value for your 'API Key'. You will use this key for all REST GET operations.
3.  **API Version Number** - we maintain multiple versions of the API in the event that our subscribers need additional time to make necessary changes to their integration to take advantage of newly released versions of our API.  The CURRENT VERSION = 2

Once you have all of the above information, you can begin downloading XML versions of your contracts.  Using the above information, your API endpoint prefix:

```
https://contracting.tourconnect.com/contractors/[ContractorID]/key/[Your API Key]/version/[API Version Number]
```
__example:__
```
https://contracting.tourconnect.com/contractors/demo-ito/key/07823D39DCAE9F1B2765A229109C658E/version/2/get_contracts.xml
```

Moving forward, we will reference the url https://contracting.tourconnect.com/contractors/[ContractorID]/key/[YourAPIKey]/version/[APIVersionNumber] as __/TourConnectEndpoint__ .

####Note On Dates
Tourconnect assumes the following date encoding for all API calls.  Any call not formatted correctly will result in an error and no data being returned:
__yyyy-mm-dd__

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

If you have questions, suggestions or any issues, please feel free to send us a note on:
http://helpdesk.tourconnect.com
We will get back to you as soon as possible!
