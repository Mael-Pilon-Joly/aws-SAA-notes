# ALB VS NLB

Application Load Balancer (ALB)
Layer: Operates at the Application Layer (Layer 7) of the OSI model.
Traffic Type: Best for HTTP and HTTPS traffic. ALB can inspect and route traffic based on content, such as URL paths, host headers, or query parameters.
Features:
Content-Based Routing: Route traffic based on URL, hostname, or HTTP headers.
WebSocket Support: Provides support for WebSockets and HTTP/2.
Advanced Features: Includes features like SSL termination, sticky sessions, and Web Application Firewall (WAF) integration.
Request and Response Handling: Capable of inspecting and modifying requests and responses.
Use Cases: Ideal for applications requiring advanced routing, SSL termination, or content-based routing (e.g., microservices, containerized applications, HTTP-based APIs).
Network Load Balancer (NLB)
Layer: Operates at the Network Layer (Layer 4) of the OSI model.
Traffic Type: Best for TCP, TLS (TCP over SSL), and UDP traffic. It provides high performance for network-based traffic.
Features:
High Performance: Handles millions of requests per second with very low latency.
Static IP Addresses: Supports static IP addresses for the load balancer and can integrate with Elastic IP addresses.
Connection-Based Routing: Routes traffic based on IP protocol data and TCP/UDP ports.
TLS Termination: Can offload TLS decryption from your servers.
Use Cases: Ideal for applications that require high performance and low latency for TCP/UDP traffic, such as gaming servers, real-time communication, or legacy applications that don’t require advanced HTTP features.