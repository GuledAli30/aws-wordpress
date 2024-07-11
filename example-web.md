# What Happens When You Type in www.example.com into the URL?

This research project explores the step-by-step process that occurs when a user types "www.example.com" into their web browser's address bar. Below is a concise outline of the sequence of events:

1. **URL Parsing**: The browser parses the URL to identify the protocol (HTTP/HTTPS), domain (example.com), and other components like the path or query string.

2. **DNS Resolution**: The browser initiates a DNS (Domain Name System) query to resolve the domain name "example.com" into its corresponding IP address. This step involves:
   - Checking the browser cache for a cached IP address.
   - If not found, querying the operating system cache.
   - If still unresolved, the OS queries the DNS resolver (typically provided by the ISP).
   - The DNS resolver performs a recursive search, querying root servers, TLD (Top Level Domain) servers, and authoritative servers until the IP address is found.

3. **TCP Connection**: With the IP address obtained, the browser initiates a TCP (Transmission Control Protocol) connection to the server using a three-way handshake process (SYN, SYN-ACK, ACK).

4. **HTTPS Handshake** (if applicable): If the URL uses HTTPS, the browser performs an SSL/TLS handshake to establish a secure connection.

5. **HTTP Request**: The browser sends an HTTP request to the server, requesting the web page (e.g., GET /index.html).

6. **Server Processing**: The web server processes the request, retrieves the necessary resources, and prepares the response.

7. **Data Transmission**: The server sends the HTTP response back to the browser, which includes the requested web page and any associated resources (CSS, JavaScript, images).

8. **Rendering**: The browser receives the response, parses the HTML, and renders the web page for the user to view.

### Key Points:
- **DNS Resolution**: Takes effect after URL parsing and before the TCP connection.
- **Data Transmission**: Occurs after the HTTP request is made and the server processes the request.

This project provides a detailed examination of each step to understand the underlying mechanisms and technologies involved in accessing a web page.
