---
# Configuration for the Jekyll template "Just the Docs"
parent: ADRs
nav_order: 2
title: Use specialized Couriers to make outgoing requests to cloud
date: {2024-07-05}
---

# Use specialized Couriers to make outgoing requests to cloud

## Context and Problem Statement
Certain functions of the app are outsourced to cloud services. For example, media submitted by users is not stored in Horizons servers directly, but rather stored in third-party cloud storage. When a user requests certain data, the application must retrieve this information from the cloud.

Should queries outsourced to third-party systems, e.g. image requests, AI recommendation requests, authentication requests, go through a centralized Courier service, or bypass a central authority and go straight to specialized Couriers, or simply be sent directly by the requesting code?  

## Decision Drivers

* Efficiency: Bottlenecks, high request traffic
* Maintainability: In the future, will the addition of more cloud service dependencies become a challenge?
* Code complexity: More code, more complexity generally
* Necessity: Is it needed?
* Security: Is it more secure to have Couriers with permission to send outgoing requests? 

## Considered Options

* Central Courier that routes to specialized Couriers
* No Central Courier, only specialized Couriers
* No Couriers at all, just send request directly from code

## Decision Outcome

Chosen option: "No Central Courier, only specialized Couriers", because it mitigates bottleneck issues arising from larger request volumes and is more maintainable for the future, despite adding some more code complexity. 

### Consequences

* Good, because separate Couriers can handle concurrent requests of different types (media, recommendations, etc.) at once
* Good, because separate Couriers are more maintainable than requests from different parts of the codebase
* Good, because Couriers provide a template for future Couriers designed to relay information from additional cloud services
* Bad, because more code complexity

## Pros and Cons of the Options

### Central Courier that routes to specialized Couriers

* Good?, because having a Central Courier with privileges only it has, that all other parts of the codebase talk to to make outgoing requests may provide more security? 
* Bad, because a Central Courier becomes a bottleneck for the many different types of requests that it needs to route to the correct Couriers
* Bad, because a Central Courier is not really needed and does not provide much functional value

### No Couriers at all, just send request directly from code

* Good, because it is the most straightforward and easy to implement
* Bad, because it is not maintainable in case changes need to be made
* Bad, because it is prone to hard-to-find bugs 

## More Information

This decision should be revisited if it is found that the specialized Couriers need to be refactored or rethought due to even them causing bottlenecks from high request volumes, or if the added complexity is too great while coding/maintaining, or if they are found to be unnecessary.