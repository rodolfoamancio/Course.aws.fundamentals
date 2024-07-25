# Reading 2.5: Networking on AWS

## What is Networking?

Networking is how you connect computers around the world and allow them to communicate with one another. In this trail, you’ve already seen a few examples of networking. One is the AWS global infrastructure. AWS has created a network of resources using data centers, Availability Zones, and Regions.

## Know the Networking Basics

Think about sending a letter. When sending a letter, there are three pieces of information you need:

- The payload or letter inside the envelope.
- The address of the sender in the From section.
- The address of the recipient in the To section.

Let’s go further. Each address must contain information such as:

- Name of sender and recipient
- Street
- City
- State or province
- Zip, area, or postal code
- Country

You need all parts of an address to ensure that your letter gets to its destination. Without the correct address, postal workers are not able to properly deliver the message. In the digital world, computers handle the delivery of messages in a similar way. This is called routing.

## What are IP Addresses?

In order to properly route your messages to a location, you need an address. Just like each home has a mail address, each computer has an IP address. However, instead of using the combination of street, city, state, zip code, and country, the IP address uses a combination of bits, 0s and 1s. 

Here is an example of a 32-bit address in binary format:

`10101100 00010000 00100001 00011100`

It’s called 32-bit because you have 32 digits. Feel free to count!

## What is IPv4 Notation?

Typically, you don’t see an IP address in this binary format. Instead, it’s converted into decimal format and noted as an IPv4 address. 

In the diagram below, the 32 bits are grouped into groups of 8 bits, also called octets. Each of these groups is converted into decimal format separated by a period. 

![alt text](image.png)


In the end, this is what is called an IPv4 address. This is important to know when trying to communicate to a single computer. But remember, you’re working with a network. This is where CIDR Notation comes in.

## Use CIDR Notation

`192.168.1.30` is a single IP address. If you wanted to express IP addresses between the range of `192.168.1.0` and `192.168.1.255`, how can you do that? 

One way is by using Classless Inter-Domain Routing (CIDR) notation. CIDR notation is a compressed way of specifying a range of IP addresses. Specifying a range determines how many IP addresses are available to you. 

CIDR notation looks like this: 

![alt text](image-1.png)

It begins with a starting IP address and is separated by a forward slash (the “/” character) followed by a number. The number at the end specifies how many of the bits of the IP address are fixed. In this example, the first 24 bits of the IP address are fixed. The rest are flexible. 

32 total bits subtracted by 24 fixed bits leaves 8 flexible bits. Each of these flexible bits can be either 0 or 1, because they are binary. That means you have two choices for each of the 8 bits, providing 256 IP addresses in that IP range. 

The higher the number after the `/`, the smaller the number of IP addresses in your network. For example, a range of `192.168.1.0/24` is smaller than `192.168.1.0/16`.

When working with networks in the AWS Cloud, you choose your network size by using CIDR notation. In AWS, the smallest IP range you can have is `/28`, which provides you 16 IP addresses. The largest IP range you can have is a `/16`, which provides you with 65,536 IP addresses.
