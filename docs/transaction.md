# The Transaction API

This API has the following attributes:

| Attribute | Value                                     |
|-----------|-------------------------------------------|
| namespace | com.yahoo.ecosystem.mobile_payment.parsec |
| version   | 1                                         |


## Resources

### [MpPaymentToken](#MpPaymentToken)

#### POST /paymentTokens

Generate token for mobile payment. authenticate by ytcookie & wssid


#### Request parameters:

| Name         | Type                              | Source | Options | Description         |
|--------------|-----------------------------------|--------|---------|---------------------|
| paymentToken | [MpPaymentToken](#mppaymenttoken) | body   |         | Token request data. |


#### Responses:

Expected:

| Code        | Type                              |
|-------------|-----------------------------------|
| 201 CREATED | [MpPaymentToken](#mppaymenttoken) |


Exception:

| Code                      | Type                                        | Comment |
|---------------------------|---------------------------------------------|---------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) |         |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) |         |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |         |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) |         |


### [MpNullResult](#MpNullResult)

#### PUT /paymentTokens/{tokenId}

Update token position. authenticate by ytcookie & wssid


#### Request parameters:

| Name         | Type                              | Source | Options | Description                       |
|--------------|-----------------------------------|--------|---------|-----------------------------------|
| tokenId      | String                            | path   |         | The token id                      |
| paymentToken | [MpPaymentToken](#mppaymenttoken) | body   |         | Token request data to be updated. |


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


#### DELETE /transactions

Delete the transaction of user.


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


### [MpTransactionCollection](#MpTransactionCollection)

#### GET /transactions

list transactions belong to the user


#### Request parameters:

| Name      | Type                        | Source           | Options                      | Description                                               |
|-----------|-----------------------------|------------------|------------------------------|-----------------------------------------------------------|
| offset    | int32                       | query: offset    | optional, default=0          | Offset of items of results.                               |
| count     | int32                       | query: count     | optional, default=10         | Number of items to return.                                |
| startTs   | [DateTime](#datetime)       | query: startTs   |                              | Resource create time as the start range.                  |
| endTs     | [DateTime](#datetime)       | query: endTs     |                              | Resource create time as the end range.                    |
| sortBy    | String                      | query: sortBy    | optional, default=createTime | sort by specific field, only support createTime for now   |
| sortOrder | [MpSortOrder](#mpsortorder) | query: sortOrder | optional, default=ASC        | Sort based on order of results.                           |
| detail    | Bool                        | query: detail    | optional, default=false      | Show summary txns or full detail txns, default is summary |


#### Responses:

Expected:

| Code   | Type                    |
|--------|-------------------------|
| 200 OK | MpTransactionCollection |


Exception:

| Code                      | Type                                        | Comment |
|---------------------------|---------------------------------------------|---------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) |         |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) |         |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |         |
| 500 Internal Server Error | [ParsecResourceError](#parsecresourceerror) |         |


### [MpTransaction](#MpTransaction)

#### GET /transactions/{transactionId}

#### Request parameters:

| Name          | Type   | Source | Options | Description        |
|---------------|--------|--------|---------|--------------------|
| transactionId | String | path   |         | The transaction id |


#### Responses:

Expected:

| Code   | Type          |
|--------|---------------|
| 200 OK | MpTransaction |


Exception:

| Code                      | Type                                        | Comment |
|---------------------------|---------------------------------------------|---------|
| 400 Bad Request           | [ParsecResourceError](#parsecresourceerror) |         |
| 401 Unauthorized          | [ParsecResourceError](#parsecresourceerror) |         |
| 403 Forbidden             | [ParsecResourceError](#parsecresourceerror) |         |
| 404 Not Found             | [ParsecResourceError](#parsecresourceerror) |         |
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

### <a name="MpPaymentType"></a> MpPaymentType
`MpPaymentType` is an `Enum` of the following values:

| Value             | Description |
|-------------------|-------------|
| CREDIT_CARD_TOKEN |             |


### <a name="MpPaymentToken"></a> MpPaymentToken

Token data.

`MpPaymentToken` is a `Struct` type with the following fields:

| Name           | Type                            | Options | Description                               | Notes |
|----------------|---------------------------------|---------|-------------------------------------------|-------|
| id             | String                          |         | Token id.                                 |       |
| tokenValue     | String                          |         | Token value.                              |       |
| expire         | [DateTime](#datetime)           |         | Token expire time.                        |       |
| expireDuration | Int64                           |         |                                           |       |
| creditCardId   | String                          |         | The credit card id in bastet for payment. |       |
| buyerId        | [GUID](#guid)                   |         |                                           |       |
| payType        | [MpPaymentType](#mppaymenttype) |         |                                           |       |
| ccode          | String                          |         |                                           |       |
| property       | String                          |         |                                           |       |
| longitude      | String                          |         |                                           |       |
| latitude       | String                          |         |                                           |       |
| passCode       | String                          |         | The user's passcode.                      |       |


### <a name="MpTransactionType"></a> MpTransactionType
`MpTransactionType` is an `Enum` of the following values:

| Value  | Description |
|--------|-------------|
| PAY    |             |
| REFUND |             |


### <a name="MpTransStatus"></a> MpTransStatus
`MpTransStatus` is an `Enum` of the following values:

| Value      | Description |
|------------|-------------|
| NOT_PAID   |             |
| PAID_OK    |             |
| PAY_FAILED |             |
| CANCELLED  |             |
| INVALID    |             |


### <a name="MpRefundStatus"></a> MpRefundStatus
`MpRefundStatus` is an `Enum` of the following values:

| Value     | Description |
|-----------|-------------|
| INIT      |             |
| DONE      |             |
| CANCELLED |             |


### <a name="MpApplyPointStatus"></a> MpApplyPointStatus
`MpApplyPointStatus` is an `Enum` of the following values:

| Value         | Description |
|---------------|-------------|
| TO_BE_APPLIED |             |
| APPLIED       |             |


### <a name="MpTransCreditCardSubType"></a> MpTransCreditCardSubType
`MpTransCreditCardSubType` is an `Enum` of the following values:

| Value            | Description |
|------------------|-------------|
| YAHOO_CO_BRANDED |             |


### <a name="MpSortOrder"></a> MpSortOrder
`MpSortOrder` is an `Enum` of the following values:

| Value | Description                      |
|-------|----------------------------------|
| ASC   | ascending order descending order |
| DESC  |                                  |


### <a name="MpPartnerId"></a> MpPartnerId
`MpPartnerId` is an `Enum` of the following values:

| Value | Description |
|-------|-------------|
| CTCB  |             |


### <a name="MpTransErrorCode"></a> MpTransErrorCode
`MpTransErrorCode` is an `Enum` of the following values:

| Value                      | Description |
|----------------------------|-------------|
| OK                         |             |
| CARD_NOT_SUPPORTED         |             |
| CARD_EXPIRED               |             |
| EXCEEDED_CREDIT_LIMIT      |             |
| EXCEEDED_TRANSACTION_LIMIT |             |
| SYSTEM_UNDER_MAINTENANCE   |             |


### <a name="MpTransaction"></a> MpTransaction
`MpTransaction` is a `Struct` type with the following fields:

| Name             | Type                                                  | Options  | Description | Notes |
|------------------|-------------------------------------------------------|----------|-------------|-------|
| id               | String                                                |          |             |       |
| transType        | [MpTransactionType](#mptransactiontype)               |          |             |       |
| payType          | [MpPaymentType](#mppaymenttype)                       |          |             |       |
| buyerId          | [GUID](#guid)                                         |          |             |       |
| ccode            | String                                                |          |             |       |
| property         | String                                                |          |             |       |
| amount           | String                                                |          |             |       |
| currency         | String                                                |          |             |       |
| realAmount       | String                                                |          |             |       |
| usedPoints       | String                                                | optional |             |       |
| summary          | String                                                | optional |             |       |
| detail           | String                                                | optional |             |       |
| status           | [MpTransStatus](#mptransstatus)                       |          |             |       |
| partnerOrderId   | String                                                | optional |             |       |
| date             | [DateTime](#datetime)                                 |          |             |       |
| cancelDate       | [DateTime](#datetime)                                 | optional |             |       |
| partnerId        | [MpPartnerId](#mppartnerid)                           |          |             |       |
| partnerTxSeq     | String                                                |          |             |       |
| merchantId       | String                                                |          |             |       |
| merchantName     | String                                                |          |             |       |
| corpId           | String                                                |          |             |       |
| corpTxSeq        | String                                                |          |             |       |
| corpTxTime       | [DateTime](#datetime)                                 |          |             |       |
| storeId          | String                                                | optional |             |       |
| storeName        | String                                                | optional |             |       |
| creditCardId     | String                                                |          |             |       |
| ccFirstDigits    | String                                                |          |             |       |
| ccLastDigits     | String                                                |          |             |       |
| ccSubType        | [MpTransCreditCardSubType](#mptranscreditcardsubtype) |          |             |       |
| ccDisplayName    | String                                                |          |             |       |
| appliedPoints    | String                                                |          |             |       |
| refundStatus     | [MpRefundStatus](#mprefundstatus)                     |          |             |       |
| applyPointStatus | [MpApplyPointStatus](#mpapplypointstatus)             |          |             |       |
| paidDate         | [DateTime](#datetime)                                 |          |             |       |
| createTime       | [DateTime](#datetime)                                 |          |             |       |
| modifyTime       | [DateTime](#datetime)                                 |          |             |       |
| longitude        | String                                                |          |             |       |
| latitude         | String                                                |          |             |       |
| errorCode        | [MpTransErrorCode](#mptranserrorcode)                 |          |             |       |


### <a name="MpTransactionCollection"></a> MpTransactionCollection
`MpTransactionCollection` is a `Struct` type with the following fields:

| Name         | Type                                         | Options | Description                                                                                    | Notes |
|--------------|----------------------------------------------|---------|------------------------------------------------------------------------------------------------|-------|
| transactions | Array&lt;[MpTransaction](#mptransaction)&gt; |         | A list of transaction                                                                          |       |
| totalResults | Int32                                        |         | Number of transactions returned                                                                |       |
| nextOffset   | Int32                                        |         | If there is more result, the nextOffset can pass to next query, return -1 if no offset anymore |       |


[Swagger URL](https://git.corp.yahoo.com/pages/ApexTest/Swagger-UI/parsec/swagger-ui/?url=https://git.corp.yahoo.com/pages/ApexTest/project_1503989415696/swagger-json/transaction_swagger.json)
