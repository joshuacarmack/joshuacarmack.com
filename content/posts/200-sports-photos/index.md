---
title: "Taking 200 player photos and keeping track of them all..."
date: 2025-08-22
draft: false
summary: "Every year I help take player photos for our church's soccer league."
tags: ["photography","automation","photos","photoshop","camera"]
---

# Intro

Every year my church has a Upward Soccer league with almost 200 players ranging from 3 years old through high schoolers. I volunteer to take the player and team photos. Being able to quickly take photos and tag them with the player information is crucial as we have to get through all of them in just a few hours. 

The way this worked this year is we had 3 people getting the kids in line and finding their player card which has a unique ID, and then passing it to me as the kid had their photo taken, and then we would do a full team picture. In addition to those 3 people putting them in order I had 1-2 helpers who would pose the kid while we were getting everything else ready. This worked really well and helped us keep the line moving and get through everyone easily.

Once the photos are taken I use a lot of computer automation to process the photos, create a player card image, and rename them before they are uploaded to our gallery website for the parents to view and purchase prints.

In this post I'm going to give all the details on how we accomplished this photo session.

# Set Up

## Player IDs

As the season begins I get a player roster from the coordinator and I build a spreadsheet of these teams and players. I have a column for the team name, the player first and last name, and then some IDs.

![Spreadsheet of player IDs](playerid-sheet.png)

The Team ID is a 2 digit ID just starting at 1 and each team has an ID. The player ID is just an incremented unique ID for each kid plus a few spare cards in case there were late additions.

The data shown here is some made up names but you get the idea. 

I then have a column concatenate these IDs and give me a 5 digit ID for each player. The reason I do this is for sorting later. I can easily sort each player into a folder based on their team number. When I publish the gallery I like to have albums for each team so the parents can find the photos easier.

## ID Cards

This year was the first year we used ID cards to be passed between the helpers and myself. Last year they had the spreadsheet I made and would give me the 5 digit ID to be manually entered into my software. This works but it was time consuming and confusing to make sure we had the numbers correct. 

Using a Dymo label printer I was able to export my spreadsheet as a csv file and import into the Dymo software. From there I made a simple design with the player name at the top, a barcode encoding the player ID, the ID larger, and the team name.

![Card with player name, barcode, number, and team name](playerid-card.png)

This worked really well for us. Prior to the shoots I printed all of these out and separated them into teams to make it easier for the helpers to find the team and player as we tend to shoot out of order as the kids arrive.

I printed these out on [Dymo compatible non-adhesive business cards](https://www.amazon.com/dp/B0BKG8C9KS?ref=ppx_yo2ov_dt_b_fed_asin_title) and I was super happy with how well this worked.

