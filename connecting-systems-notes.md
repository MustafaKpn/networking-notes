### Client side request/response
The basis of web interactions, is asking for information, and recieving information. The "asker" is the a **client**, and the respondent is the **server**. Clients send Requests to Servers asking for some kind of information. Upon receiving a Request, Servers send Responses back to the Client.
This pattern of communication is described by the request-response model:
1. Client sends a request
* The client (usually a web browser or an application) initiates the communication by sending an HTTP request to a specific URL or endpoint on the server.
* The request includes the HTTP method (such as GET, POST, PUT, DELETE) that indicates the desired action to be performed on the server, along with additional headers and sometimes a message body containing data.

2. Server parses the request
* The browser first takes the URL enetered and parses it to understand its componenets:
    As an example: http://google.com/path/to/resource/?query=param
    * protocol (http:// or https://)
    * domain name (i.e. google.com)
    * path (i.e. /path/to/resource/)
    * query parameters (?query=param)
