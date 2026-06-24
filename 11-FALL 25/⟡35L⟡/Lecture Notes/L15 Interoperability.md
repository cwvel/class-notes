## Interoperability
**Interoperability**: The degree to which two or more systems/components can exchange meaningful information
- Lets you use **services**
	- Instead of implementing functionality yourself, you can use existing service providers
- Improve **usability**
	- Users can transfer data between systems
- Cross-platform solutions
	- Simplifies communication between separately developed systems
The **Global Distribution System (GDS)** lets almost all airlines and booking systemes interoperate

### Design Principle
#### Create shared interfaces/data formats
1. List all data that needs to be exchanged
2. Define an interface/data format that supports all data
3. Implement serialization & deserialization

- Build **abstractions**
	- The interface should not expose implementation details
- Ensure language and platform **independence**
	- The format should be supported by all programming languages, operating systems, devices

#### REST APIs
- A common technique to implement shared interfaces
- **Representational state transfer (REST)** is a stateless protocol to exchange data in client-server systems via HTTP/HTTPS:
	- **POST** creates a resource
	- **GET** reads a resource
	- **PUT** updates a resource
	- **DELETE** deletes a resource
- Naming convention for URLs, based on resource identifiers
- Resources often described via XML, YAML, JSON, HTML

##### Example REST API: GDS
Request: `POST /getFlights`
```json
...
"travelPreferences": { 
	"flightType": "Direct", 
	"maximumStopsQuantity": 1 
}, 
"itineraryParts": [ { 
	"departureAirportCode": "LAX", 
	"arrivalAirportCode": "PIT", 
... ]}
...
```

#### Alternatives to REST
- RPC (remote procedure call)
	- *Calling a function on a remote server as if it were local. Can be stateful. Functions and actions beyond CRUD. Good for complex calculations. Can use multiple document formats.*
- SOAP (simple object access protocol)
	- *Can be stateful. More complex. Sometimes slower. Has more security features. Has built-in error handling. Good for distributed enterprise environments. Uses XML.*
- GraphQL
	- *Server-side schema defines types, enabling checking of data structure conformance. Good for large, complex, and interrelated data sources. Uses JSON.*

#### Compatibility test: XML/JSON/YAML Schema
- Schema describes the structure of document
	- Lists attributes and possible values, complex types
- Validation of a document against the schema can be done automatically to test compatibility at runtime
##### Example JSON schema
```json
"properties": { 
	"departureAirportCode": { 
		"type": "string", // constraints on property type
		"pattern": "^[A-Z]{3}$"
	}, 
	"price": { 
		"type": "number", 
		"minimum": 0, // constraint property value
		"exclusiveMinimum": true 
	} 
}, 
// constraints on document structure
"required": ["departureAirportCode", "price"]
```

### Semantic interoperability
- Document interfaces and their semantics: units? price including tax? date format? coordinate system reference frame?
- Agree on vocabulary
- Integration tests

#### Interface descriptions
**Syntactic view** $\rightarrow$ describes document format, actions, parameters, outputs
**Semantic view** $\rightarrow$ describes purpose/meaning of resource/action
- side-effects, usage restrictions, error handling, example input/outputs

#### Example: GDS syntactic/semantic views
##### Syntactic view
`POST /createBooking {`
- flightNumber: str
- date: dateTime
- seat: str
- paymentReference: PaymentMethod
- travelerName: str
`}`

##### Semantic view
- Purpose: airline confirms requested booking
- Side-effects: money is charged, seat marked as sold, can be canceled within 1 hr
- Usage restrictions: Authorized booking systems
- Errors: invalid format, unauthorized, too many requests, etc.

### Interoperability often conflicts with changeability
- Shared interfaces and data format mean changes have to be implemented in all cooperating systems
	- Extensions/changes require a new version of the interface, which breaks interoperability
- Often in conflict:
	- **Effort to implement** interface in systems
		- More complex interface has a higher implementantion cost
	- **Variability** allowed
		- An interface that supports more use cases and potential extensions is more likely to be adopted

#### Design pattern: Adapters
- An adapter component translates between two systems that use different interfaces
	- ex. XML to JSON