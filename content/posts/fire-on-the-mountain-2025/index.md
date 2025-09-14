---
title: "Fire on the Mountain 2025"
date: 2025-09-10
draft: false
summary: "Live streaming a tent revival from Grundy County, TN"
tags:
  - network
  - audio/video
  - livestreaming
  - video
  - streaming
---

Every year my wife Meg and I go down to Grundy County, Tennessee with [Recovery Soldiers Ministries](https://recoverysoldiersministries.org/) to their Fire on the Mountain tent revival. Meg is in their worship team and I help out with their tech team at times but during Fire on the Mountain, I’m in charge of providing the live stream. I’ve done this for the past 3 years and this year was the smoothest and quickest setup we have had so I wanted to document it and maybe share some tips and tricks of things I have learned along the way.

## Networking

The main component of the whole setup is the network that I bring in. Almost everything in my streaming setup is network based so a properly setup network is key.

The main internet connection is brought in by Ben Lomand Connect and they drop a fiber ONT and a wireless router under our stage. They provide a free WiFi for anyone attending but they let us plug into their router for a hard wired connection for our production equipment. 

See below diagram of our network and I'll explain more in depth about how it's set up and why I did it this way.

{{< mermaid >}}
flowchart LR
    ISP[Ben Lomand Connect Router]
    ISP --> SS[Stage Switch]
    SS --|Untag 1, Tag 99|--> FOH[FOH Switch]
    FOH --|U1|--> SW[Firewall]
    FOH --|U99|--> SW
    FOH --> Mini[Mini FOH Switch]
    Mini --> iMac[Presentation iMac]

    FOH --> AP((Access Point))

    POV([POV Camera]) --> SS
    S1([Static Stage Camera]) --> SS
    PTZ([PTZ Camera]) --> SS
    WLS1([Wireless Cam 1]) -.-> AP
    WLS2([Wireless Cam 2]) -.-> AP
{{< /mermaid >}}

### Stage Switch

The first part of the production network is the Stage Switch that is under the stage. Our ISP connects into this switch and rides a WAN VLAN back to Front of House (FOH). The main reason for this is so I only have to run one cable between the stage and Front of House, or where the rest of the equipment is. Also on this switch are a few cameras. All of the cameras that we run for the event are networked and PoE powered. This lets us keep cabling clean and have quick setup/teardown processes.

### FOH Switch

The stage switch plugs into the FOH Switch. This is in a rack right beside of the stream operating position and has the rest of the network devices. The WAN VLAN terminates here and goes into our firewall.

### Firewall

I set up an old firewall for our production network, just so I can have my own DHCP scope and pre-set static IPs on cameras and devices ahead of time. This lets me do a majority of the prep and programming at home and know it will all work. 

### Access Point

This year I ran just one Unifi UK-Ultra AP at front of house, this was for devices like my phone and tablet to conenct to, but also for our two wireless cameras as they are networked as well.


## Audio

In the past few years we have been very simple for audio, taking a AUX feed from the front of house console and relying on bugging the FOH mixer to make adjustments for the stream.

This year I decided to mix my own stream audio completely. The FOH console is a Allen&Heath QU-32 which can let me connect a computer via USB and get multi-track audio from it. This ran into my second laptop running Pro Tools and using Luke Hendrickson's broadcast template (https://productiononline.com/luke-hendricksons-broadcast-template/)



## Streaming PC



## Cameras


### Wireless Cameras


### Stationary Cameras


### PTZ Camera
