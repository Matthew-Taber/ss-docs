[title]: # (Automatic Secret Export)
[tags]: # (Export secret, migration,rest api, secret server cloud)
[priority]: # (1000)

# Automatic Secret Export REST API

## Overview

If you use Secret Server Cloud, you can use a REST API to download exports and view your export storage list.

The automatic export feature has the following endpoints available for cloud customers only. API usage is fully audited.

A typical use of these API endpoints is to automate downloading exports to your backup solution outside of Secret Server (for redundancy). 

> **Note:** Any permission errors when using the API will return a 403 forbidden status code and an API_AccessDenied error message.

## Viewing the Storage List

Get a list of the exports currently in storage. Your session must be authenticated, and the authenticated user must have Automatic Export view permissions.

### Sample Request

```` json
GET: http://sample.secretservercloud.com/api/v1/configuration/a
````

### Sample Response

```` json
{
	"records": [
    	{
			"id": 123,
			"autoExportConfigurationId": 1, 
    		"storageDate": "2021-07-01T07:00:02.27",
			"filename": "secret-server-export-20210707070002",
    		"canDownload": true
    	},
    	...
     ],
     ...
}
````

The response is a JSON object with a records property whose value is the list of all the exports in storage. Each list entry has the following properties:

- **id:** The ID for this export in storage, which is used with the Download Export endpoint to download the export.

- **autoExportConﬁgurationId:** The ID for the automatic export conﬁguration this export belongs to. This may be useful in the future if we support multiple export conﬁgurations, but for now it is only used internally.
- **storageDate**: The date and time the export was stored.
- **ﬁlename:** The ﬁlename for the export archive and the export XML ﬁle inside it.
- **canDownload:** Whether the user can download this export archive.

##  Downloading Secret Exports

Download an export in storage by its ID. Your session must be authenticated and the authenticated user must have automatic export download permissions.

### Sample Request

````json
GET: http://sample.secretservercloud.com/api/v1/configuration/au
````

Where **{id}** is the ID of the export you want to download. This value is obtained from the **Storage List** endpoint.

### Sample Response

A stream of bytes representing the export archive.