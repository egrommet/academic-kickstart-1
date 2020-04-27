---
title: Data Police location issues
author: Glyn Mottershead
date: '2020-04-27'
slug: data-police-location-issues
categories:
  - open data
  - Data Journalism
tags:
  - api
  - data.police
  - data journalism
subtitle: ''
summary: ''
authors: []
lastmod: '2020-04-27T07:39:58+01:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---
I've just working on a couple of tutorials using data from [data.police.uk](https://data.police.uk) - the first using the csv download method and the second using an API call using the httr package.

However, you call the data you get back a whole host of information - including the latitude and longitude of the incidents themselves.

Or do you?

Last year, one of my former students Conor Gogarty wrote this story on the GloucestershireLive site following up from a crime map that showed  - ["My search for crime in the Gloucester crime hotspot with no crime"](https://www.gloucestershirelive.co.uk/news/gloucester-news/search-crime-gloucester-crime-hotspot-2553224).

Conor, with his pair of binoculars, goes to investigate what is going on in Tredworth's Bishop's Castle Way.

He found really interesting information including these gems:
> "A total of 41 shoplifting reports were linked to the spot last year. But there are no shops there... How could 41 shoplifting incidents have been reported last year if the nearest stores were a five-minute walk away in Barton Street?"

As any journalist should, Conor gets in touch with the police - a press officer confirms there were no crimes in that area.
>"She said the markers on the map are not the exact locations of offences. They are ‘snap points’ which pull in the reports from nearby spots."

A further check led to this information:
>"Gloucestershire police said this was a question for the Home Office, which oversees the police.uk website. A Home Office spokesman told me inaccuracies can result from “inconsistent geocoding policies”. He said the website makes it clear the data is not always “fully accurate”."

## RTFM
When you read the docs, this is an issue that is highlighted:
> "The latitude and longitude locations of Crime and ASB incidents published on this site always represent the approximate location of a crime — not the exact place that it happened."

That's pretty straightforward, when you think about some offences the location could actually help identify the victim of the incident. So, obfuscation is a really good idea.

The documentation is really interesting when they explain [how the location is anonymised](https://data.police.uk/about/#location-anonymisation).

### This is not the location you are looking for

>*How are crime locations anonymised?*
>We maintain a master list of anonymous map points. Each map point is specifically chosen so that it:
>* Appears over the centre point of a street, above a public place such as a Park or Airport, or above a commercial premise like a Shopping Centre or Nightclub.
>* Has a catchment area which contains at least eight postal addresses or no postal addresses at all.
>* When crime data is uploaded by police forces, the exact location of each crime is compared against this master list to find the nearest map point. The co-ordinates of the actual crime are then replaced with the co-ordinates of the map point. *If the nearest map point is more than 20km away*, the co-ordinates are zeroed out. No other filtering or rules are applied.

>How was the master list of snap points created?
>The snap points list was created in 2012 and based on Ordnance Survey population and housing developments relevant to that year.
In summary, to create the master list of anonymous points, we:
>* Took the centre point of every road in England and Wales from the Ordnance Survey Locator dataset.
>* Augmented these with locally relevant points of interest from the Point X dataset.
>* Subsequently analysed each map point to see how many postal addresses were contained in its catchment area according to the Ordnance Survey Address-Point dataset. Any with between 1 and 7 postal addresses were discarded to protect privacy.
>* The remaining points were provided to police forces for a human assessment. A small number of additions and deletions were made based on their feedback to make the map points more locally relevant.

Ok, so as data journalists it does mean we have to subject the data to scrutiny before publishing crime near x stories. It also calls into question apps that draw on the data for things like home sales.

So, a simple point. Always read the manual for the data - and if you are interested in the data.police.uk site then [this academic paper](https://www.tandfonline.com/doi/full/10.1080/15230406.2014.972456) is worth a read if you are able to get access.
