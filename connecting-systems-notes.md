---
theme: thg-accelerator
---

# Network devices

## Load balancers

## Proxies

### Forward Proxy

### Reverse Proxy

## Firewalls

# Request/Response

Request-response model, used in network protocols and systems where clients and servers interact to exchange information. (used in APIs, network communications, SSH etc.)

### Client-Server Model

Model describes communication between two computing entities over a network in a request/response method

Client Role: initiates requests for services

- Only has to understand the response based on the relevant applicaiton protocol (how to parse/format the data for the request)

Server Role: provides a function or service, sharing of resources

#### Architecture

1. One-Tier: A single program running on a single computer without requiring network access.

2. Two-Tier: Consists of client, server and protocol that links the two.

   GUI code (C++, Java etc) resides on client host; domain logic resides on server hist

3. Three-Tier: Presentation tier–UI layer, Application tier–service layer performing processing, Data tier–database server that stores information.

4. N-Tier: Divides into logical layers and physical tiers.

   Logical: separate responsibilities, manage dependencies. Physical: runs on separate machines, improve scalability, add latency from additional network communication

   Can be closed-layer (layer can only communicate with next layer down), or open-layer (layer can communivate with any layers below).

## Client-side View

1. Initiates communication by sending HTTP request to a URL or server endpoint

   Requests would include HTTP methods: GET, POST, PUT, DELETE (HEAD, CONNECT OPTIONS, TRACE PATCH etc)

2. After recieving a response, the client then parses and processes the information to display the results or to perform further actions.

### Request structure

    Request Line: HTTP Methods

    Request Headers: metadata providing additional info in how to handle content (i.e. the request)

    - empty line indicating end of header

    (optional) Request Body: data sent by client

## Server-side View

1. Server parses requests from clients by extracting request method, determining start/end of request.

2. Then server performs the required action such as retrieving data from database, processing the data, or generating a response.

3. The server then compiles a result to send back to the client.

### Response structure

    Status Codes: Indicates request outcome

    Response Headers: metadata indicating how to handle response body/resulting data

    Response Body: returned data

# HTTP1.1

# Virtual Private Cloud (VPC)
