---
layout: post
title:  "Bachelor project: GEAR"
date:   2017-02-04 15:00:00 +0200
categories: uni
excerpt: I've finished my bachelor project. We use gaze tracking and voice recognition to improve development workflow. Watch the video to see the final prototype.
image: /assets/images/gear-screen.jpg
---
I've finished my bachelor project for the Bachelor in IT at Aarhus University. The project ran for 6 months total, alongside other courses. The project was done by me and 3 other bachelor students. The question we tried to answer with this project was:

**"How can we use a combination of gaze- and speech-interaction to aid software developers?"**

Our vision for the project was established early. We wanted the developer to _simply look at the code, and say what he wants to happen_.

![Gear screen](/assets/images/gear-usage.jpg)
<p class="img-text">The prototype in action: A developer simply looks at the screen, and speaks to his computer.</p>

## GEAR - Gaze Enhanced Audio Recognition
The prototype consists of 3 parts:
1. An eye-tracker
2. A microphone (and voice recognition software)
3. The IDE (we used [Jetbrains IntelliJ](https://www.jetbrains.com/idea/), courtesy the student license through AU)

We used a [Tobii EyeX](http://tobiigaming.com/product/tobii-eyex/) to track the users gaze on the screen. This allowed the user to switch between editor tabs without using the mouse, and direct his voice command to the appropriate editor pane. We used the C# SDK for Windows, which allowed us to get a continous stream of input from the tracking bar.

We decided to integrate with [Dragon NaturallySpeaking](http://www.nuance.com/dragon/index.htm) through DragonFly. This allowed us to create a python script that can react to certain sentences and commands, and emulate keyboard and mouse input to the IDE. The python script communicated with the C# programme over TCP to know where the user is currently looking.

You can watch a presentation of the project on Youtube below (remember to watch in fullscreen 1080p).
<iframe width="560" height="315" src="https://www.youtube.com/embed/8wgXM70eQag" frameborder="0" allowfullscreen></iframe>