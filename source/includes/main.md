# Introduction

Welcome to the HealthStream API Library. Here you can find all the information you're looking for from **To Do Items** to HLCData Items.

We have language bindings in C# and the JavaScript to call them. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Getting Started

## Client Credential Setup

## List of Available APIs

### To Do API 1.1.0

# Authentication

> To authorize, use this code:

```c
private async Task GetTokenAsync()
{
var client = new TokenClient(
"https://www.healthstream.com/STS/connect/token",
"HealthStream Client ID", // This is your HealthStream STS Client id
"HealthStream STS secret key"); // This is your HealthStream STS secret key
return await client.RequestClientCredentialsAsync("api"); // "api" is the scope
}
```

```javascript
None
```

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImowZmluQ1ppaUZjQlUybklLWDA3QmNSWHhQZyIsImtpZCI6ImowZmluQ1ppaUZjQlUybklLWDA3QmNSWHhQZyJ9.eyJjbGllbnRfaWQiOiJlY2hvIiwic2NvcGUiOiJhcGkiLCJpc3MiOiJodHRwOi8vd3d3LmhlYWx0aHN0cmVhbS5jb20vU1RTIiwiYXVkIjoiaHR0cDovL3d3dy5oZWFsdGhzdHJlYW0uY29tL1NUUy9yZXNvdXJjZXMiLCJleHAiOjE0OTcwMTQ5ODUsIm5iZiI6MTQ5NzAxNDkyNX0.jACCBuCPmPjy70ng85TLI38cBPhAhSka68JmiHQe2zivkifQbf86itWgpCI1oYSbLI0_71quqjvcSXmAFW9ViPiYpXfJRqMkqT9gUHsqCfbcWHq4C4TCjyJp6Ks0pQYUt4X-GTmfcqF43D75d_LP10s6a7opz8Xunwt85VpnGoqdoBelOUeRbXskybNEWGKr9_i0Btpq8vU2xzz6bAhfb2TIXgkv_twJ9PnV_y6oikUeIs8FlYWOcROarSjvuLxF0xCKlLEplfrm99bgmXpjDuz5Qp54dn2Hi59qtJ3EYNsRhmZA7nqBnxZ5cCsNUNsD6-MnlA3VsTAt80U9KYyUYg",
    "expires_in": 60,
    "token_type": "Bearer"
}
```

> Note: You will need to install the IdentityModel NuGet package to create a TokenClient

**Request Details**

URL: POST https://www.healthstream.com/STS/connect/token

**Header Parameters**
- Authorization: Basic ZWNobzozd1hrJlZHRX1UblJnNTgm
- Content-Type: application/x-w w w -form-urlencoded

**Body**
- grant_type: client_credentials
- scope: api


<aside class="notice">
You must put your token inside the header to access the API.
</aside>

# To Do API

## GetAssignedLearningCount Endpoint

```c
private async Task<string> GetAssignedLearning(Guid orgId, Guid userId)
{
       using (var client = new HttpClient())
       {
              client.BaseAddress = new Uri("https://www.healthstream.com/api/hs/ToDo/V1/");

              // Get an authorization token. The generated token will expire every 60 second.
              // You can utilize the same token across many request as long as it is not expired.
              var token = (await GetTokenAsync()).AccessToken.Dump("The generated token");

              // Adding the authorization header attribute.
              client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);

              var resource = string.Format("api/GetAssignedLearningCount(userId={0},orgId={1})", userId, orgId);

              var response = await client.GetAsync(resource);

              return response.StatusCode == HttpStatusCode.OK
              ? JObject.Parse(await response.Content.ReadAsStringAsync())["value"].ToString()
              : null;
       }
}

```

> The above command returns JSON structured like this:

```json
{
    "@odata.context": "http://www.healthstream.com/ToDo/V1/api/$metadata#Edm.Int32",
    "value": 9
}
```

This endpoint returns the number of assigned learning items for a particular user in a particular org.

### HTTP Request

`GET https://www.healthstream.com/api/hs/ToDo/V1/api/GetAssignedLearningCount(userId=userId,orgId=orgId)`

### Header Parameters

- Authorization: *access_token received from the request made in Acquire Authorization Token*

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```bash
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve
