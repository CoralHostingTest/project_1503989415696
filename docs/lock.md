# The Lock API

This API has the following attributes:

| Attribute | Value                                     |
|-----------|-------------------------------------------|
| namespace | com.yahoo.ecosystem.mobile_payment.parsec |
| version   | 1                                         |


## Resources

### [MpNullResult](#MpNullResult)

#### DELETE /locks

The API to delete all locks for qa testing


#### Request parameters:

| Name     | Type                              | Source          | Options | Description |
|----------|-----------------------------------|-----------------|---------|-------------|
| policy   | [MpLockPolicy](#mplockpolicy)     | query: policy   |         |             |
| duration | [MpLockDuration](#mplockduration) | query: duration |         |             |


#### Responses:

Expected:

| Code           | Type |
|----------------|------|
| 204 No Content |      |


Exception:

| Code                      | Type                                        | Comment                                 |
|---------------------------|---------------------------------------------|-----------------------------------------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) | The user given wrong format of lock.    |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) | The user not login.                     |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) | Invalid wssid or user not in whitelist. |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) | The system have error.                  |


## Types

### <a name="ParsecErrorDetail"></a> ParsecErrorDetail

DO NOT MODIFY This file is for who want to use ParsecResourceError as error
layout. But the structure here is only a reminder for user. It will not be
parsed by Parsec. Change this file will not affect the implementation of
ParsecResourceError. If you want to change the error layout of api end point,
you can customize your own error layout class.

`ParsecErrorDetail` is a `Struct` type with the following fields:

| Name         | Type   | Options | Description | Notes |
|--------------|--------|---------|-------------|-------|
| message      | String |         |             |       |
| invalidValue | String |         |             |       |


### <a name="ParsecErrorBody"></a> ParsecErrorBody

Parsec error response entity object

`ParsecErrorBody` is a `Struct` type with the following fields:

| Name    | Type                                                 | Options | Description   | Notes |
|---------|------------------------------------------------------|---------|---------------|-------|
| code    | Int32                                                |         | error code    |       |
| message | String                                               |         | error message |       |
| detail  | Array&lt;[ParsecErrorDetail](#parsecerrordetail)&gt; |         | error detail  |       |


### <a name="ParsecResourceError"></a> ParsecResourceError

This error model is designed for following EC REST API Convention (yo/ecrest)

`ParsecResourceError` is a `Struct` type with the following fields:

| Name  | Type                                | Options | Description  | Notes |
|-------|-------------------------------------|---------|--------------|-------|
| error | [ParsecErrorBody](#parsecerrorbody) |         | error object |       |


### <a name="MpNullResult"></a> MpNullResult

The object is just for no content

`MpNullResult` is a `Struct` with no specified fields


### <a name="MpCheckResult"></a> MpCheckResult

The object is for creditCardAuth & passCode check result

`MpCheckResult` is a `Struct` type with the following fields:

| Name    | Type | Options | Description                                                    | Notes |
|---------|------|---------|----------------------------------------------------------------|-------|
| isValid | Bool |         | True if credit card number or passcode is valid, false if not. |       |


### <a name="DateTime"></a> DateTime

ISO 8601 ref: http://tools.ietf.org/html/rfc3339#section-5.6
e.g.2013-03-06T11:00:00Z

`DateTime` is a `String` type.


### <a name="GUID"></a> GUID

Yahoo global uniq id

`GUID` is an alias of type `String`

### <a name="MpLockPolicy"></a> MpLockPolicy

lock policy

`MpLockPolicy` is an `Enum` of the following values:

| Value                | Description |
|----------------------|-------------|
| REQUEST_TOKEN        |             |
| RESET_BY_PASSCODE    |             |
| RESET_BY_CARD_NUMBER |             |
| VERIFY_CREDIT_CARD   |             |
| CHECK_PASSCODE       |             |


### <a name="MpLockDuration"></a> MpLockDuration

lock duration

`MpLockDuration` is an `Enum` of the following values:

| Value             | Description |
|-------------------|-------------|
| DURATION_10_MINS  |             |
| DURATION_1_HOURS  |             |
| DURATION_24_HOURS |             |


[Swagger URL](https://git.corp.yahoo.com/pages/ApexTest/Swagger-UI/parsec/swagger-ui/?url=https://git.corp.yahoo.com/pages/ApexTest/project_1503989415696/swagger-json/lock_swagger.json)
