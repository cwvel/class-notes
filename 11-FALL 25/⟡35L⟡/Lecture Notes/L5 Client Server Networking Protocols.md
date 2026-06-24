# Networking Protocols
### Client-server architecture
- **Client** requests services/resources from the **server**
- **Network** connects client and server
- Pros:
	- Centralized control of data and resources
	- Easy to maintain and scale
	- Security
- Cons:
	- Server is single point of failure
	- Requires network connectivity
- Used in web browsing, databases, emails, online games
### Peer-to-peer architecture
- Decentralized: Clients (peers) directly interact with each other
- Peers act as suppliers (server) and consumers (client) of resources
	- Peers need to identify each other, so IP addresses are exposed to others in the system
	- Can raise security concerns
- Most architectures are a hybrid of client-server and P2P
	- E.g. Zoom uses client-server mainly but P2P for 1 on 1 calls
### Protocols: TCP/IP Stack
- **TCP/IP Stack**
	- Application layer (API) provides an interface for applications to interact with the network
	- Transport layer provides end-to-end communication between apps
	- Internet layer: addressing and routing data packets
	- Link layer
- Messages have **headers** and **payloads**
	- Package wrapping: Higher-level protocols use the protocols directly below to send messages
- **URL:** uniform resource locater
	- Web address of a resource on the internet
	- `{protocol}://{domain}(:{port})?(/{resource})`
		- Domain = address, port = apartment number

**Application layer: HTTP/HTTPS**
- Stateless protocol: each request is independent, server does not remember previous requests from the client
- **HTTPS** (secure) uses encryption for more secure data transfer
- Common **status codes**
	- `2xx` = successful
		- `200` = request successful
		- `201` = created successfully
	- `4xx` = client error responses
		- `400` = bad request
		- `404` = not found
	- `5xx` = server error responses
		- `500` = internal server error
		- `502` = bad gateway, incorrect routing
- Requests
	- **GET** retrieves data from server
	- **POST** sends data to server
	- **PUT** update existing resource
	- **DELETE** remove a resource
- How it works:
	- Client (browser) sends HTTP request
	- Server receives and processes request
	- Server sends HTTP response: HTTP status code + HTML content
	- Client displays web page
- An HTTP server listens on a host and port

**Transport layer: TCP/UDP**
- **TCP (Transmission Control Protocol)**
	- 3-way handshake before data transfer
		- SYN - client sends connection request
		- SYN-ACK - server acknowledges and agrees to connect
		- ACK - client confirms and establishes connection
	- Packet loss (if it occurs) is detected and then the message is retransmitted - good for file transfer
- **UDP (User Datagram Protocol)**
	- Unreliable but lower overhead - faster
	- Used for video streaming/real time gaming

**Internet Layer**
- IPv4
	- `192.168.1.1`
- IPv6 (new standard)
	- 8 blocks of hexadecimal numbers separated by `.`
- Identifies particular sender/receiver using "addresses", similarly to USPS

**Throughput vs. latency**
- **Throughput**: Amount of data transmitted per unit time (bits per second)
	- e.g. pipe width
- **Latency**: Time taken for data to travel from source to destination (milliseconds)
	- e.g. pipe length



