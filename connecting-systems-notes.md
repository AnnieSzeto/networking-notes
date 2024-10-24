---
theme: thg-accelerator
---

# Request/Response

Request-response model, used in network protocols and systems where clients and servers interact to exchange information. (used in APIs, network communications, SSH etc.)

### Client-Server Model

Model describes communication between two computing entities over a network in a request/response method

Client Role: initiates requests for services

- Only has to understand the response based on the relevant applicaiton protocols (from application layer) (i.e. how to parse/format the data for the request)

Server Role: provides a function or service, sharing of resources

#### Application Layer

All protocols operate in an abstraction layer that specifies shared communication protocols and interface methods. The application layer abstraction is the hieghest-level layer in both the Internet Protocol Suite (TCP/IP) and the OSI model.

Internet Protocol (IP) Suite:
The application layer standardises communication and depends on transport layer protocols to establish data transfer channels and manage data exchange in client/server models.

OSI model:
The application layer is the interface responsible for communicating with host-based and user-facing applications, with two distict layers below the application layer and above the transport layer: session layer and presentation layer; each layer with its own protocol implementation

#### Architecture

Describes different ways of organising the presentation–UI layer, logic(aka application tier/niddle tier) and data layers.

1. One-Tier: When all three tiers are stored on a single device, e.g. an application that works offline and stores all data on the same device it is running from.

2. Two-Tier: When the presentation and logic layers are stored on the client's side while the data layer is stored on the server's side. Consists of client, server and protocol that links the two.

3. Three-Tier: When all three tiers are stored separately, presentation layer on the clients side, logic layers on an application server and data layers on a database server

4. N-Tier: Divides logic layers into multiple layers to improve performance, management and stability

   Non-physical: separate responsibilities, manage dependencies. Physical: runs on separate machines, improve scalability, add latency from additional network communication

   Can be closed-layer (layer can only communicate with next layer down), or open-layer (layer can communivate with any layers below).

## Client-side

Operations are performed on the client side when information/functionality is available on the client side only, e.g. when user input or observation is required or if the server lacks the processing power to perform all operations quick eough for all clients (if operations can be performed by the client without sending data over networks, less time and bandwidth is used and it incurs a lesser security risk).

Common languages on client side (WWW): CSS, HTML, JavaScript.

### Client-Side View

1. Initiates communication by sending HTTP request to a URL or server endpoint

   Requests would include HTTP methods: GET, POST, PUT, DELETE (HEAD, CONNECT OPTIONS, TRACE PATCH etc)

2. After recieving a response, the client then parses and processes the information to display the results or to perform further actions.

### Request structure

    Request Line: HTTP Methods

    Request Headers: metadata providing additional info in how to handle content (i.e. the request)

    - empty line indicating end of header

    (optional) Request Body: data sent by client

### HTTP Methods

FORMAT:

- [Name] ([Safe(Y/N)] [Idempotent(Y/N)] [Cacheable(Y/N/Conditional)]): Description

The only methods that servers are required to support are GET and HEAD.

- GET (YYY): requests a representation of the specified resource (shouldn't containe request content).
- HEAD (YYY): asks for reponse identical to GET but without a response body.
- POST (NNC): submits an entity to the specified resource (causing change in state/sideeffects on server).
- PUT (NYN): replaces all current representations of target resource with request content.
- DELETE (NYN): deletes specified resource.
- CONNECT (NNN): establishes a tunnel to server identified by target resource.
- OPTIONS (YYN): describes communication options for target resource.
- TRACE (YYN): performs message loop-back test along the path to target resource.
- PATCH (NNC): applies partial modifications to a resource

## Server Side

Operations are performed on the server-side when information/functionality is available only on the server (e.g. data) or when performing such operations on the client-side would be slow, unreliable or insecure. Operations include formulating responses to client requests and maintenance tasks

Common languages on server side (WWW): C#, Java, Python, Ruby, Node.js, etc.

### Server-side View

1. Server parses requests from clients by extracting request method, determining start/end of request.

2. Then server performs the required action such as retrieving data from database, processing the data, or generating a response.

3. The server then compiles a result to send back to the client.

### Response structure

    Status Codes: Indicates request outcome

    Response Headers: metadata indicating how to handle response body/resulting data

    Response Body: returned data

### Status Code types

1XX Informational responses. Examples:

- 100 Continue: continue request/ignore response if request is finished.
- 101 Switching Protocols: response to Upgrade request header.
- 102 Processing: indicates that a request is received but no status was available at the time of response.
- 103 Early Hints: used with Link request header, indication to start preloading resources while server prepares for a response.

2XX Successful responses. Examples:

- 200 OK: request succeeded.
- 202 Accepted: request received but not yet acted upon (for cases where another porcess/server handles the request).
- 204 No Content: no content but headers to send in response.
- 205 Reset Content: reset document which sent the request.

3XX Redirectional messages. Examples:

- 300 Multiple Choices: request has more than one possible response.
- 301 Moved Permanently: requested URL has changed permanently, new URL is given in response.
- 302 Found: requested URI has changed temporarily, same URI should be used in future requests.
- 304 Not Modified: response has not been modified, client can use the same cached version of response.

4XX Client error responses. Examples:

- 400 Bad Request: server can't/won't process request due to apparent client error.
- 401 Unauthorized: client must authenticate itself to get response.
- 403 Forbidden: client doesn't have acces rights to content (client's identity is known to server)
- 404 Not Found: URL not recognised, endpoint may be valid but resource itself doesnt exits. Servers may send this instead of 403 to hide existence of a resource from an anauthorised client.
- 408 Request Timeout: server would like to shut down an idle connection.

5XX Server error responses. Examples:

- 500 Internal Server Error: server encountereed situation it doesn't know how to handle. General code used when server can't find a more appropriate 5XX code to respond with.
- 501 Not Implemented: request method is not supported and cannot be handled.
- 502 Bad Gateway: server (working as gateway) got an invalid response.
- 503 Service Unavailable: server is not ready to handle request (e.g. down for maintenance, overloaded). A user-friendly explanation page should be sent.
- 508 Loop Detected: server detected an infinite loop while processing request.

# Network devices

## Load balancers

## Proxies

### Forward Proxy

### Reverse Proxy

## Firewalls
