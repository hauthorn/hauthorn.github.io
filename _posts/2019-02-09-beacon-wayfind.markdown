---
layout: post
title:  "Using beacons to out-compete googles indoor navigation"
date:   2019-02-09 11:35:00 +0100
categories: emplate work
excerpt: We are doing more work to build reliable and accurate in-door navigation
image: /assets/images/emplate-wayfind/emplate-wayfind-round-icon.png
---

In Emplate, we try to improve the shopping experience for the visitors. We've done alot to improve the utility of the app while at home, but recent had more consumers that ask for wayfinding capabilities in the app.

Using the "Own time" (4 hours every sprint that is free to be used on any project the employee deems interesting/worthy) provided to all employees at Emplate, I wanted to test the following hypothesis:

1. **Can I visualize my current location** in a intuitive way? (wilst also conveying some of the inaccuracy that the solution has)
2. **Is the tracking accurate enough** that it might be used instead of existing solutions? (eg. Google Maps)
3. Given our current knowledge of the layout at Storcenter Nord, **can we provide turn-by-turn navigation?**

## Where are our beacons placed?
<div style="float: right; margin: 1em;">
<img src="/assets/images/emplate-wayfind/2019-01-17-beacons-located.jpg" alt="Beacons in Storcenter Nord" style="max-width: 320px; height auto;">
<p class="img-text">Using the prototype our dev Mieszko built during his internship, <br>I located beacons in the mall.</p>
</div>
We have bluetooth beacons placed at the entrances to the stores in the mall.
Using an app that one of our student programmers built during his internship here, I located the beacons on the map, and sent the exact locations to our system for use in the future.

The app is shown in the image to the right.

Once all beacons were located, I was ready to build my small prototype that would show my location based on the signal from the beacons to my phone.

By the way - locating and using the app to send the coordinates in SCN took about an hour. Now we just need to keep it up to date 😂 

<div style="clear: both;"></div>

## Emplate Wayfind
I setup a simple app with Google Maps integrated in order to show the map of the mall (and of course to compete with Google for best location service).

Listening for the beacons is easily done using the SDK that our supplier [Kontakt.io](https://developer.kontakt.io/mobile/android/sdk/) provides us.

Then there's the hypothesis: *Can I visualize my current location in a intuitive way?*

To get a sense of the data we ready from the sensors, I started displaying every beacon in sight, using opacity to show signal strength (used as a proxy to distance to the beacon).
This gives a sense of how many sensors the phone picks up at any given point in time, but leaves alot to the user to process. It's probably better to go with a circle showing the approximate location of the user.

Another observation from testing: we rarely have good signal from more than 3 beacons at a time.

This informed the design:

- Show a circle that encloses the 1-3 nearest beacons at any time.
- If only one beacon is in range:
    - Chose center of the circle to be the location of the beacon
    - Radius of circle is $$min(dist_b, 10)$$, where $$dist_b$$ is the distance to the beacon in meters
- If there's multiple beacons $$B = \{b_1, b_2, \dots, b_k \}$$ in range:
    - Calculate simple centroid lat/lng: $$lat = \frac{\sum_{b \in B} b_{lat}}{k}$$, $$lng = \frac{\sum_{b \in B} b_{lng}}{k}$$
    - Let radius $$r_{max}$$ equal to the distance of the farthest beacon
    - Draw circle with center in the centroid $$c$$ and radius $$r_{max}$$

Images of the two visualizations:

<div class="mdl-grid">
	<div class="mdl-cell mdl-cell--6-col">
		<img src="/assets/images/emplate-wayfind/pins-with-opacity.png" alt="Pins of nearby beacons">
		<p class="img-text">Pins of beacons that the phone picks up</p>
	</div>
    <div class="mdl-cell mdl-cell--6-col">
		<img src="/assets/images/emplate-wayfind/circle-with-nearest.png" alt="Circle based on nearest beacons">
		<p class="img-text">Using the nearest beacon to draw a circle around your location</p>
	</div>
</div>

With this out of the way - here's a screen recording of me walking along the outermost corridors of Storcenter Nord.

1. The blue circle is Google Maps using all the sensors of the phone to locate me.
2. The orange is my prototype, only using bluetooth.

<iframe width="800" height="480" src="https://www.youtube-nocookie.com/embed/98t9eyD2JPE?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

If you look closely in the video, my prototype had issues in some locations of the mall with a low density of beacons (left corridor), but Google had multiple instances of showing me ghost-walking through walls, and guessing I'm in a different corridor at times.

I'm feeling confident that the setup can be tweaked to yield better performance just using bluetooth, and obviously get even more accurate location if we use more sensors.