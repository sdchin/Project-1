---
# Configuration for the Jekyll template "Just the Docs"
parent: ADRs
nav_order: 1
title: Use cloud-based recommendation system
date: {2024-07-05}
---

# Use cloud-based recommendation system

## Context and Problem Statement
The crux of the app is its ability to recommend new ideas based on a user's stated goals. A recommendation system is used to select the best items out of many items that a user might be interested in.

Should I try to implement a recommendation system on my own server, or should I make use of cloud-based recommendation systems?

## Decision Drivers

* Costs: Server costs, costs of using cloud
* Time: Time spent implementing
* Knowledge: Do I have the prerequisite knowledge to make my own?
* Efficiency: Which one is faster?
* Infrastructure: My one server or the entire cloud?

## Considered Options

* Implement my own recommendation system on my own server
* Use cloud-based recommendation system and send/store the data needed

## Decision Outcome

Chosen option: "Use cloud-based recommendation system and send/store the data needed", because it will be a much more reliable/accurate source of recommendations and save me the time and effort of researching and implementing my own system, with the precaution that I mock it up first and set safety guards before I attempt connecting to the cloud.

### Consequences

* Good, because cloud-based recommendation systems and algorithms have been improved upon over many years
* Good, because cloud-based recommendation systems are built by people much smarter than me
* Good, because cloud infrastructure is much bigger and more powerful than my server
* Bad, because getting data to and back from the cloud is heavily reliant on the network and the cloud service itself
* Bad, because all the important recommendation data is stored on the cloud not in my ownership
* Bad, because searching/training/per hour/etc. prices look scary and I don't want an oopsies

## Pros and Cons of the Options

### Implement my own recommendation system on my own server

* Good, because fewer requests over network
* Good, because more customizable and in my control
* Good, because the data is on my server and not owned by the cloud
* Bad, because I lack the knowledge to make a recommendation system
* Bad, because it would take a lot of time and effort to create a recommendation system that is likely to be bad
* Bad, because it would eat up a lot of resources on my server and likely increase server costs
* Bad, because a bad recommendation system on limited server resources would take more compute time

## More Information

This decision should be revisited if it somehow gets too expensive (it shouldn't because I won't have any users), or if I cannot figure out how to set it up, or if someday the need arises for a more custom bespoke recommendation system.