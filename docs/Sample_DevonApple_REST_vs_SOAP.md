# REST and SOAP APIs: Which is Better for Your Service?

When you want to create a web service, your best options are [REST](https://restfulapi.net/) (REpresentational State Transfer) and [SOAP](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/webservices/soap-web-services) (Simple Object Access Protocol). Both application programming interfaces (APIs) allow developers to build software that reliably communicates between applications and servers. SOAP and REST approach the task in different ways, so it pays to know how each can work for you.

- [Why do you need REST or SOAP?](#why-do-you-need-rest-or-soap)   
- [REST and SOAP APIs](#rest-and-soap-apis)   
- [REST details](#rest-details)   
- [SOAP details](#soap-details)   
- [Selecting an API service](#selecting-an-api-service)   

## Why do you need REST or SOAP?

SOAP and REST are API services that help you to connect two pieces of software, usually a client application and a server. These web services define how the sender and receiver exchange information over a network. The right API makes it easy for you to connect networked services within an organization. A good API also makes it easier to partner with third-party web services, without exposing the internal details of your program. Developers for partner services can use your APIs to interface with your product and build mutual value.

## REST and SOAP APIs

REST and SOAP APIs handle web services in fundamentally different ways. They share some basic similarities, and REST APIs can interact with SOAP APIs, but you can't use them interchangeably.

SOAP is a protocol, a function-driven set of operation standards for connecting web services. SOAP exclusively uses Extensible Markup Language (XML) for data exchange. The strength of a SOAP API is its structure and security. That same structure can cause challenges when scaling, and relies on rigidly defined operations to connect web services. You need significant end-to-end control over the systems you want to join, which requires infrastructure and detailed contracts about how the two points communicate. Some call it an “envelope”: a secure, structured package that requires resources to seal, transmit, and open.

REST is a data architecture, an object-oriented method for exchanging information. REST APIs use Uniform Resource Identifiers (URIs) and HTML to connect web services. A RESTful API is light, fast, and easy to process. REST uses XML, as well as smaller message types like JSON or YAML. APIs built using REST principles are flexible, accessible, and need little infrastructure to connect with other APIs. REST standards have a smaller learning curve, and the design is similar to other web technologies. If SOAP is an envelope, REST is a “postcard”, a smaller package that is less secure but much easier to produce and send.

## REST details

> In 2000, computer scientist Roy Fielding proposed the REST API standard to support quick and reliable communication between diverse servers across an expanding web.

**APIs for a diverse internet:** The REST method corrects for different levels of trust, unpredictable data traffic, and the growing variety of web services. RESTful APIs use light communication, small data payloads, and have lower overhead requirements for client applications.

**A leaner API:** REST APIs were adopted by the internet community as a quicker, lightweight alternative to the SOAP protocols. REST APIs are quicker to produce, use less bandwidth to transmit data, and easily bring together diverse servers and clients. The stateless nature of REST APIs means that requests are self-contained and pass all of the information needed for the desired operation. REST APIs can use XML, as well as a variety of leaner formats, such as comma-separated values (CSV) and JavaScript Object Notation (JSON). You can also set up REST API calls to be cached if needed.

**HTTP only:** REST APIs require direct point-to-point communication. REST APIs can only use the HTTP and HTTPS transport protocols. This isn't a significant limitation because HTTP and HTTPS are popular and can operate through firewalls. REST is lean, in principle, but REST APIs have the capacity to become bloated or complicated depending on use.

## SOAP details

> MicroSoft invented the SOAP API structure in 1998 by to replace the binary messaging protocols of the time. The Distributed Component Object Model (DCOM) and Common Object Request Broker Architecture (CORBA) didn't work well over the internet.

**XML only:** SOAP applications use structured XML packages to transmit operations between multiple languages, platforms, and transport protocols, including SMTP and HTTP.

**Comprehensive standards:** SOAP's complex and detailed rules ensure security and reliability. There are a host of Web Service (WS) standards that you can add, and these standards cover every aspect of a given operation. SOAP's built-in error handling is standardized and detailed enough that developers can reliably program automated responses to errors in a SOAP request. SOAP's extra WS protocols can provide end-to-end security for data transmissions across protocols.

**Steep learning curve:** It is a challenge to code for SOAP's comprehensive set of rules. Every operation needs a full set of XML specifications, which is a challenge to automate and uses a lot of bandwidth. SOAP is also error-intolerant. SOAP products typically need a third-party library to translate between the server and the client. The most comprehensive third-party tool is the Web Services Description Language (WSDL). Updating your SOAP application through WSDL typically requires you to push out library changes to all client systems, which can be labor-intensive, and discourages updates.

## Selecting an API service

Choose REST APIs for light HTTP communications, small data payloads, and lower overhead requirements for client applications.

Choose SOAP APIs for enterprise solutions, when you have firm control over every participating system in the network environment, security is a priority, and bandwidth isn't a factor.
