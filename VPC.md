# DNS

In AWS VPCs, DNS resolution and DNS hostname are related to how domain names are resolved into IP addresses and how instances within a VPC communicate using domain names. Here’s a breakdown of each concept:

DNS Resolution
DNS resolution refers to the process of translating domain names into IP addresses. In the context of a VPC, DNS resolution determines how instances within the VPC resolve domain names (e.g., example.com) into IP addresses so they can communicate over the network.

Key Points:

Internal DNS Resolution: AWS provides internal DNS resolution within a VPC. Instances can use DNS to resolve other instances’ private IP addresses within the same VPC. For example, if you have an EC2 instance with a private DNS name, other instances within the same VPC can use this private DNS name to resolve to the instance’s private IP address.
External DNS Resolution: For external domain names (those outside the VPC), AWS uses Route 53 or other public DNS services to resolve these names to their corresponding IP addresses.
Configuration:

You can enable or disable DNS resolution in a VPC by setting the enableDnsSupport option in the VPC settings.
The DNS resolver’s IP address is provided by AWS and is typically found at 169.254.169.253.
DNS Hostname
DNS hostname refers to the domain names assigned to instances within a VPC. These hostnames are used to identify and access instances in a human-readable format.

Key Points:

Private DNS Hostnames: For instances in a VPC, AWS can assign private DNS hostnames. These are internal to the VPC and resolve to the instance’s private IP address. This allows instances to communicate with each other using domain names rather than IP addresses.
Public DNS Hostnames: If you want an instance to be accessible from the internet, AWS can also assign a public DNS hostname (provided that the instance has a public IP or an Elastic IP address associated with it).
Configuration:

You can enable or disable DNS hostnames in a VPC by setting the enableDnsHostnames option in the VPC settings.
For an instance to have a public DNS hostname, the VPC must have DNS resolution enabled and the instance must have a public IP or an Elastic IP.
Examples:

Internal DNS Hostname: If you have an EC2 instance with a private IP, its internal DNS hostname might look like ip-10-0-1-23.ec2.internal.
Public DNS Hostname: If the instance has a public IP, its public DNS hostname might look like ec2-203-0-113-25.compute-1.amazonaws.com.
Summary
DNS Resolution in a VPC handles translating domain names to IP addresses, allowing instances to find and communicate with each other or with external resources.
DNS Hostname is the domain name assigned to instances, which can be used to access them either privately within the VPC or publicly if the instance is exposed to the internet.

# Traffic Mirroring

What is Traffic Mirroring?
PDF
Traffic Mirroring is an Amazon VPC feature that you can use to copy network traffic from an elastic network interface of type interface. You can then send the traffic to out-of-band security and monitoring appliances for:

# Network firewall

You can filter network traffic at the perimeter of your VPC using AWS Network Firewall.