---
layout: post
title: Atlas Obscura Roadtrip Planner
date: '2018-06-01T12:01:39-05:00'
tags:
- maps
- roadtrip
- scraper
---

Earlier this summer, my girlfriend and I visited southern California in an [Escape campervan](http://escapecampervans.com/). It was an amazing experience and it was the first time we were going into our vacation without planning anything.

What we did, however, is scan [Atlas Obscura](https://www.atlasobscura.com/) (AO) for cool things to visit and photograph. It's a super useful and fun website to find offbeat, quirky, less touristy locations. For example, we visited a mailbox in the middle of desert, a beach filled with sculptures made of junk and a waterfall in the shape of a heart, just to name a few. 

[PHOTO]

Unfortunately, AO's website isn't really made to plan things ahead and prepare your trip. You can select locations and place them in a list that can also be viewed on a map, but the UI is very limited in terms of functionalities.

While gazing at the beautiful scenery California offered us, I started thinking about a better way to do this. What I was looking for was basically Google Maps Directions Service mixed with Atlas Obscura's content. Thus, I created the [Atlas Obscura Roadtrip Planner](https://atlas-obscura-roadtrip-planner.herokuapp.com/).

# Directions

Getting the directions is pretty easy using the Google Maps API. There are limitations as to how many waypoints you can add to your trip, but in most roadtrips it shouldn't be an issue.

```javascript
	let directionsService = new google.maps.DirectionsService();
	let directionsRenderer = new google.maps.DirectionsRenderer();
	directionsRenderer.setMap(map);

	directionsService.route(options, (result, status) => {
		if (status === 'OK') {
			directionsRenderer.setDirections(result);
		} else {
			alert(`Unable to determine route for.`);
		}
	});
```

# Buffering

I don't necessarily want locations that are gonna hit my route exactly so I'm going to need to add a buffer to that same route (let's say, 5km around the route) and create a polygon out of that. That same polygon is going to be used to find out which AO locations are within reach.

To create the actual polygon, I turned to the awesome turf library:

CODE

# Getting the data

At first, I thought I would be able to request locations through webservices exposed by Atlas Obscura (AO). Unfortunately, there doesn't seem to a lot going on in terms of services. There's one JSON API endpoint to request details for a particular place, but not to get subsets of data based on bounds or location.

Instead, there's an AO map page containing a giant JavaScript array with all locations (IDs and lat/lon values). With a simple request and some regex fu, it's pretty easy to extract the whole dataset and start getting to work.

CODE

Since I'm aiming at strictly building a webapp, I'll be needing some cross-origin resource sharing (CORS) circumvention. There are a handful of solutions out there, like [cors-anywhere](https://github.com/Rob--W/cors-anywhere) and [corsproxy/crossorigin.me](https://corsproxy.github.io/).

With the polygon and data in hand, I can use a simple contains method in Google Maps SDK to find out which locations are on my route:

CODE

# Conclusion 

Voilà! The app is now [up and running]() and we can plan our next roadtrip. There are still a couple of things I'd like to introduce, such as mobile support, waypoints re-ordering and locations routing. So I might revisit this project soon enough