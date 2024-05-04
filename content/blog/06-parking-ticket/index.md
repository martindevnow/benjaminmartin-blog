---
title: "Poor Input Validation and Sanitization Led to a Parking Ticket"
date: "2024-05-03T00:00:01.000Z"
description: When paying for parking in BC with a rental car that had AB plates, I entered the license plate number 'incorrectly' which led to me getting a parking ticket"
---

Web, and more generally software, development comes in many many shapes and forms. But regardless of what type of software you develop, you should build your UI to target the lowest common denominator. Basically, assume your user is an idiot. This is a story about a time when I was that idiot.

Several years ago, I visited Vancouver with family from Ontario and had a frustrating experience with a parking app. We had rented a car that had Alberta license plates, and I had no idea that this would cause an issue when it came time to pay for parking with my cell phone.

As we arrived at Stanley Park and tried to pay for parking through the Vancouver (or maybe BC) sponsored app, I entered the license plate number. It may not be common knowledge, but AB license plates are hyphenated. So, when registering my vehicle in the parking app, I including the hyphen in the license plate. I thought nothing more of it becauseno error messages were displayed, and my input was accepted.

In contrast, I've dealt with apps that get upset if you don't put a space in your postal code (in Canada, we use the format `A1A 1A1`). Anyways, we went on to enjoy our day at the aquarium. However, when we returned to the car, we were surprised to find a parking ticket on the windshield patiently waiting for us.

Obviously, I was confused and frustrated as I had paid for parking through the app, and I had email receipts to prove it. Luckily, there was a website I could visit to pay or refute the ticket, so I visited it. But when I tried to refute the ticket online, and I entered my license plate number, I once again used the hyphen in the license plate. This time, the website gave me an error. Not a validation error, mind you.. it was basically a `404`. I figured I ought to *try* it without the hyphen, and low and behold, it found my ticket. At this point, I came to the realization that the hyphen in my license plate number had caused the issue.

With this new found information in hand, I contacted the parking enforcement agency to provide my payment records and explain the situation. While I was lucky to receive a pardon and have the ticket cancelled, I was scolded for my mistake and was warned that this was an exception... The whole ordeal left a very sour taste in my mouth. Much like the flavour of today's sponsor... just kidding..

So, what can we learn from this situation...

Sanitize your inputs. Especially when taking input that is of a known shape or could easily map to a RegEx function. Only keep the relevant bits and ignore the "styling". Much like how `12125551234` and `1 (212) 555-1234` are functionally equivalent.

Use input validation both on the client side and server side. While, yes, this is obviously good practice to both a) give your customers fast feedback by incorporating input validation in the UI, it also b) protects against bad-actors by guarding your server-side APIs with input validation as well. You can then also force strict contracts on your APIs since your average user won't be interfacing directly to your REST endpoints. Then you can sanitize the string in the UI before sending the ajax request.

Moreover, good unit testing, API testing and QA processes could have helped prevent this issue.

It's unfortunate that this oversight led to a negative experience for me and my family. This situation also highlights the impact that poor UI can have on the User Experience. While I won't make that same specific mistake again, I bet someone else eventually will. That is, until they fix this bug. But I guess that's more parking ticket dollars for the city of Vancouver... 

