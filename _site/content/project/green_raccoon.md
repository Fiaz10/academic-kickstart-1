+++
title = "Green Raccoon"
date = 2018-09-18T15:34:34-05:00
draft = false

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["mobile-development", "machine-learning"]

# Project summary to display on homepage.
summary = "A react-native application which takes a picture and tells you if something is recyclable or not. react-native, google-cv-api, snack.expo"

# Optional image to display on homepage.
image_preview = "green_raccoon.png"

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Does the project detail page use source code highlighting?
highlight = true

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
[header]
image = ""
caption = ""

+++

![Application Home Screen](/project/green-raccoon/green_raccoon.png)

_Originally made for EarthxHack 2018. Code available [here](https://github.com/sid-devic/greenraccoon), live in-browser demo available [here](https://snack.expo.io/Bys9hVqnG)._

Recycling is difficult. The rules of recycling can be even more difficult: items with food need to be washed, bottles need to have their caps removed, etc. This project is an attempt to simplify recycling so that (especially) children can learn how to do it properly.

The application has two main parts: 

1. Informing the user through a simple list what is recyclable
2. An embedded camera which takes a picture and determines if the item in the picture is recyclable or not

### Parsing Google's Computer Vision API
The response from Google, at least for the specific api we were toying with, was a list of words that the item in the picture may be. Our simple hueristic to determine if an item is recyclable or not is whether any of the following were a subset of the parsed return:

`var keywords = ["Aerosol", "cans", "completely empty",
"Aluminum", "cans",  
"Beverage", "cans",
"Brochures",
"Cardboard", "cereal", "boxes", "plastic", "lining", "OK",
"Computer", "paper",
"Coupons",
"Egg", "cartons",
"Food", "cans",
"Glass", "bottles", "jars",
"Glass", "cosmetic", "bottles",
"Glass", "unbroken",
"Junk", "mail",
"Laundry", "bottles", "remove", "caps", "lids",
"Ledger", "paper", "drink",
"Magazines",
"Milk", "juice", "cartons",
"Newspaper",
"Paper", "product",
"Paper", "tubes",
"Phone", "books",
"Pizza", "boxes", "clean",
"Plastic",
"Tin", "cans",
"Tissue", "boxes",
"Used", "envelopes",
"Wrapping", "paper"]`

Obviously, this is a very simplistic approach. Suprisingly though, it works with (anecdotally) ~80% accuracy, which is good enough for have 24 hours to code a project. Here is an example of what we return to the user:

![Decision Screen](/project/green-raccoon/no_re.png)

As you can see, we also returned the labels we considered the item in the image to actually be.

All in all, it was a pretty fun experience learning react-native from scratch to having a working product in only 24 hours. It was extremely gratifying to have children come up and love learning about something as mundane as recycling, because of our cute mascott.