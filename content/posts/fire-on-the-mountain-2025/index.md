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

```mermaid
flowchart LR
    ISP[Ben Lomand Connect Router]
    ISP —> SS[Stage Switch]
    SS —|Untag 1, Tag 99| FOH[FOH Switch]
    FOH —|U1| SW[Firewall]
    FOH —|U99| SW
    FOH — Mini[Mini FOH Switch]
    Mini — iMac[Presentation iMac]

    FOH — AP((Access Point))

    POV([POV Camera]) —> SS
    S1([Static Stage Camera]) —> SS
    PTZ([PTZ Camera]) —> SS
    WLS1([Wireless Cam 1]) -.-> AP
    WLS2([Wireless Cam 2]) -.-> AP
```


## Audio



## Streaming PC



## Cameras


### Wireless Cameras


### Stationary Cameras


### PTZ Camera
