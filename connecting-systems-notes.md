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


#### OSI model
NOTE: I am trying to understand the OSI model through some youtube videos and I am keeping notes here.

**Layer1-Physical**

* Devices that only operate on this layer can only transmit data in binary using a physical meduim such as: copper, light, waves.
* Layer 1 does not provide access control and does not offer uniquely identified devices.
* If two devices are communicating on a layer 1 level only, collisions or noise would be transmitted too since there is no added layer of control yet.
* Layer 1 transmits raw data

**Layer2-Data Link**

* It is built on layer 1 with the addition of extra functionality.
* Layer 2 introduces the concept of frames. Frames are a format for sending information over the layer 2 network.
* Layer 2 also introduces mac address for every connected devices. Example of a mac address: 23:22:fb:b9:5b:75
    * MAC addresses are uniquely attached to hardwares (not software). This is assigned by the manufacturer.
    * The mac address on a network card should be globally unique
* Ethernet is a L2 protocol used generally for local networks.
* Frames used by layer 2 consist of:
    1. Preamble and start frame delimiter. This is to allow devices to know the start of a frame.
    2. The destination and the source MAC addresses. 
    3. Ether type: to specify which layer 3 protocol is putting its data inside the frame.
    4. The previous elements are called the MAC Header
    5. The MAC Header is followed by the payload where data is encapsulated.
    6. Finally is the Frame Check Sequence to identify an errors

If two devices are connected and want to transmit data on a layer 1 level only, this will cause collision because both devices might be sending data at the same time. This is solved using the 2nd layer which provides a controlled access to the media devices.

Let's say we have device A and device B that are connected with a physical meduim. A wants to send data to B. Using layer 2 functionality, it creates a frame first. Then it checks if there is a carrier in the physical meduim. If there is a signal coming, it waits unitl it passes. If there is not, layer 1 takes the frame data, converts it to physical standard and transmits it to device B. B receives the passed frame and checks the MAC address of the destination found in the MAC header in the frame. If the MAC address corresponds to device B, the frame is taken in.

**Layer3-Network**
* Let's say we have LAN1 and LAN2. Both are isolated local area networks. Using only layer2, only those networks joined by a direct point to point link using the same layer2 protocol could communicate. Here comes layer3 to connnect devices accross local area networks.
* IP Packets are moved step by step from source to destination via intermediate networks, encapsulated in different frames along the way.
* Routers move packets of data across different networks. They encapsulate a packet inside an Ethernet frame for each local journey for that particular network. Then when it needs to be moved to another network, the old frame is removed and a new one is added around the same packet and is moved to the next local network.
* So if a video is being sent from a company in the US to my computer, the video would need to be moved between different local networks until it gets here. For each network it moves to, it needs to be encapsulated in a particular frame that corresponds to that network. When it is moved, the old frame is removed a new one is assigned.
* IP is needed to allow us to connect to different remote networks crossing intermediate networks.
* IP packets have source and destination addresses, but unlike frames, these addresses are not local.
* IP packets can have different versions such as v4 and v6.
* Packets contain many data types. One of the is Protocol field. This is defined by layer 4, and it stores the protocol being used such as TCP and UDP. For TCP, the protocol's field value would be 6. Whereas for UDP the value is 17.
* Another data field, is Time To Live (for v4) or Hop Limit (for v6). This data field defines a limit for how many different points or hops the packets are moved between. This is to avoid looping. When the packets reach their maximumn Time To Live number without arriving to their detination, they get discarded.
* IP addresses have have the format: nnn.nnn.nnn.nnn where nnn is a number in the range from 0 to 255. The first two parts of an IP address represent the network part. The last two part represent the host on that network.
* If the 'Network' part of two IP addresses match, it means they are on the same IP network. If not, they are on different networks.

 
