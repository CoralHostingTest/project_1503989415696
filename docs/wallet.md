# The Wallet API

This API has the following attributes:

| Attribute | Value                                     |
|-----------|-------------------------------------------|
| namespace | com.yahoo.ecosystem.mobile_payment.parsec |
| version   | 1                                         |


## Resources

### [string](#string)

#### POST /wallet

#### Request parameters:

| Name | Type   | Source               | Options | Description |
|------|--------|----------------------|---------|-------------|
| body | string | body                 |         |             |
| sign | string | header: Req-Msg-Sign |         |             |


#### Responses:

Expected:

| Code   | Type   |
|--------|--------|
| 200 OK | string |


Exception:

| Code                      | Type          | Comment |
|---------------------------|---------------|---------|
| 400 Bad Request           | ResourceError |         |
| 401 Unauthorized          | ResourceError |         |
| 403 Forbidden             | ResourceError |         |
| 500 Internal Server Error | ResourceError |         |


[Swagger URL](https://git.corp.yahoo.com/pages/ApexTest/Swagger-UI/parsec/swagger-ui/?url=https://git.corp.yahoo.com/pages/ApexTest/project_1503989415696/swagger-json/wallet_swagger.json)
