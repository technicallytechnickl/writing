---
title: Building a Company on Free and Open Source Software
layout: post
---

As a former co-founder and a technical lead at multiple early stage startups, I have built tech stacks from scratch more than once and across different eras of technologies. In this post I will share some of my experiences and lessons learned. I will try to keep this post agnostic as far as a hardware startup vs. a software startup as a lot of the lessons learned apply to both.  I'll use the term *maker* to refer to the technical team members.

## Starting Up
The starting up part of a startup is often a hectic jumble of learning and doing.  It's also a time of poverty, at least for the company, if not the founders as well. Therefore decision are (or should be) made based on how little money it will take, and how much flexibility the decision maintains. Cash is oxygen for a startup, at least so I've [heard](https://pitchbook.com/profiles/company/62659-36#overview).

As an example of retaining cash and flexibility, consider the work environment of the startup.  Working from a couch is basically free, and doesn't tie you down to a lease.  A co-working space has a bit more professional appearance and gives a place for meetings.  In return, it costs a bit more than the couch, but does maintain some flexibility as it is pay as you go. For maximum professional appearance and cross-functional teamwork a dedicated office is ideal.  The downside to that shiny new office is being tied to a multi-year lease and paying for all the extras that go into an office.  Splurging for the shiny solution at the wrong time will absolutely suffocate a startup. 
The same goes for infrastructure and tech stack. Keeping up with the Jones' by jumping on whatever cloud stack is currently trendy may sound cool, but signing up for a million monthly fees with third parties can tie you down both monetarily and technologically. Therefore, sticking with the couch and Free and Open Source Software (FOSS) where possible, especially in the early days, can be a key to staying afloat. 

A long term vision tied to short term plans is also critical to planning out the tech stack of the company. Make shift solutions can cover all requirements in the early days, but a plan to move toward more specialized solutions when necessary will keep the proper trade-offs in mind. 

## What is it you do here?
Sticking with the oxygen metaphor a bit longer, keeping focus on what it is your startup is doing is akin to swimming toward the light.  A deep understanding of what's critical for your company to accomplish and what's flexible is the baseline for making decisions about your tech stack. This baseline will shift rapidly, hence the requirement for flexibility mentioned above.  

In the early days of a startup, there may be only one or two makers on the team.  That means that the amount of in house technical time is at a premium.  Therefore, tech stack solutions should focus on ease of integration and minimization of maintenance.  

An example of this type of selection is handling time series data using InfluxDB$^1$ (cloud hosted) vs. any in house solution or more advanced hosted solution. Getting started in InfluxDB is free and the data structures consist of buckets where basically any structure of time series data can be dumped. Though they have now regressed, previously InfluxDB also included a workable dash-boarding solution and schedule calculations. It was a one stop shop that required practically no maintenance.  This setup has been ideal in many situations I have faced in getting time series data stored and observable in a minimum amount of time. 

However, InfluxDB on the cloud has many shortcomings that may not scale indefinitely with the goals of a new company. In one such situation, we eventually made the move to AWS TimeStream.  This move is a great example of trading ease of integration and maintenance for reliability and functionality. Setting up InfluxDB for a basic data stream is (or was in V2) extremely simple.  Create an account, create a bucket, and start sending.  No security settings, no schema required, and immediate plots of the data. AWS TimeStream on the other hand, is a tiny piece of the AWS behemoth. Security settings for users, connecting to Kinesis and handling the data in that layer, setting processing rules for each stream, pre-configured schema and tables, etc.  In the early days all of that is infrastructure that takes away from time creating critical features, but there will be some inflection point where characteristics such as security, capability to scale, and data security start to outweigh ease of configuration. 

The key in all of this to the tech stack is to constantly monitor your business requirements, and be ready to adapt your stack as you go.  The worst case is when you fail to update your stack, and a critical failure occurs that shouldn't happen to a company with that level maturity. 

## When is it time to spend?
That brings us to identifying that inflection point where stack upgrades are necessary.  
Some obvious inflection points:
-A critical and embarrassing failure has occurred.
-You get your first paying customer. 
-You're required to get a certification or comply is specific regulations like SOCs, FDA 5XX, ISOXX, etc.

Some less obvious inflection points:
-Some piece of the stack is preventing implementation of critical features
-Support begins to decline for a critical piece of the stack
-Some piece of the stack becomes a roadblock as the team grows
-An upgrade elsewhere in the stack has impacted another piece of the stack in a objective way
-Licensing changes 

Not reasons to upgrade your stack:
-A new cool technology is available
-The "other guys" are doing it
-A manager thinks you should
-You're embarrassed to tell other professionals what tools you're using


## An example
This is an example starting stack that works for an industrial scale IoT based company:
-NodeRed
-Ubuntu
-InfluxDB (I'd look for a replacement here)
-JavaScript/Svelte
-Mosquitto/MQTT

This stack is sufficient to scale to very large systems with "pretty good" reliability. 
NodeRed is a surprisingly robust tool for IoT and SCADA applications.  The biggest downside I've experienced is in working with large teams.  Configuration management works, but flows are based on a single JSON file.  This file tends to change lots of unimportant values such as locations of nodes.  That means it's hard to track down critical changes, and there is no good visual diff available.  
Ubuntu is obviously sufficient for industrial scale. 
InfluxDB worked for us until the company made poor technical and business decisions that we couldn't live with.  The tool itself was still holding up well to our use case though. 
JavaScript/Svelte has no obvious limit. 
We actually "downgraded" from XXX to Mosquitto for our messaging layer across our sites. Mosquitto is more than sufficient for resilience and reliability requirements while being free and simple to configure. 






$^1$ I may write a separate post about InfluxDB, but I can no longer recommend the cloud hosted version as a solution.  Their lack of focus on data security creates an untenable risk for any mission critical data stored on their service.  