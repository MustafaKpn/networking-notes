### Client side request/response
The basis of web interactions, is asking for information, and recieving information. The "asker" is the a **client**, and the respondent is the **server**. Clients send Requests to Servers asking for some kind of information. Upon receiving a Request, Servers send Responses back to the Client.
This pattern of communication is described by the request-response model:
1. #### Client sends a request
* The client (usually a web browser or an application) initiates the communication by sending an HTTP request to a specific URL or endpoint on the server.
* The request includes the HTTP method (such as GET, POST, PUT, DELETE) that indicates the desired action to be performed on the server, along with additional headers and sometimes a message body containing data.

2. #### Server parses the request
* The browser first takes the URL enetered and parses it to understand its componenets:
     As an example: http://google.com/path/to/resource/?query=param
    * protocol (http:// or https://)
    * domain name (i.e. google.com)
    * path (i.e. /path/to/resource/)
    * query parameters (?query=param)

3. #### DNS resolution

The browser needs to find the IP address that corresponds to the domain name. It sends a request to the Domain Name System (DNS) server to resolve the domain name into an IP address.
Then, the DNS responds to the request with the IP address of the server hosting the requested URL. DNS is often called the 'phonebook of the internet'.

4. #### Establishing connection
* Once the browser receives the IP address, it tries to establish connection with the hosting server. For https, this involves an additional step to create a secure connection via SSL/TCP.
    * Transmission Control Protocol (TCP) is a connection-oriented protocol for communications that helps in the exchange of messages between different devices over a network.
    * SSL is standard technology for securing an internet connection by encrypting data sent between a website and a browser. SSL uses certificates that contain a public key that authenticates the website’s identity and allows for encrypted data transfer through asymmetric, or public-key cryptography.

5. #### Server processing

The server receives the request, processes it (which may involve accessing a database or performing other backend operations), and prepares an HTTP response.

6. #### Receiving the response

The browser receives the response from the server. This includes:
* Status line includes the status code (i.e. 404) and a phrase line (i.e. Not Found).
* Headers (information about the response).
* Body that contains the actual data.

7. #### Rendering the page

After receiving the response, the browser renders the HTML content:
    * HTML parsing: the browser parses the HTML to build the Document Object Model (DOM) tree, which represents the structure of the webpage.
    * CSS and JavaScript parsing (if applicable).
    * Layout and Painting: Finally, the browser calculates the layout of the page (where elements are positioned) and paints them to the screen.


