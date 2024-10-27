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
* IP addresses are 32 bits. Each byte is called Octet. 
* A Subnet Mask allows a Host to determine if an IP adress it needs to communicate with is local or remote. Which determines if it needs to use a gateway or can communicate locally.
* When communicating through a network to a remote destination, the router compares packat destination IP and route table for matching detinations. Then packet is forwarded on to the next hop or target.
* In an IP address, specific prefixes are preferred: 
    * If we have the IP address: 52.215.13.0/24, the prefix 24 indicates that the first 24 bits of the IP address is a network address, and the rest are the host's. The most specific IP address would have the prefix 32 and the least specific is 0 where it represents a default route (for example, the one found on the router that directs traffic to the Internet Service Provider).


#### Other Notes
##### Ports
Ports are numeric identifiers that direct network traffic to different services on a device. Each device has many services running on it, and ports distinguish between them. Ports help ensure that data sent to a device (identified by its IP address) reaches the correct application or service on that device.
For example:
* Port 80 handles HTTP web traffic.
* Port 433 handles HTTPs (secure web).
 
##### Sockets
A socket is an endpoint for communication between two devices or processes over a network. It’s created by pairing an IP address with a port number. Example: A socket could look like 192.168.1.5:80, where 192.168.1.5 is the IP address and 80 is the port.
A socket allows devices to exchange data across the network, ensuring that the right data reaches the correct application at both ends of the connection.



#### Internet Security

When connecting to a website using HTTP protocol, anyone who intercepts that communication would be able to know the data being sent as it is not encrypted. HTTPs protocol offers this encryption using Transport Layer Security (TLS).
Securing a connection between a client and a server using TCP comprises 4 steps:
1. TCP handshake

Just like the case of HTTP, the browser establishes a TCP connection with the server. As discussed in the lecture, this handshake process is being optimised in TLS 1.3 to reduce the number of networks rounds form 2 to 1.

2. Certificate Check

After the browser establishes a TCP connection with the server, the TLS handshake begins. The browser sends a 'client hello' to the server. In this 'hello' message, the browser tells the server two things: 1. What TLS version it can support. 2. What cipher suite (set of encryption algorithms) it can support.
The server then sends back a 'server hello' message to the client including the TLS and the cipher suite it will use.
The server sends a SSL certificate that includes a lot of data.

3. Key Exchange 
One important thing that is included in the certificate's data is a public key that is used by the client in asymmetric encryption. In asymmetric encryption, data encrypted using the public key on the client side, can only be decrypted using the private key on the server side.
This is how the client send an encryption key safely to the server after encrypting it using the public key.
The server encrypts the session key using the server's public key and sends it to the server. Then the server decrypts the session key using the private key.

4. Data Transmisson
Using the session key and the cipher suite both the server and the client agreed on. Data is encrypted and transmitted between the server and the client.

NOTE: Asymmetric encryption is computationally intensive. That's why symmetric encryption is used.

#### mTLS
Mutual Transport Layer Security (mTLS), also known as Two-Way TLS, is an extension of the Transport Layer Security (TLS) protocol. Mutual authentication, is a fundemental part of mTLS, involves both the client and the server presenting certificates to each other to establish trust and verify their identities. 

How does it work?

As discussed earlier, the client needs to verify the certificate that includes a public key sent by the server to ensure its validity. Using mTLS, the client needs to present a valid certificate to the server too. The client's certificate also includes a public key that will be used to establish a secure communication.
In contrast, TLS (and its predecessor SSL) only provides authentication of the server to the client, which is sufficient for many use cases where the client trusts the server and wants to verify the identity of the server before sending sensitive data.

##### TLS versus mTLS

While TLS and mTLS provide encrypted communication, the primary difference lies in the authentication process. In TLS, only the server’s identity is authenticated by the client, whereas in mTLS, both client and server identities are authenticated mutually. mTLS offers a higher level of security than standard TLS because it requires both client and server to authenticate each other.

Both TLS and mTLS are helpful in different scenarios. For instance, TLS is commonly used in basic web browsing, where the user only needs to confirm the server’s identity. On the other hand, mTLS comes in handy when both parties need to validate each other’s identities – this is especially important in business-to-business (B2B) data transmissions, connecting cloud services, and high-security applications.


DIAGRAM: https://excalidraw.com/#json=iN3YKHFS8oSFGIbtolKSd,qqosPtksCtONVzzFLXbmfw
