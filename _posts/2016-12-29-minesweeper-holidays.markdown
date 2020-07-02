---
layout: post
title:  "Minesweeper holidays"
date:   2016-12-29 21:12:37 +0200
categories: work
excerpt: I've created a typescript version of the minesweeper game, and an AI that plays it for me. Implemented using Angular 2 and with Angular Material of course.
image: /assets/images/minesweep-ai.png
---

I've created a small minesweeper game in Angular 2 to refresh my Typescript in the holidays. I decided to give the [Angular-CLI](https://github.com/angular/angular-cli) a spin, and check the current state of [Angular Material 2](https://material.angular.io/).

I also wanted to try some game AI technigues, so the game and the AI is inspired by a chapter in [Introduction to Game AI](https://www.amazon.com/Introduction-Game-AI-Neil-Kirby/dp/1598639986). The original project in the book is implemented in Visual Basic, and with quite a different aesthetic.

![AI in action](/assets/images/minesweep-ai.png)
<p class="img-text">The rules based AI in action. Notice the sidebar text is a little cramped.</p>

#### The AI
The AI is a rules based AI. Every iteration, every possible rules efficiency is evaluated, and the one yielding the highest score wins. For example, the "mark fields as bombs"-rule has a score equal to the number of fields we are 100% sure are bombs at the current state of the board.

The AI picks the rule with the highest score at every iteration. This usually results in it either marking a set of fields as bombs, or exposing a set of fields that it knows are safe.

I choose not to make the AI "guess" when there are no more fields so safely mark or expose (it happens in minesweeper), as I do not want to take away the *thrill of failing* away from the user.

#### Take it for a spin
You can [try the minesweeper game](http://hauthorn.me/ng-minesweep/) here on this site. It's published using github pages, which is easy to do using the angular cli (just run `ng github-pages:deploy`, and you are golden).