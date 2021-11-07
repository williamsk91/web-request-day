---
title: A Day in the Life of a Web Page Request
slug: /
---

# A Bright Morning

Hi Bob!

> I'm not Bob

Well, you are now

> Okay...

I see you want to access the internet and go to this site called www.google.com

> No, not really... Why did you even start talking to me? Who are you?

Don't sweat the detail Bob. Here, let **ME** teach you what goes in the background
from when you type www.google.com in your browser until you get this

{Google landing page image}

> What?! I don't have time for this!

We start at the beginning

> Oh no...

## Starting Map

Here is our starting map. We will assume a few things

- You are connected to the internet through an ethernet cable
- You are in your school netwrork (hopefully studying hard)
- Your internet service provider (ISP), the one you pay to access the internet,
  is called Comcast

<!-- {Starting map} -->

> Huh, it's not as complicated as I expected

That's the spirit! We will break down each steps even further

> O... How many steps are there?

There are just 4 main parts

1. Obtaining important IP addresses (including yours, Bob)
2. Translating IP address to MAC address
3. Obtaining Google's IP address
4. Requesting and receiving data from google web's server

> What are IP and MAC addresses?

- MAC address - Unique ID for you computer. Used to identify and communicate with
  other computers **within** your local network (e.g. your school).
- IP address - Unique ID for your computer. Used to identify and communicate with
  other computers **outiside** your local network, the **internet**. It can change when you move from one network to another!

> So MAC address is like my ID and IP address is like my home address?

Exactly! Are you some kind of genius Bob?

> Hehe 😏

Moving on! When your computer connects to the internet, let's say through Ethernet,
it runs a protocol to get an IP address.

## Dyanamic Host Control Protocol (DHCP)

```
{DHCP map and flow}

Bob -> Switch -> Router
```

1. Your computer screams to every single connected device.

   Bob: Hi all! I'm Bob. Can someone give me an IP address?

2. Connected devices, such as switches, rescreams this information until it
   reaches a device that can give you an IP address.

   Switch: Bob is desperate for an IP address. Can someone give it
   to him?

3. The router eventually hears this. Gets an IP address for you and sends it back.
   This time not screaming to everyone as the router knows where you are through
   your MAC address.

   Router: Bob, here is an IP address you can use
   Switch: Bob, here is an IP address you can use

4. The information reaches you and you now have and IP address!

> Yey!

5. Not only that, you also get 2 other IP addresses we will soon use

- First Hop Router's IP address
- DNS server's IP address

This set of steps to obtain an IP address is call **Dynamic Host Control Protocol
(DHCP)**. We will see that the internet is made up of many different protocols.

> Cool~

{Updated map with IP addresses}

The DNS server will help you get the IP address of www.google.com. However,
to reach it we need to go outside of our local network.

```
Bob -> router -> other routers -> DNS
```

It's important to note that, to talk with devices within your network you use
MAC addresses, while communicating outside you use IP addresses.

And since the Router is within your network we will need its MAC address.

## Adress Resolution Protocol (ARP)

**Adress Resolution Protocol (ARP)** is used to translate IP addresses to
MAC addresses.

```
{ARP map and flow}

Bob -> Switch -> Router
```

1. Your computer once again screams to every single connected device.

   Bob: Hi all! I'm Bob. Can someone at IP address give me their
   MAC address?

2. The router once again hears this. Notice that the IP address being referred to
   is it's own IP address. Then replies with it's MAC address.

   Router: "O, that's me! Here's my MAC address, Bob"

3. The information then travels back to you. You now have both the IP and MAC
   addresses of the first hop router

{Updated map with IP & MAC addresses}

## Domain Name Service (DNS)

> Can we talk to the DNS now?

Indeed

```
{DNS map and flow}

Bob -> Switch -> Router -> other routers & switches -> DNS server
```

1. Your computer writes a query message to the DNS server.

   Bob: Hey DNS, what is the IP address of www.google.com?

2. The query message reaches the DNS server.

3. The DNS server look for this information in its database and returns a
   DNS record.

   DNS: Bob, www.google.com lives at IP address

4. The message then travels back to you

5. Your computer sees this message and store this locally for some period of time.
   The next time you write www.google.com your computer can use the same
   IP address and skip the entire DNS server trip!

{Updated map with IP & MAC addresses & google IP}

> Wow, long trip this time. What else do we need now?

As a matter of fact, you are all set to contact www.google.com.
You have your own, Google, and routers IP addresses. As well as our own and router's
MAC address. We are ready!

> let's goooooo!

## HyperText Transfer Protocol (HTTP)

```
{HTTP map and flow}


Bob -> router -> router -> Google
```

1. The protocol used to send and receive web data is called HyperText Transfer
   Protocol (HTTP), you might have heard it. Contrary to the other protocols we
   have encountered so far, HTTP uses Tranmission Control Protocol (TCP) underneath the
   hood.

> What difference does this make?

This adds an overhead before even asking google for data

2. First, your computer will try to establish a connection using a 3-way handshake

   Bob: Hey google, available for some data transfer?

   Google: Sure, for you, anything 😉 , Let's talk using this channel

   Bob: Fantastic, let's do that

3. Only then, can you ask for data using the established channel

   Bob: Can I please get data for your homepage `www.google.com/index.html` ?

   Google: Here you go

4. Your browser sees this message, extract data from the body of the message
   and finally display it on your screen!

> Wow

Yea, you now know more from when me started a couple of minutes ago! We saw that
internet uses many different protocols to communicate with each other. Computers
have MAC and IP address akin to ID and home address of people. And different
devices are there for many different purposes, such as the DNS for translation.

# Extras

## The need for DNS

> So if I know the IP of Google I won't need DNS service?

Yes, try entering [172.217.31.255](http://172.217.31.255) into your url bar. This is google's IP address and should work like normal.

## Internet layers done separately

The Internet itself is made up of 5 distinct layers. Each built on top of each
other.

| Layer       | Detail                                     | Examples                              |
| ----------- | ------------------------------------------ | ------------------------------------- |
| Application | The one you interacts with                 | HTTP for web browsing, IMAP for email |
| Transport   | Sending and receiving data                 | TCP, UDP                              |
| Network     | End to end routing                         | IP                                    |
| Link        | Hop to hop routing                         | ARP                                   |
| Physical    | actual data transfer through maybe a cable | Ethernet                              |

:::info

Each protocol we have used lies somewhere in the Internet layer

:::

## Acknowledgement

Many of the information here is extracted from Chapter 6.7 "Retrospective: A Day in the Life of a Web
Page Request" of [Computer Networking: A Top-Down Approach book by Kurose and Ross](https://gaia.cs.umass.edu/kurose_ross/index.php). The book goes into deeper detail for each layer and is highly recommended.
