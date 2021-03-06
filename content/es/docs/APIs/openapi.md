---
title: MasMovil Ticketing API - Inbound (External Systems > MasMovil)
language_tabs:
  - java: Java
  - go: Go
  - ‘javascript: JavaScript’
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<h1 id="masmovil-ticketing-api-inbound-external-systems-masmovil-">MasMovil Ticketing API - Inbound (External Systems > MasMovil) v1.1.8</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

This is the ticketing-api server.

Base URLs:

* <a href="{protocol}://{environment}">{protocol}://{environment}</a>

    * **protocol** -  Default: https

        * https

        * http

    * **environment** -  Default: ticketing.dev.k8s.masmovil.com/v1/api

        * 0.0.0.0:8080

        * ticketing.dev.k8s.masmovil.com/v1/api

        * ticketing.private.sta.k8s.masmovil.com/v1/api

Email: <a href="mailto:ticketing_squad@masmovil.com">Support</a> 

# Authentication

- HTTP Authentication, scheme: bearer 

<h1 id="masmovil-ticketing-api-inbound-external-systems-masmovil--ticket">Ticket</h1>

Operations about Tickets

## createTicket

<a id="opIdcreateTicket"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/ticket");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "{protocol}://{environment}/ticket", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /ticket`

*Create new ticket*

Creates a ticket in MasMovil ticketing tool.

> Body parameter

```json
{
  "project": "IDR",
  "summary": "Ticket summary",
  "description": "This is a ticket description example",
  "ticketType": "Incidencia Red",
  "createdDate": "2019-08-20T10:29:29.908+1100",
  "massive": "NO",
  "criticality": "N1-Crítica o de corte",
  "unavailability": "SI",
  "affectedNetworkElement": "Network Element",
  "affectedNetworkType": "Voz-Red Mercurio",
  "affectedBusiness": "Empresas",
  "eventStartDate": "2019-08-19T10:29:29.908+1100",
  "title": "test"
}
```

<h3 id="createticket-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|object|true|Fields needed to create a ticket in MasMovil Ticketing tool|

> Example responses

> 201 Response

```json
{
  "id": "123456789",
  "key": "##-1234"
}
```

<h3 id="createticket-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[inline_response_201](#schemainline_response_201)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## getTicketById

<a id="opIdgetTicketById"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/ticket/{ticketId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "{protocol}://{environment}/ticket/{ticketId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /ticket/{ticketId}`

*Get a ticket by id*

Retrieves the details of a ticket that has previously been created.

<h3 id="getticketbyid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|ticketId|path|string|true|The Ticket ID in MasMovil ticketing tool. You can use either ID or KEY.|
|expand|query|array[string]|false|Filter for ticket response body. (You must add 'attachment' query param to get ticket attachments in response body)|
|x-api-key|header|string|true|none|

#### Enumerated Values

|Parameter|Value|
|---|---|
|expand|attachment|

> Example responses

> 200 Response

```json
{
  "id": "3240786",
  "status": "EN CURSO",
  "summary": "ERI_MM_OLTZ3562010LAP012_para que se revise",
  "description": "ERI_MM_OLTZ3562010LAP012_para que se revise",
  "priority": "Medium",
  "ticketType": "Incidencia Red",
  "project": "IDR",
  "createdDate": "2018-02-28T17:43:38.000+0100",
  "attachment": {
    "name": "attachment.txt",
    "data": "SGVsbG8gd29ybGQgZnJvbSBNUywgY2hhbmdlZA==",
    "mimeType": "multipart/form-data"
  }
}
```

<h3 id="getticketbyid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Ticket response|[TicketResponse](#schematicketresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## updateTicket

<a id="opIdupdateTicket"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/ticket/{ticketId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PATCH");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PATCH", "{protocol}://{environment}/ticket/{ticketId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`PATCH /ticket/{ticketId}`

*Update an existing ticket*

This service can be used to update ticket information.

For udating ticket status, you must provide a transtition ID to apply. You can get this ID through this *GET* request: **/ticket/{ticketId}/transitions**

If your system needs to use a callback to send back information about previous MasMovil request, you must use this service using especified integration fields.

> Body parameter

```json
{
  "transitionId": 11
}
```

<h3 id="updateticket-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|ticketId|path|string|true|The Ticket ID in MasMovil ticketing tool. You can use either ID or KEY.|
|x-api-key|header|string|true|none|
|body|body|object|true|Body must include the ticket fields that need to be updated.|

#### Detailed descriptions

**body**: Body must include the ticket fields that need to be updated.
See examples below.

> Example responses

> 400 Response

```json
{
  "code": "0015",
  "status": "BAD_REQUEST",
  "message": "Bad Request",
  "detailMsg": "string"
}
```

<h3 id="updateticket-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|No Content|None|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## addAttachment

<a id="opIdaddAttachment"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/ticket/{ticketId}/attachment");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "{protocol}://{environment}/ticket/{ticketId}/attachment", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /ticket/{ticketId}/attachment`

*Add attachment to ticket*

> Body parameter

```json
{
  "name": "image_example.jpg",
  "data": "R0lGODdhAQABAPAAAP8AAAAAACwAAAAAAQABAAACAkQBADs"
}
```

<h3 id="addattachment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|ticketId|path|string|true|The Ticket ID in MasMovil ticketing tool. You can use either ID or KEY.|
|x-api-key|header|string|true|none|
|body|body|object|true|Both fields name and data are required.|

#### Detailed descriptions

**body**: Both fields name and data are required.
Data must be base64 encoded.

> Example responses

> 201 Response

```json
{
  "message": "Attachment added successfully."
}
```

<h3 id="addattachment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[inline_response_201_1](#schemainline_response_201_1)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## addComment

<a id="opIdaddComment"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/ticket/{ticketId}/comment");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "{protocol}://{environment}/ticket/{ticketId}/comment", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /ticket/{ticketId}/comment`

*Add comment to ticket*

> Body parameter

```json
{
  "body": "This is a comment example"
}
```

<h3 id="addcomment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|ticketId|path|string|true|The Ticket ID in MasMovil ticketing tool. You can use either ID or KEY.|
|x-api-key|header|string|true|none|
|body|body|object|true|Property body is mandatory.|

> Example responses

> 201 Response

```json
{
  "message": "Comment added successfully."
}
```

<h3 id="addcomment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[inline_response_201_2](#schemainline_response_201_2)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## post__ticket_{ticketId}_attachmentWithComment

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/ticket/{ticketId}/attachmentWithComment");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "{protocol}://{environment}/ticket/{ticketId}/attachmentWithComment", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /ticket/{ticketId}/attachmentWithComment`

*Add attachment with comment to ticket*

> Body parameter

```json
{}
```

<h3 id="post__ticket_{ticketid}_attachmentwithcomment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|ticketId|path|string|true|The Ticket ID in MasMovil ticketing tool. You can use either ID or KEY.|
|x-api-key|header|string|true|none|
|body|body|object|true|Both comment and attachment are mandatory.|

> Example responses

> 201 Response

```json
{
  "message": "Attachment with comment added successfully."
}
```

<h3 id="post__ticket_{ticketid}_attachmentwithcomment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[inline_response_201_3](#schemainline_response_201_3)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## getFieldInformation

<a id="opIdgetFieldInformation"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/ticket/field/{fieldName}?projectKey=MAS");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "{protocol}://{environment}/ticket/field/{fieldName}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /ticket/field/{fieldName}`

*Get information about an API field. It returns info about MasMovil ticketing tool field name and allowed values.*

<h3 id="getfieldinformation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|fieldName|path|string|true|The field name in MasMovil ticketing API.|
|projectKey|query|array[string]|true|The project key in MasMovil ticketing tool|
|x-api-key|header|string|true|none|

#### Enumerated Values

|Parameter|Value|
|---|---|
|projectKey|MAS|

> Example responses

> 200 Response

```json
{
  "required": true,
  "name": "Titulo de la incidencia"
}
```

<h3 id="getfieldinformation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get field information|[FieldResponse](#schemafieldresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## getAllowedTransitions

<a id="opIdgetAllowedTransitions"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/ticket/{ticketId}/transitions");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "{protocol}://{environment}/ticket/{ticketId}/transitions", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /ticket/{ticketId}/transitions`

*Get information about allowed transitions for a ticket.*

<h3 id="getallowedtransitions-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|ticketId|path|string|true|The Ticket ID in MasMovil ticketing tool. You can use either ID or KEY.|
|x-api-key|header|string|true|none|

> Example responses

> 200 Response

```json
{
  "transitions": [
    {
      "id": 41,
      "name": "Reasignar",
      "status": "Asignado"
    },
    {
      "id": 21,
      "name": "Resolver",
      "status": "RESUELTO"
    }
  ]
}
```

<h3 id="getallowedtransitions-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get transitions|[TransitionsResponse](#schematransitionsresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## getFieldsForTicketType

<a id="opIdgetFieldsForTicketType"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/creationDataInfo?projectKey=MAS&ticketType=Aver%C3%ADa%20%28FTTH%29");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "{protocol}://{environment}/creationDataInfo", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /creationDataInfo`

*Get information about fields needed to create a given type of ticket*

<h3 id="getfieldsfortickettype-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|projectKey|query|array[string]|true|The project key in MasMovil ticketing tool|
|ticketType|query|array[string]|true|The ticket type in MasMovil ticketing tool|
|x-api-key|header|string|true|none|

#### Enumerated Values

|Parameter|Value|
|---|---|
|projectKey|MAS|
|ticketType|Avería (FTTH)|
|ticketType|Avería Cliente|
|ticketType|Incidencia|
|ticketType|Reclamación Instalación|
|ticketType|Cancelación Cliente|

> Example responses

> 200 Response

```json
{
  "subscriptionNumber": {
    "required": true,
    "name": "Suscripción"
  },
  "icc": {
    "required": false,
    "name": "ICC"
  },
  "contactEmail": {
    "required": false,
    "name": "Email del Cliente"
  }
}
```

<h3 id="getfieldsfortickettype-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Fields for ticket type|[CreationDataInfo](#schemacreationdatainfo)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## getTicketTypes

<a id="opIdgetTicketTypes"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/project/ticketTypes");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "{protocol}://{environment}/project/ticketTypes", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /project/ticketTypes`

*Get information about ticket types per project*

<h3 id="gettickettypes-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|

> Example responses

> 200 Response

```json
{
  "projects": [
    {
      "key": "string",
      "name": "string",
      "ticketTypes": [
        {
          "name": "string",
          "description": "string"
        }
      ]
    }
  ]
}
```

<h3 id="gettickettypes-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Get ticket types|[TicketTypesResponse](#schematickettypesresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## getEditableFields

<a id="opIdgetEditableFields"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/ticket/{ticketId}/editableFields");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "{protocol}://{environment}/ticket/{ticketId}/editableFields", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /ticket/{ticketId}/editableFields`

*Get information about editable fields for a ticket*

<h3 id="geteditablefields-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|ticketId|path|string|true|The Ticket ID in MasMovil ticketing tool. You can use either ID or KEY.|

> Example responses

> 200 Response

```json
{
  "description": {
    "name": "Descripción",
    "required": true
  },
  "customerPostalCode": {
    "name": "Código Postal",
    "required": false
  },
  "customerSegment": {
    "name": "Segmento Cliente",
    "required": false,
    "allowedValues": [
      {
        "value": "EMPRESA"
      },
      {
        "value": "RESIDENCIAL"
      },
      {
        "value": "HORECA"
      },
      {
        "value": "AUTONOMO"
      }
    ]
  }
}
```

<h3 id="geteditablefields-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Editable Fields for ticket|[EditableFields](#schemaeditablefields)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

## searchTickets

<a id="opIdsearchTickets"></a>

> Code samples

```java
URL obj = new URL("{protocol}://{environment}/search");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        "Authorization": []string{"Bearer {access-token}"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "{protocol}://{environment}/search", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /search`

*Search tickets*

You can add fields to filter tickets. Allowed special opeators are $like:value and $in:[array], maxResults default results is 10.
Fields to return must be specified in "fields" json property.
Field names used in filters can be both Jira field name or ms-ticketing-API name, i.e.: you can use "customerDocument" or "Documento Cliente".

> Body parameter

```json
{
  "filters": {
    "project": "MAS",
    "customerDocument": {
      "$like": "50744198B"
    }
  },
  "startAt": 0,
  "maxResults": 10,
  "fields": [
    "key",
    "summary",
    "issuetype",
    "status"
  ]
}
```

<h3 id="searchtickets-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|none|
|body|body|object|true|Filters to apply to search query|

> Example responses

> 200 Response

```json
[
  {
    "id": "3240786",
    "status": "EN CURSO",
    "summary": "ERI_MM_OLTZ3562010LAP012_para que se revise",
    "description": "ERI_MM_OLTZ3562010LAP012_para que se revise",
    "priority": "Medium",
    "ticketType": "Incidencia Red",
    "project": "IDR",
    "createdDate": "2018-02-28T17:43:38.000+0100",
    "attachment": {
      "name": "attachment.txt",
      "data": "SGVsbG8gd29ybGQgZnJvbSBNUywgY2hhbmdlZA==",
      "mimeType": "multipart/form-data"
    }
  }
]
```

<h3 id="searchtickets-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Ticket response|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|[Error400](#schemaerror400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[Error401](#schemaerror401)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|[Error404](#schemaerror404)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Internal Server Error|[Error500](#schemaerror500)|

<h3 id="searchtickets-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[TicketResponse](#schematicketresponse)]|false|none|none|
|» id|string|false|none|none|
|» status|string|false|none|none|
|» summary|string|false|none|none|
|» description|string|false|none|none|
|» priority|string|false|none|none|
|» ticketType|string|false|none|none|
|» project|string|false|none|none|
|» createdDate|string|false|none|none|
|» attachment|[TicketResponse_attachment](#schematicketresponse_attachment)|false|none|none|
|»» name|string|false|none|none|
|»» data|string|false|none|none|
|»» mimeType|string|false|none|none|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
bearerAuth
</aside>

# Schemas

<h2 id="tocSticketresponse">TicketResponse</h2>

<a id="schematicketresponse"></a>

```json
{
  "id": "3240786",
  "status": "EN CURSO",
  "summary": "ERI_MM_OLTZ3562010LAP012_para que se revise",
  "description": "ERI_MM_OLTZ3562010LAP012_para que se revise",
  "priority": "Medium",
  "ticketType": "Incidencia Red",
  "project": "IDR",
  "createdDate": "2018-02-28T17:43:38.000+0100",
  "attachment": {
    "name": "attachment.txt",
    "data": "SGVsbG8gd29ybGQgZnJvbSBNUywgY2hhbmdlZA==",
    "mimeType": "multipart/form-data"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|none|
|status|string|false|none|none|
|summary|string|false|none|none|
|description|string|false|none|none|
|priority|string|false|none|none|
|ticketType|string|false|none|none|
|project|string|false|none|none|
|createdDate|string|false|none|none|
|attachment|[TicketResponse_attachment](#schematicketresponse_attachment)|false|none|none|

<h2 id="tocSfieldresponse">FieldResponse</h2>

<a id="schemafieldresponse"></a>

```json
{
  "required": true,
  "name": "Titulo de la incidencia"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|required|boolean|false|none|none|
|name|string|false|none|none|

<h2 id="tocScreationdatainfo">CreationDataInfo</h2>

<a id="schemacreationdatainfo"></a>

```json
{
  "subscriptionNumber": {
    "required": true,
    "name": "Suscripción"
  },
  "icc": {
    "required": false,
    "name": "ICC"
  },
  "contactEmail": {
    "required": false,
    "name": "Email del Cliente"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|subscriptionNumber|[CreationDataInfo_subscriptionNumber](#schemacreationdatainfo_subscriptionnumber)|false|none|none|
|icc|[CreationDataInfo_icc](#schemacreationdatainfo_icc)|false|none|none|
|contactEmail|[CreationDataInfo_contactEmail](#schemacreationdatainfo_contactemail)|false|none|none|

<h2 id="tocSeditablefields">EditableFields</h2>

<a id="schemaeditablefields"></a>

```json
{
  "description": {
    "name": "Descripción",
    "required": true
  },
  "customerPostalCode": {
    "name": "Código Postal",
    "required": false
  },
  "customerSegment": {
    "name": "Segmento Cliente",
    "required": false,
    "allowedValues": [
      {
        "value": "EMPRESA"
      },
      {
        "value": "RESIDENCIAL"
      },
      {
        "value": "HORECA"
      },
      {
        "value": "AUTONOMO"
      }
    ]
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|description|[EditableFields_description](#schemaeditablefields_description)|false|none|none|
|customerPostalCode|[EditableFields_customerPostalCode](#schemaeditablefields_customerpostalcode)|false|none|none|
|customerSegment|[EditableFields_customerSegment](#schemaeditablefields_customersegment)|false|none|none|

<h2 id="tocSfieldnotfound">FieldNotFound</h2>

<a id="schemafieldnotfound"></a>

```json
{
  "message": "We didn't found information about that field."
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|false|none|none|

<h2 id="tocSerror400">Error400</h2>

<a id="schemaerror400"></a>

```json
{
  "code": "0015",
  "status": "BAD_REQUEST",
  "message": "Bad Request",
  "detailMsg": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|code|string|false|none|none|
|status|string|false|none|none|
|message|string|false|none|none|
|detailMsg|string|false|none|none|

<h2 id="tocSerror401">Error401</h2>

<a id="schemaerror401"></a>

```json
{
  "code": "0003",
  "status": "UNAUTHORIZED",
  "message": "Unauthorized",
  "detailMsg": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|code|string|false|none|none|
|status|string|false|none|none|
|message|string|false|none|none|
|detailMsg|string|false|none|none|

<h2 id="tocSerror404">Error404</h2>

<a id="schemaerror404"></a>

```json
{
  "code": "0004",
  "status": "NOT_FOUND",
  "message": "Not found",
  "detailMsg": "Resource not found"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|code|string|false|none|none|
|status|string|false|none|none|
|message|string|false|none|none|
|detailMsg|string|false|none|none|

<h2 id="tocSerror500">Error500</h2>

<a id="schemaerror500"></a>

```json
{
  "code": "0002",
  "status": "UNEXPECTED",
  "message": "Unexpected Error",
  "detailMsg": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|code|string|false|none|none|
|status|string|false|none|none|
|message|string|false|none|none|
|detailMsg|string|false|none|none|

<h2 id="tocStransitionsresponse">TransitionsResponse</h2>

<a id="schematransitionsresponse"></a>

```json
{
  "transitions": [
    {
      "id": 41,
      "name": "Reasignar",
      "status": "Asignado"
    },
    {
      "id": 21,
      "name": "Resolver",
      "status": "RESUELTO"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|transitions|[[TransitionsResponse_transitions](#schematransitionsresponse_transitions)]|false|none|none|

<h2 id="tocStickettypesresponse">TicketTypesResponse</h2>

<a id="schematickettypesresponse"></a>

```json
{
  "projects": [
    {
      "key": "string",
      "name": "string",
      "ticketTypes": [
        {
          "name": "string",
          "description": "string"
        }
      ]
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|projects|[[TicketTypesResponse_projects](#schematickettypesresponse_projects)]|false|none|none|

<h2 id="tocSinline_response_201">inline_response_201</h2>

<a id="schemainline_response_201"></a>

```json
{
  "id": "123456789",
  "key": "##-1234"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|none|
|key|string|false|none|none|

<h2 id="tocSinline_response_201_1">inline_response_201_1</h2>

<a id="schemainline_response_201_1"></a>

```json
{
  "message": "Attachment added successfully."
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|false|none|none|

<h2 id="tocSinline_response_201_2">inline_response_201_2</h2>

<a id="schemainline_response_201_2"></a>

```json
{
  "message": "Comment added successfully."
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|false|none|none|

<h2 id="tocSinline_response_201_3">inline_response_201_3</h2>

<a id="schemainline_response_201_3"></a>

```json
{
  "message": "Attachment with comment added successfully."
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|false|none|none|

<h2 id="tocSticketresponse_attachment">TicketResponse_attachment</h2>

<a id="schematicketresponse_attachment"></a>

```json
{
  "name": "attachment.txt",
  "data": "SGVsbG8gd29ybGQgZnJvbSBNUywgY2hhbmdlZA==",
  "mimeType": "multipart/form-data"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|data|string|false|none|none|
|mimeType|string|false|none|none|

<h2 id="tocScreationdatainfo_subscriptionnumber">CreationDataInfo_subscriptionNumber</h2>

<a id="schemacreationdatainfo_subscriptionnumber"></a>

```json
{
  "required": true,
  "name": "Suscripción"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|required|boolean|false|none|none|
|name|string|false|none|none|

<h2 id="tocScreationdatainfo_icc">CreationDataInfo_icc</h2>

<a id="schemacreationdatainfo_icc"></a>

```json
{
  "required": false,
  "name": "ICC"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|required|boolean|false|none|none|
|name|string|false|none|none|

<h2 id="tocScreationdatainfo_contactemail">CreationDataInfo_contactEmail</h2>

<a id="schemacreationdatainfo_contactemail"></a>

```json
{
  "required": false,
  "name": "Email del Cliente"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|required|boolean|false|none|none|
|name|string|false|none|none|

<h2 id="tocSeditablefields_description">EditableFields_description</h2>

<a id="schemaeditablefields_description"></a>

```json
{
  "name": "Descripción",
  "required": true
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|required|boolean|false|none|none|

<h2 id="tocSeditablefields_customerpostalcode">EditableFields_customerPostalCode</h2>

<a id="schemaeditablefields_customerpostalcode"></a>

```json
{
  "name": "Código Postal",
  "required": false
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|required|boolean|false|none|none|

<h2 id="tocSeditablefields_customersegment_allowedvalues">EditableFields_customerSegment_allowedValues</h2>

<a id="schemaeditablefields_customersegment_allowedvalues"></a>

```json
{
  "value": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|value|string|false|none|none|

<h2 id="tocSeditablefields_customersegment">EditableFields_customerSegment</h2>

<a id="schemaeditablefields_customersegment"></a>

```json
{
  "name": "Segmento Cliente",
  "required": false,
  "allowedValues": [
    {
      "value": "EMPRESA"
    },
    {
      "value": "RESIDENCIAL"
    },
    {
      "value": "HORECA"
    },
    {
      "value": "AUTONOMO"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|required|boolean|false|none|none|
|allowedValues|[[EditableFields_customerSegment_allowedValues](#schemaeditablefields_customersegment_allowedvalues)]|false|none|none|

<h2 id="tocStransitionsresponse_transitions">TransitionsResponse_transitions</h2>

<a id="schematransitionsresponse_transitions"></a>

```json
{
  "id": 0,
  "name": "string",
  "status": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|integer|false|none|none|
|name|string|false|none|none|
|status|string|false|none|none|

<h2 id="tocStickettypesresponse_tickettypes">TicketTypesResponse_ticketTypes</h2>

<a id="schematickettypesresponse_tickettypes"></a>

```json
{
  "name": "string",
  "description": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|description|string|false|none|none|

<h2 id="tocStickettypesresponse_projects">TicketTypesResponse_projects</h2>

<a id="schematickettypesresponse_projects"></a>

```json
{
  "key": "string",
  "name": "string",
  "ticketTypes": [
    {
      "name": "string",
      "description": "string"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|key|string|false|none|none|
|name|string|false|none|none|
|ticketTypes|[[TicketTypesResponse_ticketTypes](#schematickettypesresponse_tickettypes)]|false|none|none|

