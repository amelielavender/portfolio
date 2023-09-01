---
title: "Nextcloud and Apache"
date: 2023-03-01T00:42:55-05:00
draft: true
layout: blog
---

note: this is the worst blog post in the world. it is very boring and you will die of boredom less than halfway through reading this. it's my blog though and i wanted to write it!!!!!!!

As a late birthday present to myself one day in February, I decided to snag the url `sapphic.online` just for kicks. I already had a digital ocean droplet running (just for a Valheim server, at the time) so I thought I could do something useful with the both of them in tandem.

## the next thing
It turns out that a while ago I had deleted all my files off of Google Drive and I'd been lazily floating alternatives ever since (I used big G's takeout service so I should have everything in theory but honestly, I've been too lazy to look). I decided to finally bite the bullet and look into Nextcloud. 

I can't really extol the virtues of Nextcloud as well as an actual fan would; I don't need it for much after all. If it can sync some selected files on a VPS for others' access then I'm good to go. I guess I just called myself a fake fan of a self-hosted gdrive alternative, huh. Oh well. 

But, seriously, there's a *lot* that Nextcloud does that I will probably never get to see or use like a kanban board, voice and text chat, e-mail management, along with the usual Google Drive/Documents stuff like forms, presentations, spreadsheets... The list is impressive, and it gets a lot bigger when you consider all the official and third-party apps that area available in the "app store".

Following this video tutorial on Learn Linux TV worked a treat. I followed Jay's instructions to the latter (mostly). I should have been done there. I should have been happy with my new and shiny `nc.sapphic.online` instance. 

Until I wasn't.

Of course, the thing that came to me as an afterthought was figuring out what to do with the actual top-level `sapphic.online` url. I thought it'd be a odd if someone curious went to it and they just got an error from Nextcloud talking about "illegal urls" (paraphrased since I don't recall what they called it). I wanted to put, really, anything there as my personal "hello, world". I'd also (correctly) assumed that figuring out how to serve two different websites living on one VPS would net me knowledge about how to set up other subdomains.

## nextcloud nation
So after some quick searches I learned that apache can serve multiple websites on one ip address via something called virtualhosts. These virtualhosts are called for by the `<VirtualHost>` directive. Here's an example I took directly from apache's website.

```apache
Listen 80
<VirtualHost *:80>
    DocumentRoot "/www/example1"
    ServerName www.example.com

    # Other directives here
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "/www/example2"
    ServerName www.example.org

    # Other directives here
</VirtualHost>
```

After poring over a few more examples, I set up my apache configs in my `/etc/apache2/sites-available` directory and, hey, it didn't work? Why is that?

Let's take a closer look at my personal directives inside of one of my config files:

```apache
<IfModule mod_ssl.c>
<VirtualHost *:443>
    Header always set Strict-Transport-Security "max-age=15552000; includeSubDomains"
    ServerName sapphic.online

    DocumentRoot /var/www/sapphic.online
        
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

	SSLCertificateFile /etc/letsencrypt/live/sapphic.online/fullchain.pem
	SSLCertificateKeyFile /etc/letsencrypt/live/sapphic.online/privkey.pem
	Include /etc/letsencrypt/options-ssl-apache.conf
</VirtualHost>
</IfModule>
```

For all intents and purposes, I'm pretty sure this is at least "okay" to use. My `nc.sapphic.online-le-ssl.conf` looks pretty much the same. But again, why was I being redirected from what I wanted to be my "root" domain to my nextcloud instance?

There are a couple of un-obvious clues here, especially as a first time apache user. I ended up replacing every wildcard (`*`) with the specific domain name that I was trying to get apache to server properly. I don't think this is best practice, at least according this stack overflow answer:

> Using a fully qualified domain name for the IP address of the virtual host is not recommended. It is misleading how it works. Name based virtual hosts determine the host through the `ServerName` directive, and not through the FQDN in the `VirtualHost` directive (`<VirtualHost FQDN:80>`). In fact this is seen as `<VirtualHost 127.0.0.1:80>`

Anyway, me and my VPS chugged along for several months with this band-aid fix. I even learned that apache can do reverse proxying in the meantime. Do I know anything more apache now than when I first started? Barely. There are just too many directives to wrap my head around and the official documentation is way to obtuse for me to grasp. But one night,  I was working on this very website and I decided to try and finish this very blog post you're reading. It was going to end way back when I talked about "fixing" the problem via changing every single `<virtualhost>` IP to a FQDN but for some reason I wanted to go **deeper** and not long after, had some brain blasts that honestly came from nowhere. 
### the first clue
When you first install apache on a Debian or Ubuntu server, you'll be introduced to the typical "it works!" page if you, well, try and test out your server. Keep looking through that page and you'll eventually find a section that talks about *how it was extremely important that Debian explode upstream apache's config files into bits and pieces in order to "fit" the "tooling" better*. Sure. I didn't think anything of this at first. I figured all I had to do was work on my specific websites' configs and I'd be fine. 
### the second clue
Apache comes with a tool called `apachectl` with which you can check various things and tell apache to do... whatever else. Most importantly it has a utility to parse and check if your configs are in order. Whenever I'd run `apachectl configtest` it always gave me a warning that went a li'l something like this: `AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1. Set the 'ServerName' directive globally to suppress this message`.

wildcard make apache serve the first servername it finds which was in this case localhost or 127.0.01 which makes it crawl thru all the configs and serve the first one that it finds in alphabetical order.

Can you see what's happening, yet? If we go back to when my config contained wildcards (`*:80` and so on...) apache looks for the server's FQDN declared globally. When this isn't declared, it assumes 127.0.0.1 and crawls through the sites enabled until it hits the first one it feels meets this FQDN requirement, most often the first one in alphabetical order. 

lol jk setting the servername in the global config didn't do anything 