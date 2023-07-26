---
title: "Nextcloud and Apache"
date: 2023-03-01T00:42:55-05:00
draft: true
---

As a late birthday present to myself one day in February, I decided to snag the url `sapphic.online` just for kicks. I already had a digital ocean droplet running (just for a Valheim server, at the time) so I thought I could do something useful with the both of them in tandem.

It turns out that a while ago I had deleted all my files off of Google Drive and I'd been lazily floating alternatives ever since (I used big G's takeout service so I should have everything in theory but honestly, I've been too lazy to look). I decided to finally bite the bullet and look into Nextcloud. 

I can't really extoll the virtues of Nextcloud as well as an actual fan would; I don't need it for much after all. If it can sync some selected files on a VPS for others' access then I'm good to go. I guess I just called myself a fake fan of a self-hosted gdrive alternative, huh. Oh well. 

But, seriously, there's a *lot* that Nextcloud does that I will probably never get to see or use like a kanban board, voice and text chat, e-mail management, along with the usual Google Drive/Documents stuff like forms, presnetations, spreadsheets... The list is impressive.

Following this video tutorial on Learn Linux TV worked a treat. I followed Jay's instructions to the latter (mostly). I should have been done there. I should have been happy with my new and shiny `nc.sapphic.online` instance. 

Until I wasn't.

Of course, the thing that came to me as an afterthought was figuring out what to do with the actual top-level `sapphic.online` url. I thought it'd be a odd if someone curious went to it and they just got an error from Nextcloud talking about "illegal urls" (paraphrased since I don't recall what they called it). I wanted to put, really, anything there as my personal "hello, world". I'd also (correctly) assumed that figuring out how to serve two different websites living on one VPS would net me knowledge about how to set up other subdomains.

## virtualhosts

So after some quick searches I learned that apaches can serve multiple websites on one ip address via something called virtualhosts. These vrtiaulhosts are called for by the `<VirtualHost>` directive.
