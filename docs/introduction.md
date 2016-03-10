# Introduction

Welcome to the Home☆Star / IOTDB project, a platform for controlling, monitoring and modeling the Internet of Things.

Mentally, think of this being in the same space as:

* HomeKit
* AllJoyn
* Brillo
* Open Interconnect Consortium
* OpenRemote
* The Thing System

Just better.

## Why is it better? 

IOTDB is designed around a couple of simple concepts. 
These two are the most important:

* Things have fundamental similarities that we can described _semantically_. Semantic descriptions allow us to the solve some of the biggest issues of the IoT, including "the basket full of remotes" problem, and the "silo" problem. 
* the Internet of Things is about adding APIs to Things.  Everything inside of IOTDB is built around the "mental model" of APIs: that we manipulate and monitoring Things by manipulating JSON dictionaries.

Or to put it another way, IOTDB provides a Universal Language for Things and Sensors that easily understood by programmers.

## What's the difference between IOTDB and Home☆Star?

* IOTDB is the core Node.JS library and it's concepts
* Home☆Star is the management and web interfaces build on top of IOTDB

## About

This project is:

* Open Source (Apache 2.0 License)
* Node.JS (but provides flexible APIs)
* uses JSON-LD semantic models
* has a strong vocabulary
* has a solid, practice and experience-driven, theory of "how" we model Things
* works with many real Things, with more coming

The core audience of this project (at this time) is developers and hardware enthusiasts. 
It's written in Node.JS and will run on must any hardware that runs on.
It's not ready for your parent's living room - yet.