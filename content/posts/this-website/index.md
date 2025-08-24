---
title: "How I Made This Website"
date: 2025-08-01
draft: false
summary: "I wanted to learn more about Hugo, so I built this site in it."
tags: ["development","website","cloudflare","dns","coding","hugo"]
---
## How did I make this website?

This website is built using [Hugo](https://gohugo.io/) which is a framework for building static websites easily. I got tired of having to maintain WordPress installations for simple websites so I looked for something simpler. 

You can install Hugo and run a simple command such as "hugo new site joshuacarmack.com" and it will build the entire site for you and then you can edit it. 

I used a theme called [Blowfish](https://blowfish.page/) to make the site look the way I wanted. Blowfish has their own tooling that I used to create the site. It was as simple as running a command "blowfish-tools new joshuacarmack.com" and it sets up Hugo and installs their theme and a starter site.

From there I made a few changes to the homepage to list my projects and change the menu bar. From there it's as simple as adding a new folder in the content folder and a simple markdown file to create a blog post.

I can edit the site from VS Code at home, using Working Copy on my iPad, or editing text files on GitHub.

The entire site is on a GitHub repo at [https://github.com/joshuacarmack/joshuacarmack.com](https://github.com/joshuacarmack/joshuacarmack.com). You can see the files that Hugo runs and see any changes I have made.

The site actually runs on Cloudflare Pages. Anytime I push to the master branch on that repo, Cloudflare sees that there has been an update and will rebuild the site and update it within a few minutes. 

This being a static website means that it loads quickly and has very little scripts to load in the background before you see content. 

I highly recommend checking out Hugo if you want simple and fast websites or blogs.