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

I sourced all of my parts from Amazon for the quick delivery as I wanted this built in just a few days so we could deploy it on the next trip up to the tower.

- [Raspberry Pi 4B](https://www.amazon.com/dp/B07TD42S27)
- [SixFab 4G Hat](https://www.amazon.com/dp/B089X8N2TY)
- [BME280 Sensor](https://www.amazon.com/dp/B0GRRDXGH8)
- USB C Power Adapter
- MicroSD Card


## Hardware Setup

To begin with the hardware setup it is pretty easy, unbox all of the parts and start assembling the main Raspberry Pi board. Add the SixFab 4G hat, install the PCIe card, connect the antennas, insert the SIM card, and plug in the USB cable.

For the temperature sensor this took a bit more work. First I had to solder on the 6 pin header to the module and then connect the 4 cables needed for I2C communications to the Pi.

![Photo of a Raspberry Pi and cables](IMG_4788.jpeg)

Once everything was connected, it was time for the software. 

## Software Setup

For the software side of the project, I wanted it to work a certain way. I have been learning MQTT messaging recently and knew it was a very lightweight and data efficient way of sending a bit of data across the internet. So for this project I could send an MQTT message from the Pi to my home MQTT broker running EMQX. From there this data could flow into [InfluxDB](https://www.influxdata.com/) for long term storage, into [Home Assistant](https://www.home-assistant.io/) for alerting, and into [Grafana](https://grafana.com/) for graphing. These parts of the setup I already have in place, so it made sense to go this route.

### Python Script

For the software, I did enlist the assistance of Claude Code. So fair warning most of the code was AI written. It is a very simple Python script and the GitHub repo is below.

{{< github repo="joshuacarmack/karc-tower-monitor" showThumbnail=true >}}

The main part of this code is a simple script that does a health check every 10 minutes and sends it to my MQTT broker for distribution. The script collects a few pieces of data from the Pi itself such as uptime and cell signal, and it also gets data from the BME280 sensor for temperature, humidity, and barometric pressure. Once it gets all of this data together, it makes a simple message and sends it out. This data is only about 0.2 MB per day of traffic coming from the Pi. 

### MQTT Reception

The data gets received by the MQTT broker running on my server at home. Think of the MQTT broker as a bulletin board, the Pi sends its telemetry and it gets put on the bulletin board for anyone else to see it. 

An example of this data is below. This data is shown in a program called MQTT Explorer, which is a great tool for seeing realtime data and verifying that it is working properly.

![MQTT Data sceenshot](mqttdata.png)

Once we have the telemetry in MQTT we can begin using it for our different pieces.

### Home Assistant

The main piece that I wanted this data for, was Home Assistant. Home Assistant (HA) is a home automation platform that I use for some smart home devices, but one of the neat things it can do is injest this MQTT data, show it on dashboards, and give alerts off of it. With the help of the Claude Home Assistant MCP, I was able to have it generate a quick dashboard showing all of the statistics that the tower Pi was sending.

![Home Assistant dashboard with data](ha-dashboard.png)

From this, I can get a quick overview of what is going on. 

Once I know the data works, we can begin creating some automations. The first I wanted to do is get an alert if we haven't heard from the Raspberry Pi in 30 minutes. If it stops sending the data, we can assume that the power is offline, or the Pi has an issue. This at least gives us an alert to check the repeaters and see if they are working. To do this, we do a simple check for when the Tower Status sensor changes to Unavailable for 30 minutes, and then we wait 5 minutes to make sure it is still offline and then send the alert. 

![Home Assistant alert automation configuration](ha-alertconfig.png)

We also do this in reverse, if the status changes from Unavailable to Online, we send an alert that it is back online.

