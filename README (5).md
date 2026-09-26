<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](https://nextwork.ai/projects/da091986-ef01-5973-a070-b15e174f59d8)

**Author:** agustinnico2302@gmail.com  
**Email:** agustinnico2302@gmail.com

---

![Image](https://nextwork.ai/content_gray_heroic_hyena/uploads/da091986-ef01-5973-a070-b15e174f59d8_8ee57662)

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC provides an isolated network in AWS where you can deploy and manage cloud resources. You can customize it by setting security rules, controlling how traffic flows, and organizing resources into subnets that can grow with your needs.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to test the connectivity between my instance to validate if they can communicate successfully and to know if the network ACLs and Security Group configurations are correct.

### One thing I didn't expect in this project was...

One thing I didn't expect from this project was that it demonstrated that security groups are stateful. Initially, I was confused about why there was no need to allow outbound traffic in the private security group of my private instance for ICMP replies. But I realized that security groups are stateful, which means they allow traffic that is part of an existing connection.

### This project took me...

This project took me for almost 2hrs, because I'd reverse engineered my network ACL and subnet configuration since I love to play things around to better understand how these virtual firewalls works in AWS virtual network.

## Connecting to an EC2 Instance

Connectivity is all about how good different parts of the network communicate with each other and as well with the external networks. A good connectivity defines how data flow smoothly across the network, starting from powering up a simple static web hosting to complex connectivity like Netflix that uses 100,000 EC2 instance to power up their operations.

My first connectivity test was whether I could connect to the public EC2 instance and test its connectivity with the private instance.

![Image](https://nextwork.ai/content_gray_heroic_hyena/uploads/da091986-ef01-5973-a070-b15e174f59d8_88727bef)

## EC2 Instance Connect

EC2 instance Connect is a way to connect to an EC2 instance using the AWS management console. It is an convenient way to initiate connection with an instance since AWS handles the key pairs for you because traditionally, the user will be managing this key to connect to their instance using the generic SSH connection via their terminal.

My first attempt at getting direct access to my public server resulted in an error, because the security group of the instance wasn't configured to allow SSH connections, instead it only allow all the http traffic which is not the protocol used to initiate SSH connection.

I fixed this error by adding a rule in security group to allow all the IPv4 inbound connections via SSH protocol.

![Image](https://nextwork.ai/content_gray_heroic_hyena/uploads/da091986-ef01-5973-a070-b15e174f59d8_1cbb1b88)

## Connectivity Between Servers

Ping is used to test the connectivity between networking and end devices to ensure that two devices can communicate successfully. I used it to test the connectivity between my public and private EC2 instance to validate if they can communicate successfully using the ICMP protocol.

The ping command I ran was 'ping 10.0.0.238'. The IP address specified is the private address of the private EC2 instance.

The first ping returned nothing which means that there is a connectivity issue between the instance.

![Image](https://nextwork.ai/content_gray_heroic_hyena/uploads/da091986-ef01-5973-a070-b15e174f59d8_defghijk)

## Troubleshooting Connectivity

I troubleshooted this by allowing all IPv4 ICMP traffic on the Private Network ACL for both inbound and outbound rule and allowing the same traffic at the Private Security Group but for inbound only since security groups are stateless, there is no need to configure the outbound traffic for ICMP replies.

![Image](https://nextwork.ai/content_gray_heroic_hyena/uploads/da091986-ef01-5973-a070-b15e174f59d8_4a9e8014)

## Connectivity to the Internet

Curl comman is used to send request to an URL, often for fetching a webpage or data from the server.

I used curl to test the connectivity between my public EC2 instance and the public internet to test if the instance can communicate with the public internet.

### Ping vs Curl

Ping and curl are different because ping is used to check the connectivity between two (2) machines which in my case the connection between my two instances. On the otherhand, curl is used for fetching data or webpage from the internet.

## Connectivity to the Internet

I ran the curl command 'curl example.com' which returned the landing page of the domain. I also test it with other websites like facebook which returns a ton of data such as its HTML, CSS, and Javascript codes.

![Image](https://nextwork.ai/content_gray_heroic_hyena/uploads/da091986-ef01-5973-a070-b15e174f59d8_8ee57662)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/da091986-ef01-5973-a070-b15e174f59d8)*
