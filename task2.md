# Networking Assignment 2

## 1. Basic commands and protocols

### ipconfig

`ipconfig` shows the network settings of a Windows computer, such as its IP address, subnet mask, default gateway, and DNS server.


### nslookup

`nslookup` checks DNS. It finds the IP address belonging to a domain name.

```text
nslookup www.google.com
```

This asks the DNS server for the IP address of Google.


### ping

`ping` checks whether another computer or server can be reached. It also shows the response time.

```text
ping www.google.com
```

It sends a small request and waits for a reply. A blocked firewall can cause ping to fail even when the website works.


### traceroute

`traceroute` shows the routers, or hops, used to reach a destination. On Windows the command is called `tracert`.

```text
tracert www.google.com
```

This is useful for finding where a connection is slow or stops.


### TCP and UDP

TCP and UDP are transport protocols. They use port numbers to send data to the correct application.

| TCP | UDP |
| --- | --- |
| Creates a connection first | Does not create a connection first |
| Checks delivery and order | Does not guarantee delivery or order |
| Used by HTTPS, SSH, and email | Used by DNS, video calls, and streaming |
| More reliable but slower | Faster with less overhead |


## 2. What happens after entering `https://www.something.com`?

### Data flow

1. **The browser reads the URL.** It understands that `https` means a secure web connection, the website name is `www.something.com`, and the default port is `443`.

2. **DNS finds the server.** The computer checks its DNS cache. If the address is not there, it asks a DNS server. DNS changes the website name into an IP address.

3. **The packet leaves the computer.** The computer checks its routing table. Since the server is usually outside the local network, the packet goes to the default gateway, normally a home or office router.

4. **Routers forward the packet.** The packet passes through several routers until it reaches the web server. A home router may also change the private IP address to a public IP address using NAT.

5. **TCP creates a connection.** The computer connects to the server on port 443. TCP uses a three-way handshake: `SYN`, `SYN-ACK`, and `ACK`. TCP makes sure data arrives in the correct order.

6. **TLS makes the connection secure.** The server sends a security certificate. The browser checks that it belongs to the website and is trusted. Both sides then create encryption keys.

7. **The browser sends an HTTP request.** The request is encrypted and asks the server for the home page, for example:

   ```http
   GET / HTTP/1.1
   Host: www.something.com
   ```

8. **The server processes the request.** It finds or creates the requested page and sends back a response. The response normally contains HTML and may also refer to CSS, JavaScript, images, and fonts.

9. **The browser displays the page.** The computer receives and decrypts the response. The browser reads the HTML, downloads the other files, builds the page layout, and displays it on the screen.
