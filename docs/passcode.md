# The Passcode API

This API has the following attributes:

| Attribute | Value                                     |
|-----------|-------------------------------------------|
| namespace | com.yahoo.ecosystem.mobile_payment.parsec |
| version   | 1                                         |


## Resources

### [MpNullResult](#MpNullResult)

#### POST /passcodes

The API give user setup 1st passcode


#### Request parameters:

| Name     | Type                      | Source | Options | Description             |
|----------|---------------------------|--------|---------|-------------------------|
| passcode | [MpPasscode](#mppasscode) | body   |         | user enter the passcode |


#### Responses:

Expected:

| Code           | Type |
|----------------|------|
| 204 No Content |      |


Exception:

| Code                      | Type                                        | Comment                                                                 |
|---------------------------|---------------------------------------------|-------------------------------------------------------------------------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) | The user given wrong format of passcode or passcode have already setup. |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) | The user not login.                                                     |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |                                                                         |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) | The system have error.                                                  |


#### PUT /passcodes

Reset passcode by given old passcode or authorized card number


#### Request parameters:

| Name      | Type                        | Source | Options | Description            |
|-----------|-----------------------------|--------|---------|------------------------|
| resetData | [MpResetData](#mpresetdata) | body   |         | Reset data user given. |


#### Responses:

Expected:

| Code           | Type |
|----------------|------|
| 204 No Content |      |


Exception:

| Code                      | Type                                        | Comment |
|---------------------------|---------------------------------------------|---------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) |         |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) |         |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |         |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) |         |


#### GET /passcodes

Check the user have set passcode or not.


#### Responses:

Expected:

| Code           | Type |
|----------------|------|
| 204 No Content |      |


Exception:

| Code                      | Type                                        | Comment |
|---------------------------|---------------------------------------------|---------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) |         |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) |         |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |         |
| 404 Not Found             | [ParsecResourceError](#parsecresourceerror) |         |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) |         |


#### DELETE /passcodes

Check the user and its passcode.


#### Responses:

Expected:

| Code           | Type |
|----------------|------|
| 204 No Content |      |


Exception:

| Code                      | Type                                        | Comment |
|---------------------------|---------------------------------------------|---------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) |         |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) |         |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |         |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) |         |


### [MpCheckResult](#MpCheckResult)

#### POST /passcodes/check

Given passcode to check match user's passcode or not


#### Request parameters:

| Name     | Type                      | Source | Options | Description             |
|----------|---------------------------|--------|---------|-------------------------|
| passcode | [MpPasscode](#mppasscode) | body   |         | The passcode user given |


#### Responses:

Expected:

| Code   | Type          |
|--------|---------------|
| 200 OK | MpCheckResult |


Exception:

| Code                      | Type                                        | Comment |
|---------------------------|---------------------------------------------|---------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) |         |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) |         |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |         |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) |         |


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

### <a name="MpResetType"></a> MpResetType

Support reset by old passcode or card number.

`MpResetType` is an `Enum` of the following values:

| Value          | Description                                                |
|----------------|------------------------------------------------------------|
| BY_PASSCODE    | indicate reset by passcode. indicate reset by card number. |
| BY_CARD_NUMBER |                                                            |


### <a name="MpResetData"></a> MpResetData

The reset data for passcode.

`MpResetData` is a `Struct` type with the following fields:

| Name        | Type                        | Options | Description                                        | Notes |
|-------------|-----------------------------|---------|----------------------------------------------------|-------|
| resetType   | [MpResetType](#mpresettype) |         | indicate reset by "old passcode" or "card number". |       |
| cardNumber  | String                      |         | required if ResetType is BY_CARD_NUMBER.           |       |
| oldPasscode | String                      |         | required if ResetType is BY_PASSCODE.              |       |
| newPasscode | String                      |         | The new passcode for reset.                        |       |


### <a name="MpPasscode"></a> MpPasscode

passcode

`MpPasscode` is a `Struct` type with the following fields:

| Name     | Type   | Options | Description      | Notes |
|----------|--------|---------|------------------|-------|
| passcode | String |         | passcode string. |       |


[Swagger URL](https://git.corp.yahoo.com/pages/ApexTest/Swagger-UI/parsec/swagger-ui/?url=https://git.corp.yahoo.com/pages/ApexTest/project_1503989415696/swagger-json/passcode_swagger.json)
