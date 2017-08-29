# The CreditCardAuth API

This API has the following attributes:

| Attribute | Value                                     |
|-----------|-------------------------------------------|
| namespace | com.yahoo.ecosystem.mobile_payment.parsec |
| version   | 1                                         |


## Resources

### [MpNullResult](#MpNullResult)

#### POST /creditCardAuths

Authorize a card by ssl


#### Request parameters:

| Name           | Type                                  | Source | Options | Description |
|----------------|---------------------------------------|--------|---------|-------------|
| creditCardAuth | [MpCreditCardAuth](#mpcreditcardauth) | body   |         |             |


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


#### POST /creditCard3dAuthsResult

3D authorize callback to set result from CCP


#### Request parameters:

| Name                 | Type                                              | Source | Options | Description |
|----------------------|---------------------------------------------------|--------|---------|-------------|
| creditCardAuthResult | [MpCreditCardAuthResult](#mpcreditcardauthresult) | body   |         |             |


#### Responses:

Expected:

| Code   | Type         |
|--------|--------------|
| 200 OK | MpNullResult |


Exception:

| Code                      | Type                                        | Comment |
|---------------------------|---------------------------------------------|---------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) |         |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) |         |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |         |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) |         |


#### DELETE /creditCardAuths

Delete the transactions of user.


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


### [CreditCardAuthResult](#CreditCardAuthResult)

#### POST /creditCard3dAuths

Authorize a card by 3d


#### Request parameters:

| Name           | Type                                  | Source | Options | Description |
|----------------|---------------------------------------|--------|---------|-------------|
| creditCardAuth | [MpCreditCardAuth](#mpcreditcardauth) | body   |         |             |


#### Responses:

Expected:

| Code   | Type                 |
|--------|----------------------|
| 200 OK | CreditCardAuthResult |


Exception:

| Code                      | Type                                        | Comment |
|---------------------------|---------------------------------------------|---------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) |         |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) |         |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |         |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) |         |


### [MpCreditCardAuthCollection](#MpCreditCardAuthCollection)

#### GET /creditCardAuths

#### Request parameters:

| Name   | Type  | Source        | Options                 | Description                                        |
|--------|-------|---------------|-------------------------|----------------------------------------------------|
| offset | int32 | query: offset | optional                | Offset of items of results.                        |
| count  | int32 | query: count  | optional                | Number of items to return.                         |
| sync   | Bool  | query: sync   | optional, default=false | Sync with bastet or not, only support if count = 0 |


#### Responses:

Expected:

| Code   | Type                       |
|--------|----------------------------|
| 200 OK | MpCreditCardAuthCollection |


Exception:

| Code                      | Type                                        | Comment |
|---------------------------|---------------------------------------------|---------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) |         |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) |         |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |         |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) |         |


### [MpCheckResult](#MpCheckResult)

#### POST /creditCardAuths/checkByCardNumber

Check credit card number has set in bastet and ccv verified.


#### Request parameters:

| Name           | Type                                  | Source | Options | Description                        |
|----------------|---------------------------------------|--------|---------|------------------------------------|
| creditCardAuth | [MpCreditCardAuth](#mpcreditcardauth) | body   |         | The credit card number user input. |


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

### <a name="MpCreditCardAuth"></a> MpCreditCardAuth
`MpCreditCardAuth` is a `Struct` type with the following fields:

| Name       | Type   | Options | Description | Notes |
|------------|--------|---------|-------------|-------|
| cardId     | String |         |             |       |
| cvv2       | String |         |             |       |
| passcode   | String |         |             |       |
| cardNumber | String |         |             |       |


### <a name="CreditCardAuthResult"></a> CreditCardAuthResult
`CreditCardAuthResult` is a `Struct` type with the following fields:

| Name             | Type   | Options  | Description                                           | Notes |
|------------------|--------|----------|-------------------------------------------------------|-------|
| support3d        | Bool   |          | is the card support 3d?                               |       |
| retCode          | Int32  |          |                                                       |       |
| success          | Bool   | optional | not support 3D, will return SSL auth result directly. |       |
| creditCardAuthId | String | optional | support 3D, redirect to 3d auth page.                 |       |
| accessUrl        | String | optional |                                                       |       |


### <a name="MpCreditCardAuthResult"></a> MpCreditCardAuthResult
`MpCreditCardAuthResult` is a `Struct` type with the following fields:

| Name               | Type   | Options | Description | Notes |
|--------------------|--------|---------|-------------|-------|
| payment_session_id | String |         |             |       |
| platform_id        | String |         |             |       |
| bill_id            | String |         |             |       |


### <a name="MpCreditCardAuthCollection"></a> MpCreditCardAuthCollection
`MpCreditCardAuthCollection` is a `Struct` type with the following fields:

| Name            | Type                                               | Options | Description                                                                                    | Notes |
|-----------------|----------------------------------------------------|---------|------------------------------------------------------------------------------------------------|-------|
| creditCardAuths | Array&lt;[MpCreditCardAuth](#mpcreditcardauth)&gt; |         |                                                                                                |       |
| totalResults    | Int32                                              |         | Number of creditCardAuth returned                                                              |       |
| nextOffset      | Int32                                              |         | If there is more result, the nextOffset can pass to next query, return -1 if no offset anymore |       |


[Swagger URL](https://git.corp.yahoo.com/pages/ApexTest/Swagger-UI/parsec/swagger-ui/?url=https://git.corp.yahoo.com/pages/ApexTest/project_1503989415696/swagger-json/creditcard_swagger.json)
