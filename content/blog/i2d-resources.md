---
title: "I2d Resources"
tags: ['inochi2d', 'vtubing', 'open-source', 'links']
date: 2024-02-18T14:14:51-05:00
draft: false 
images: [''] 
layout: blog
---

this is a personal collection of resources for the inochi2d set of software that includes inochi session and inochi creator. most, if not all of these resources were originally posted in the inochi2d discord server and most recently gathered together through an effort by Licore et. al. thanks a lot!

please be aware that these resources are relevant as of the date of this blog post, 18 February 2024 and may not reflect the most up-to-date i2d software.

## general

### documentation

#### [Unofficial documentation](https://docs.google.com/document/d/1c6wNwVipg4NZ_XPUJJL-hdZarJrX9rGu1tLPNRCvbjw/edit?usp=sharing)
written by higasa mitsue. probably the most extensive writeup on inochi2d creator and session to this day. might be missing stuff introduced with the latest release (0.8.3).

#### [Official FAQ](https://docs.inochi2d.com/en/latest/inochi2d/faq.html)
answers things like cost, live2d compatibility, licensing...

#### [Official docs](https://docs.inochi2d.com/en/latest/)
contains a mini tutorial to get you up and running with i2d software, as well as developer docs (WIP as of this writing).

#### [Discord](https://discord.gg/inochi2d-community-855173611409506334)
the Official inochi2d community discord server. you can get real time help and assistance here as well as show off your creations. 

### videos

#### [How to Rig a Vtuber Model](https://www.youtube.com/watch?v=wNwoKXeqtQY)
Dragonator96 shows you the general steps for rigging a vtuber and setting it up in OBS. uses an older version of both creator and session but much of it still applies to 0.8.3.

#### [Rigging by seagetch/seagetty](https://discord.com/channels/855173611409506334/855173611409506337/1123160353421930526)
discord link
- Part 1 : Defining hierachy and meshes
- Part 2 : Arming facial parameters
- Part 3 : Arming body parameters
- Part 4 : Adjustment of some parts and arming physics parameters

#### [inochi creator from the very beginning](https://www.youtube.com/playlist?list=PLobCmNaRKsjUApKCu2zd5-EhQjdrEbcXZ)
a youtube playlist by yuçuna that shows you everything right from the beginning, starting with importing your first model. also covers some inochi vocabulary, like nodes, etc. WIP, i think.

#### [rig with me by navy prince](https://www.youtube.com/watch?v=KcOxxSNwFLs)
recording of a rigging livestream. 

#### [rigging vods](https://www.youtube.com/playlist?list=PLHSSzKuby9Jj4GFl1K3YI0r-pT8VJSAqp)
by arteno enjo. another stream vod. 

## how do i...?

### open inochi creator on macOS?

as of 0.8.3, inochi creator needs some manual massaging to open on macOS. please refer to the following steps in order to get creator to see SDL2 properly.

1. Right click Inochi Creator, Show package contents
2. navigate to Contents/Frameworks
3. rename `libSDL2-2.0.dylib` to `libSDL2.dylib` 
(via Luna)

### work with flip pairings?
{{% aside %}}
a flip pairing is a configuration of parts that are generally the left nd right of a given rig. for example, i might have a part named `Eye::Left` and create a flip pairing with its counterpart `Eye::Right`.
{{% /aside %}}
<p></p>

#### [copy and paste a mesh to use with other parts?](https://discord.com/channels/855173611409506334/888154799357440030/1080316944495943790)
discord link

if you would like to copy a mesh that you've already created from one node to another node, switch to your target node and then drag the name of the node from the nodes menu onto the Edit Mesh button. the buttons should then change into "Copy Mesh" and you can drop the mesh onto the button to copy it.

#### [copy a rig to its symmetrical counterpart?](https://discord.com/channels/855173611409506334/888154799357440030/1128340725025738813)
(eg left eye to right eye blink) - discord link
seagetch shows how to copy a rigged right eye parameter to Ada's left eye.

#### create flip pairings?
TODO

### export video
#### export video from inochi creator?
[install ffmpeg](https://ffmpeg.org/download.html) 
if you've created an animation in inochi creator and would like to export a video of it directly, you'll need to install ffmpeg. the export animation menu entry will be disabled otherwise. 

### use the path deform tool?
#### [use the path deform tool?](https://youtu.be/gPMdlKGLELE?si=9OGjWKNJektpooEC)
Inochi2D Physics and Path Deform by Horns for Eyes shows you how to use both the path deform tool and the physics engine in inochi creator.

### use physics?
#### rig physics?
see above video

### use expression bindings?

#### [inochi session wiki](https://github.com/Inochi2D/inochi-session/wiki)
not too user-friendly but if you know a bit of lua and how math works, you'll probably understand this pretty quickly.

#### [expresison bindings test model by navy prince](https://ko-fi.com/s/7a25339fbe)
this includes both an inp and inx file to play with.

#### [expression binding notes](https://docs.google.com/document/d/11Xsjy5mZml6OIpqDdt9xfz32onw2OsO2bwTv_smuH8Y/edit)
also by navy prince

## external software 
### tracking
#### [puppetstring](https://ar14.itch.io/puppetstring)
desktop webcam tracking solution for inochi session. you can use various inputs to control your rig with this software, including mouse tracking, face-tracking, button toggles and more. if you care, by the way, PS is *not* open source.  

#### [OpenSeeFace](https://github.com/emilianavt/OpenSeeFace)
"Robust realtime face and facial landmark tracking on CPU with Unity integration"

#### [VtubeStudio](https://denchisoft.com/)
"VTube Studio is an app for Virtual YouTubers that makes it easy and fun to bring your own Live2D models to life."

### dependencies
#### [ffmpeg](https://ffmpeg.org/download.html) 

## tips and tricks

### L2D tuts applicable to inochi
{{% aside %}}
i've not vetted or watched any of these live2d tutorials. proceed at your own risk?
{{% /aside %}}
### rigging tips
### fun effects
[rigging a 90 degree head turn](https://youtu.be/LKPhURDQbh4?si=Q4Zy1yRLnaAGX-Cx)
cool as hell tbh

sorry i got bored here. TODO
