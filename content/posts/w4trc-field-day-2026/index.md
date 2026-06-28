---
title: "W4TRC Field Day 2026"
date: 2026-06-26
draft: true
summary: "Setting up logging system for Kingsport Amateur Radio Club's Field Day event, and making it complicated."
tags: ["networking","radio","amateur radio","w4trc","cloudflare","web app"]
---

Every year, [Kingsport Amateur Radio Club ](https://w4trc.org/) participates in the American Radio Relay League (ARRL)'s Field Day event. During this event radio clubs and operators across the US set up, test their emergency equipment, and operate for 24 hours. We normally set up somewhere in Kingsport and operate up to 3 radio stations as much as we can.

For this event, we utilize computerized logging software to track other stations that we contact. We use this to compile our contacts and submit our logs to the ARRL. As part of this, part of my job is to set up the logging systems and this year we changed it up a bit.

## Last Year

Our setup last year was pretty simple. I keep a few spare laptops on hand ready for events like this and we used a simple wireless router to have a local area network (LAN) for them to communicate on. 

## This Year

For this year, I took this a step further. This year we had a working internet connection, used some different logging software, and had some custom made software that communicated with this logging system.

### The Internet Connection - Starlink

This year, we got a Starlink dish to provide internet access at our field day location. We set up at Netherland Inn and would not have any public internet access. Internet is not necessary for this event, but it is just another communication method we could deploy in emergencies so I wanted to test that out. 

Our setup was really simple, I used a Starlink Mini on a Roam plan which provided up to 100 Mbps download and 20 Mbps upload speed which was plenty for our small network. I set this up on a small tripod and ran a power and ethernet line to it. 

![Starlink dish on a tripod](starlink-dish.jpeg)

The Starlink Mini is a fantastic piece of equipment and we could run this off of a generator or battery power if needed.

### The Network - Old Sonicwall Firewall

Because I placed the Starlink away from the shelter where it would have a clear view of the sky, I wanted to use a different router and wireless access point closer to where the computers would be. For this, I used an old Sonicwall firewall that I had in my spare IT kit. 

You can place the Starlink in bypass mode, which disables its own built-in router and lets your external router handle DHCP/DNS and routing. From there I was able to broadcast a wireless network.

This equipment lives in a small waterproof box that we sit to the side.

![View of the network box with firewall and mini PC](network-box.jpeg)

### The computers

I set up 4 PCs that we use for logging. These are just some basic Lenovo and HP laptops running windows. They are all connected to the wireless network and one is sat beside each radio with a spare just in case we need one.

### The "Mini Server"

I run a Larkbox Mini PC as our "Mini Server". This is a small Windows PC that hides in the network equipment box and runs as the primary logger and agent for the custom software I will cover later in this post.

![Mini Server](mini-server.png)

### The software - N1MM Plus Logger

Previously we have used N3FJP logger which I am a fan of, but I wanted to try something new this year.

My main issue with N3FJP is it operates with one computer having a master log and it shares this file over SMB to the other computers. In the past I have used the Mini Server which has a file share that this log file lives in. This was designed so we could reboot the laptops if needed or swap them around and have no issues with the log file.

N1MM networked mode works a little bit better in my opinion. Each computer maintains its own SQLlite database for the log file, but broadcast each contact it makes over multicast. This lets each other computer add the contacts other computers make into its log. We do this for duplicate detection, as in field day you are not supposed to contact the same station on the same band and mode, or it is a duplicate contact. Networking the computers together makes this duplicate detection work no matter what computer the contact was made on.

N1MM just feels more robust to me, as any computer can drop offline, even our "master" of the Mini Server and the other computers will still have their logs and resync when the others come back online.

Because N1MM broadcasts any contacts that are made over the network, this gave me the idea of being able to capture these contacts and make a public dashboard on our website.

### The Sending Agent



### The Website Dashboard



### The Desktop App


### Reporting


## Review

