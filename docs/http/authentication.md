# API-key Authentication

To use HTTP API Endpoints, you need to provide your enabled API-key with available Tickets to authenticate that your access to it is valid.

This article describes how HTTP API Endpoint performs authentication.

## Authorization Header

HTTP API Endpoint uses Authorization Header to check whether the user is allowed to access the endpoint.

Every query to the endpoint must contain API-key as Authorization Header like below:

```header
Authorization: bearer <Your API-key>
```

## Curl Example

This is a few example of queries using curl command.

```bash
curl --header 'Authorization:bearer <Your API-key>' https://api.exchangedataset.cc/v1/filter/bitmex/1589120055?channels=orderBookL2
curl --header 'Authorization:bearer <Your API-key>' https://api.exchangedataset.cc/v1/snapshot/bitmex/1589102088123456789?channels=orderBookL2
```
