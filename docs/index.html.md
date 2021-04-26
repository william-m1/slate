---
title: API Reference - MinusOneDB

includes:
  - errors

search: true
---

# Introduction

Welcome to minusone.

# Authentication

> To create the auth token:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/auth' \
--form 'username="yourUserName"' \
--form 'password="yourPassword"'
```


All the API calls to our services are authenticated with a token that is passed in the headers. The token can be generated using the `/auth` API as stated on the right.

The command on the right would generate an auth token and it will return a HTTP response `200` with a token content as below:<br>
`ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=`

> To send the auth token in all the other API calls

```shell
curl --location --request GET 'https://events-sage.minusonedb.com/health' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4='
```

This token can be used to pass in the headers for authorisation purposes of all the other APIs as shown on the right.

Please note that except `/auth` API, all the other APIs work with the auth token sent in the headers, failure to which a 401 HTTP status code will be returned.


# Access & User Management

## Authorisation

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/auth' \
--form 'username="yourUserName"' \
--form 'password="yourPassword"'
```

> The above command returns a generated token in plain text like this:

```shell
ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=
```

This endpoint generates a token and returns that for all your future purposes.

### HTTP Request

`POST 'https://events-sage.minusonedb.com/auth`

### Query Parameters

Parameter | Description
--------- | -----------
username | The username that has been created by you.
password | The password of the username.

<aside class="success">
A generated token that can be used in all the subsequent API calls.
</aside>

## Create a New User

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/user/add' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'username="NewUserName"' \
--form 'password="PasswordForTheNewUSer"' \
--form 'rights="schema"'
```

This endpoint creates a new user and returns a HTTP Code, `204` if the user was created successfully.

### HTTP Request

`POST 'https://events-sage.minusonedb.com/user/add`

### URL Parameters

Parameter | Description
--------- | -----------
username | The new username to be created
password | Password for the new user
rights | The rights assigned to the user. You can pass multiple rights with comma separated.<br>Please refer to Annexure A for the details on different types of rights.

## Change password of a user

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/user/password' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'username="OldUserName"' \
--form 'password="YourNewPassword"'
```

This endpoint creates a new user and returns a HTTP Code, `204` if the user's password was changed successfully.

### HTTP Request

`POST 'https://events-sage.minusonedb.com/user/password`

### URL Parameters

Parameter | Description
--------- | -----------
username | The new username to be created
password | Password for the new user

## Update rights of a user

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/user/update' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'username="m1william"' \
--form 'rights="admin"'
```

This endpoint creates a new user and returns a HTTP Code, `204` if the user's rights were updated.

### HTTP Request

`POST 'https://events-sage.minusonedb.com/user/update`

### URL Parameters

Parameter | Description
--------- | -----------
username | The new username to be created
rights | The rights assigned to the user. You can pass multiple rights with comma separated.<br>Please refer to Annexure A for the details on different types of rights.

## List all Users

```shell
curl --location --request GET 'https://events-sage.minusonedb.com/user/list' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4='
```

> The above command will return a HTTP code `200` with below contents:

```shell
[
    {
        "username": "chandra",
        "rights": [
            "admin",
            "schema",
            "get",
            "publish",
            "sessionUpdate",
            "sessionQuery"
        ]
    },
    {
        "username": "service_dev_smp_session",
        "rights": [
            "sessionUpdate"
        ]
    }
]
```

This endpoint creates a new user and returns a HTTP Code, `200` with all the users list in the JSON response will be returned as shown on the right.

### HTTP Request

`GET 'https://events-sage.minusonedb.com/user/list`

## Get details about a specific user

> To get details about a specific user:

```shell
curl --location --request GET 'https://events-sage.minusonedb.com/user/get' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'username="william"'
```

> Successful API call will return the response as below:

```shell
*.*
```

This endpoint can be used to retrieve details about a specific user.

### HTTP Request
`GET 'https://events-sage.minusonedb.com/user/get`

### URL Parameters

Parameter | Description
--------- | -----------
username | The username whose details are needed


### Rights Needed
`admin`

### API Response
A successful API Call will return a HTTP status code `200` with a JSON response as shown on the right.

## Remove a user

> To remove a user:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/user/remove' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'username="william"'
```

This endpoint can be used to delete a user and its rights from the system

### HTTP Request
`POST 'https://events-sage.minusonedb.com/user/remove`

### URL Parameters

Parameter | Description
--------- | -----------
username | The username whose details are needed


### Rights Needed
`admin`

### API Response
A successful API call will return a HTTP Status code `204`.

# Data Lake Methods

## Retrieve the current schema

> To retrieve the current scheam,

```shell
curl --location --request GET 'https://events-sage.minusonedb.com/schema' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4='
```


> The successful query will return the schema as below:

```shell
{
    "browser.screen.pixelDepth": {
        "large": false,
        "multivalued": false,
        "name": "browser.screen.pixelDepth",
        "type": "integer",
        "required": false
    },
    "_m1key": {
        "large": false,
        "multivalued": false,
        "name": "_m1key",
        "type": "integer",
        "required": true
    },
    "_m1rand": {
        "large": false,
        "multivalued": false,
        "name": "_m1rand",
        "type": "double",
        "required": true
    }
}
```

This endpoint will retrieve the currently loaded schema in your database. as shown on the right.
By default, the 2 columns, `_m1key` and `_m1rand` are always present in your database.<br><br>Any other columns added from the schema add endpoint will also appear in this list.

### HTTP Request

`GET 'https://events-sage.minusonedb.com/schema`

### Rights Needed
`schema, get, publish`

## Add a schema

> To add columns to the schema

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/schema/add' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'properties="[
  {
       \"name\": \"form.action\",
       \"type\": \"string\"
  }]"'
```


> A typical JSON passed in the parameter `properties`:

```json
[
  {
       "name": "form.action",
       "type": "string"
  },
  {
       "name": "form.method",
       "type": "string"
  }
]
```


This endpoint will add properties to the data lake. You can call this endpoint as many times to add any new properties of your desire to the data lake.

### HTTP Request

`POST 'https://events-sage.minusonedb.com/schema/add`

### URL Parameters

Parameter | Description
--------- | -----------
properties | A JSON string with structure mentioned on the right.

### Rights Needed
`schema`


## Wipe all schema

> To wipe and delete all the properties from the schema:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/schema/wipe' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4='
```

This endpoint can be used to wipe out and remove all the properties from the schema. Please note that the wipe fucntion will not remove the 2 default schema properties, `_m1key` and `_m1rand`.

### HTTP Request

`POST 'https://events-sage.minusonedb.com/schema/wipe`

### Rights Needed
`schema`

## Publish the data

> To publish data from S3 archive files:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/publish' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 's3file="s3://filePath"' \
--form 'format ="json"'
```

This endpoint can be used to publish all data from S3 into the data lake with optional transformation

### HTTP Request
`POST https://events-sage.minusonedb.com/schema/publish`

### URL Parameters

Parameter | Description
--------- | -----------
s3file | A fully qualified S3 file path
rules | Transformation rules, if any
format | Format of the file in S3, could be one of txt, csv, json, jsonl<br>If not present, file format would be used.
compression | could be one of gz, zip.<br>If not present, filename will be inspected.
encoding | Any java supported file encoding. Default is `utf-8`
delimiter | Delimiter used in the file<br>Tabs or Comma would be assumed for txt and csv files
headers | Specifies whether headers are present for delimited file formats. If not a TransformRuleSet will be required. Default true.
files | Used (only) to specify specific files to be extracted from zip archives.


### Rights Needed
`publish`

### API Response
A successful API call will return a HTTP code `204`.

## Retrieve a data

> To retrieve a specific data:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/get' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'ids="0"'
```

> A successful API response would be as below:

```shell
[
    {
        "_m1.ip": "1.1.1.1",
        "_m1key": 0,
        "event.element": "World",
        "_m1.receivedUTC": "2021-02-23T19:18:04.399Z",
        "_m1rand": 0.3628966850910368,
    }
]
```

This endpoint can be used to query the data from the Data Lake directly using the `_m1key`.

### HTTP Request
`POST 'https://events-sage.minusonedb.com/get`

### URL Parameters

Parameter | Description
--------- | -----------
ids | List of IDS to be retrieved.


### Rights Needed
`get`

### API Response
A successful API call will return a HTTP code `200` with a JSON body with contents as shown on the right.

# Archive Data Layer Methods

## Write Method

> To publish a data into the archive:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/write' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'publish="true"' \
--form 'items="[{\"seer_event\":\"click\"}]"'
```

This endpoint is used to persist any arbitrary data into the persistent archive layer.

### HTTP Request

`POST 'https://events-sage.minusonedb.com/write`

### URL Parameters

Parameter | Default | Description
--------- | ----- | -----------
items | None | A JSON string as an array items to be published.<br> A typical JSON array items is shown as an example on the right.
publish | false | Flag to tell if the data should be immediately published from the archieve layer to data store.
async | true | A flag to tell items should be published asynchronously.

### Rights Needed
`publish`

### API Response

If `async` is set as `false`, then a value is returned which denotes the `_m1key` for that record along with a HTTP status code `200`. In other cases, a HTTP status code `204` is returned.

# Data Store Methods

## Query from the database

> To query from the database:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/query' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'store="index"' \
--form 'q="time.utc.month:3"' \
--form 'rows="1"' \
--form 'fl="time.utc.month"' \
--form 'sort="_m1key asc"' \
--form 'json="{
  \"facet\": {
    \"eventsByUser\": {
      \"field\": \"seer_event\",
      \"type\": \"terms\",
      \"limit\": -1
    }
  }
}"'
```

> Successsful API Response

```shell
{
    "response": {
        "docs": [
            {
                "_m1key": 1680000,
                "time.utc.month": 3
            }
        ],
        "numFound": 735,
        "start": 0
    },
    "responseHeader": {
        "params": {
            "q": "time.utc.month:3",
            "fl": "time.utc.month,_m1key",
            "sort": "_m1key asc",
            "rows": "1"
        },
        "status": 0
    },
    "facets": {
        "count": 0
    }
}
```

The database supported SOLR query syntaxes. And hence you can refer to this [documentation](https://lucene.apache.org/solr/guide/8_0/searching.html#searching) for more details on running advanced queries.

### HTTP Request
`POST 'https://events-sage.minusonedb.com/query`

### URL Parameters

Parameter | Default | Description
--------- | ----- | -----------
store | None | Default store name where the query will run
q | None | SOLR syntax query
rows | 0 | Total number of row to be returned
fl | None | Properties projection list separated by comma
sort | None | Field and order in which the response has to be sorted
json | None | SOLR Facet JSON for advanced query


### Rights Needed
`get`

### API Response
The API response will be a HTTP status code `200` with the list of all the matching documents as per the query passed in the parameters.

## Store List

> To find the store list:

```shell
curl --location --request GET 'https://events-sage.minusonedb.com/store/list' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4='
```

> Successful API response:

```shell
[
    {
        "shards": 1,
        "autocommit": 2,
        "replicas": 1,
        "name": "index",
        "active": true,
        "type": "standard"
    }
]
```

This endpoint is used to get the list of all the stores avaialble.

### HTTP Request
`GET 'https://events-sage.minusonedb.com/store/list`

### Rights Needed
`get, admin`

### API Response
A successful command will return HTTP status code `200` with a JSON body with the list and details of the store list as shown on the right.

## Store Enable / Disable

> To disable / enable a store:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/store/enable' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'store="stash"' \
--form 'active="false"' \
```

This endpoint can be used to enable / disable a store.

### HTTP Request
`POST 'https://events-sage.minusonedb.com/store/enable`

### URL Parameters

Parameter | Description
--------- | -----------
store | A JSON string with structure mentioned on the right.
active | true / false - to enable / disable respectively


### Rights Needed
`admin`

### API Response
A successful API response would return HTTP code `204`.

## Store AutoCommit

> To enable / disable autocommit for a store:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/store/enable' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'store="stash"' \
--form 'on="false"' \
```

This endpoint can be used to enable / disable autocommit for the store.

### HTTP Request
`POST 'https://events-sage.minusonedb.com/store/autocommit`

### URL Parameters

Parameter | Description
--------- | -----------
store | A JSON string with structure mentioned on the right.
on | true / false - to enable / disable respectively

### Rights Needed
`admin`

### API Response
A successful API response would return HTTP code `204`.

# Session Store Methods

## Session Apply

> To insert / delete items from the session store:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/session/update' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'store="stash"' \
--form 'ops="[ { \"upsert\": [  {   \"a\" : 1,   \"session\": { \"id\": 2002  }  }  ]  } ]"'
```


> A detailed JSON for the parameter ops is as below:

```json
[ 
	{ 
		"upsert": [  
			{   "a" : 1,   "session": { "id": 2002  }  }  
		]  
	},
	{ 
    	"delete": [ 2001 ]
  	}
]
```

### HTTP Request
`POST 'https://events-sage.minusonedb.com/session/update`

### URL Parameters

Parameter | Description
--------- | -----------
store | A JSON string with structure mentioned on the right.
ops | A JSON array with 2 keys for insertion and deletion. One of them being mandatory.<br>Details are on the right.

<aside class="success">
	<ul><li>Please note that `upsert` in the parameter is used to insert an item in the session store.</li>
	<li>And `delete` in the parameter is used to delete the item from the session store.</li></ul>
</aside>


### Rights Needed
`sessionUpdate`

### API Response
A successful API response would return HTTP code `204`.

## Session Search

> To search from the session store:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/session/query' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'store="stash"' \
--form 'q="*:*"' \
--form 'sort="session.id asc"'
```


> A successful API response will contain matching results:

```json
{
    "count": 1,
    "items": [
        {
            "a": 1,
            "_m1": {
                "geo": {
                    "continent_name": "Asia",
                    "subdivision_2_name": "",
                    "registered_country_geoname_id": 1269750,
                    "latitude": 23.3426,
                    "continent_code": "AS",
                    "subdivision_1_iso_code": "JH",
                    "accuracy_radius": 200,
                    "time_zone": "Asia/Kolkata",
                    "network": "49.37.64.0/19",
                    "geoname_id": 1258526,
                    "is_anonymous_proxy": false,
                    "subdivision_2_iso_code": "",
                    "locale_code": "en",
                    "city_name": "Ranchi",
                    "country_iso_code": "IN",
                    "metro_code": "",
                    "country_name": "India",
                    "is_in_european_union": false,
                    "is_satellite_provider": false,
                    "position": "23.3426,85.3099",
                    "postal_code": "834001",
                    "subdivision_1_name": "Jharkhand",
                    "longitude": 85.3099
                },
                "receivedUTC": 1618474796186,
                "session": {
                    "lastUpdated": 1618474796495
                },
                "ip": "49.37.82.136"
            },
            "session": {
                "id": 2002
            }
        }
    ]
}
```

The database supported SOLR query syntaxes. And hence you can refer to this [documentation](https://lucene.apache.org/solr/guide/8_0/searching.html#searching) for more details on running advanced queries.

### HTTP Request
`POST 'https://events-sage.minusonedb.com/query`

### URL Parameters

Parameter | Default | Description
--------- | ----- | -----------
store | None | Default store name where the query will run
q | None | SOLR syntax query
rows | 0 | Total number of row to be returned
sort | None | Field and order in which the response has to be sorted

### Rights Needed
`sessionSearch `

### API Response
The API response will be a HTTP status code `200` with the list of all the matching documents as per the query passed in the parameters.

## Session List

> To list all the active sessions:

```shell
curl --location --request GET 'https://events-sage.minusonedb.com/session/list' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4='
```

> A successful API response would be:

```json
[
    {
        "shards": 1,
        "replicas": 1,
        "name": "stash",
        "key": "session.id"
    }
]
```

This endpoint can be used to list all the active sessions.

### HTTP Request
`GET 'https://events-sage.minusonedb.com/session/list`

### URL Parameters
`None`

### Rights Needed
`get, admin`

### API Response
A successful API call will return HTTP Status Code `200` with a JSON body as shown on the right.

# System Configurations

## Retrieve all system configurations

> To retrieve all the system properties:

```shell
curl --location --request GET 'https://events-sage.minusonedb.com/system' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4='
```

> A successful API response would be:

```json
{
    "bucket": "m1-11654edf3e264bd596f62ea916eea541",
    "geo": "true",
    "property-received": "_m1.receivedUTC",
    "init": "true",
    "cors": "abc.com,efg.com",
    "property-ip": "_m1.ip",
    "token-expire-ms": "720000000",
    "password-min-length": "8",
    "region": "us-east-1",
    "property-session-id": "session.id"
}
```

This endpoint can be used to retrieve all the currently configured system properties.

### HTTP Request
`GET 'https://events-sage.minusonedb.com/system`

### URL Parameters
`None`

### Rights Needed
`admin`

### API Response
A successful API call with a valid system property name could give the details of the system property details as shown on the right.

## Retrieve a specific system properties

> To retrieve a specific system property, you can pick the property name and run:

```shell
curl --location --request GET 'https://events-sage.minusonedb.com/system/cors' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4='
```

> A successful API response would be:

```shell
abc.com,efg.com
```

This endpoint can be used to retrieve a specific system property

### HTTP Request
`GET 'https://events-sage.minusonedb.com/system/<system_property_name>`

### URL Parameters
`None`

### Rights Needed
`admin`

### API Response
A successful API call with a valid system property name could give the details of the system property details as shown on the right.

## Set a System property

> To set a system property value:

```shell
curl --location --request POST 'https://events-sage.minusonedb.com/system/cors' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4=' \
--form 'value="seermedia.io,marconi.io"'
```

This endpoint can be used to set system properties.

### HTTP Request
`POST 'https://events-sage.minusonedb.com/system/<system_property_name>`

### URL Parameters

Parameter | Description
--------- | -----------
value | The value you want to set to the specific system property


### Rights Needed
`admin`

### API Response
A successful API response would return HTTP code `204`.

# Operations

## HealthChecks

> To check the healthcheck:

```shell
curl --location --request GET 'https://events-sage.minusonedb.com/health' \
--header 'm1-auth-token: ATaxKeeAnxPH3R8FX4xb/+/5WuHTYpZ1IbCMw4lNqE+vFNGIpW17s/Cw9fP63S2RWmdSVUifOnhPXKYjGeas5zc/2NKkRBEZky5fy1Uf5CE+bfFZfTHLzs8dRNvY/UvlQgMpoTTeIDZL/YQQ1RKSsofwdVjtarg1t2ixpes2ji4='
```

> A successful call will respond with:

```shell
{
    "geo": {
        "status": "PASSED",
        "message": "Data loaded."
    },
    "sessions": {
        "status": "PASSED",
        "message": "",
        "details": {
            "Node stash shard 0 replica 0": {
                "status": "PASSED",
                "message": "Status 200"
            }
        }
    },
    "system": {
        "status": "PASSED"
    },
    "stores": {
        "status": "PASSED",
        "message": "",
        "details": {
            "Node index shard 0 replica 0": {
                "status": "PASSED",
                "message": "Status 200"
            }
        }
    },
    "overall": {
        "status": "PASSED"
    },
    "id": {
        "status": "PASSED"
    },
    "lake": {
        "status": "PASSED"
    },
    "db": {
        "status": "PASSED"
    },
    "users": {
        "status": "PASSED"
    }
}
```

### HTTP Request
`GET 'https://events-sage.minusonedb.com/health`

### URL Parameters
None

### Rights Needed
`admin`

### API Response
The request will return a HTTP code `200` with details about all the system components and its related health details. A typical health check response is shown on the right.

# Annexures

## Annexure A - Rights to the Users

<aside class="notice">Below are the set of Rights that can be assigned to the users while thier accounts are being created.</aside>


Rights | Meaning
---------- | -------
admin | The user would be able to perform all the admin related operations
schema | The user would be able to perform all the schema alterations related operations
get | The user would only be able to fetch data from the database
publish | The user would be able to publish data to the database
sessionSearch | The user would be able to search from the live sessions store
sessionupdate | The user would be able to add / delete data from the live sessions store
