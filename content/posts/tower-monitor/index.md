---
title: "Monitoring our radio tower over 4G"
date: 2026-04-19
draft: true
summary: "Setting up a Raspberry Pi with a 4G IoT SIM card to monitor our radio tower."
tags: ["monitoring","network","server","graphs","alerts","Grafana","Raspberry Pi","4G"]
---

This past week we have had some power issues at the [Kingsport Amateur Radio Club](https://w4trc.org/) tower located on Bays Mountain. We would notice at random times, our repeaters would be offline. The tower is a 30 minute drive up a service road from Bays Mountain park, so by the time we were free and could run up there, they would be online again. 

To figure out why this was happening and get better alerting on when it does happen, I decided to build a Raspberry Pi shack monitor that has 4G connectivity and can let us know when the shack power is down.

I had a few requirements for this project, one of those being it needed to be self-contained and standalone from any infrastructure other than power. This meant it needed to be on a 4G data connection for sending its checks and telemetry. For this reason I chose a Raspberry Pi with a SixFab IoT 4G card.

## Parts List
- [Raspberry Pi 4B](https://www.amazon.com/dp/B07TD42S27)
- [SixFab 4G Hat](https://www.amazon.com/dp/B089X8N2TY)
- [BME280 Sensor](https://www.amazon.com/dp/B0GRRDXGH8)


{{< github repo="joshuacarmack/karc-tower-monitor" showThumbnail=true >}}