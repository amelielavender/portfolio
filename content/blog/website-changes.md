---
title: "Website Changes"
tags: ['updates', 'hugo', 'static site generators']
date: 2024-05-12T14:15:46-04:00
draft: true
images: ['background.png'] 
layout: blog
---

i felt like i shouldn't leave my poor li'l blog alone for too long so i figured i'd post what i've been doing with the site and how i'm getting along with [hugo](https://gohugo.io "hugo's homepage"), a static site generator. 

- dark mode
- table of contents moved to side
- smaller font
- tags on blog
- also added categories on blog
- edited main nav to have link to blog
- typography changes
  - smaller font
  - better looking headings
  - made blog text area more narrow and thus easier to read, esp if you sit closer to your monitor
- added a specific hugo shortcode for html `aside` elements. if you enable unsafe markup in your `hugo.toml` you can use regular html tags in your blog posts/markdown documents. you can add a callout/aside this way but you won't be able to use markdown inside of it, like this: 

`<aside>this is an aside **with bold text**</aside>`

it looks like this when rendered: 
<aside>this is an aside **with bold text** </aside>

the shortcode is a bit ~~Long-winded~~ annoying compared to just using html tags but it allows for something like this:

`{{</* aside >}}this is an aside **with bold text**{{</ aside */>}}`

{{< aside >}}this is an aside **with bold text**{{</ aside >}}

i might edit that shortcode to add something like a class or a title so i have can different flavors of callouts (like warning! or note: or idea). sounds kinda cute.
