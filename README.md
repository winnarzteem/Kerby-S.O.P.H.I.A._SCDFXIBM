# Kerby-S.O.P.H.I.A._SCDFXIBM
S.O.P.H.I.A. (Safety Officer Personalised Health Intelligence Assistant) is an real-time monitoring system that analyzes dynamic household living data to evoke a cost-efficient and effective response. It aims to call upon early intervention actions as soon as possible to reduce further risks of the vulnerable population and to ease the operating workload of SCDF officers.

## Contents

1. [Short Description of Problem and Proposed Solution](#short-description)
1. [Demo video](#demo-video)
1. [Solution architecture](#the-architecture)
1. [Long Description of Detailed Solution](#long-description)
1. [Project roadmap](#project-roadmap)
1. [Getting started](#getting-started)
1. [Running the tests](#running-the-tests)
1. [Live demo](#live-demo)
1. [Built with](#built-with)
1. [Authors](#authors)
1. [Acknowledgments](#acknowledgments)

## Short description

### What's the problem? 

Problem Statement Chosen: Emergency Medical Services

A bulk of SCDF's inbound calls are related to the Emergency Medical Services. At a staggering number of 191,468 calls (~98% of Total calls; where Total calls = EMS + Fire Incidents), our team decide to create a solution around EMS to ease SCDF's operating workload. Calls which involved the elderly population attributed to 43.8% of total EMS calls. This is no surprise as Singapore is currently experiencing an upward trending growth in the aging population. A portion of the aging population are "vulnerable populations" (e.g. without a next of kin), which highlights an emergence of higher risk within households.

### How can technology help?

By capturing data of household and homeowner activity, we are able to monitor the personalised baseline patterns during normal times. If there is a divergence from such normality, an investigative procedure will be performed. With a well connected infrastructure, the system is able to find appropriate measures for self-aid resources or to alert Community First Responders (CFRs) to enlist their help. 

Depending on the magnitude of divergence from an established baseline, the system will allocate different level of severities. In non-severe cases, the situation will be highlighted to the relevant parties (e.g. next-of-kin, CFR, social workers). They can then act as an early intervention measure to prevent the escalation of injury/accident risk. In highly severe cases, the system will inform the SCDF or other relevant organisations for immediate attention. 

The aim of this solution is to utlize technology:
1. To analyze the status quo of a given household via data analysis
2. To prevent a high-risk situation by creating opportunities for early intervention as early as possible
3. To remedy different situations with different level of support based on severity

### The idea

In view of the growth in the aging population, it is important that we have to create a safer household for everyone so that their needs are met and they are well supported at all times. This is especially significant in times of crises such as the current COVID-19 pandemic. During our nation's circuit breaker, social interaction is reduced and this poses a huge problem for the aging households without a next-of-kin. In such households, when a high-risk event happens it might already be too late.

Our team proposes S.O.P.H.I.A., a lightweight,

## Demo video

[![Watch the video](https://github.com/Code-and-Response/Liquid-Prep/blob/master/images/IBM-interview-video-image.png)](https://youtu.be/vOgCOoy_Bx0)

## The architecture

![S.O.P.H.I.A. System](solution-architecture.png)

1. Machine Learning is done in IBM Watson Studio (see long description for details)
2. Other Health Organizations and SCDF's APIs are assumed to be available in this solution (see long description for justification)
3. The Analytics Team refer to any team that is authorized to monitor and analyze the user data provided by the Machine Learning Model.
4. The Household IoTs are as the name suggests, they measure the usage of resources. Motion sensors monitors movement in the kitchen. The rationale behind this is to prevent fires from unwatched stoves.

## Long description

[Click here to view detailed explanation](LONGDESCRIPTION.md)

## Project roadmap

![Roadmap](roadmap.jpg)

## Getting started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them

```bash
dnf install wget
wget http://www.example.com/install.sh
bash install.sh
```

### Installing

A step by step series of examples that tell you how to get a development env running

Say what the step will be, for example

```bash
export TOKEN="fffd0923aa667c617a62f5A_fake_token754a2ad06cc9903543f1e85"
export EMAIL="jane@example.com"
dnf install npm
node samplefile.js
Server running at http://127.0.0.1:3000/
```

And repeat

```bash
curl localhost:3000
Thanks for looking at Code-and-Response!
```

End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why, if you were using something like `mocha` for instnance

```bash
npm install mocha --save-dev
vi test/test.js
./node_modules/mocha/bin/mocha
```

### And coding style tests

Explain what these tests test and why, if you chose `eslint` for example

```bash
npm install eslint --save-dev
npx eslint --init
npx eslint sample-file.js
```

## Live demo

You can find a running system to test at [callforcode.mybluemix.net](http://callforcode.mybluemix.net/)

## Built with

* [IBM Cloudant](https://cloud.ibm.com/catalog?search=cloudant#search_results) - The NoSQL database used
* [IBM Cloud Functions](https://cloud.ibm.com/catalog?search=cloud%20functions#search_results) - The compute platform for handing logic
* [IBM API Connect](https://cloud.ibm.com/catalog?search=api%20connect#search_results) - The web framework used
* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds


## Authors

**Billie Thompson** 


## Acknowledgments

* Based on [Billie Thompson's README template](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2).
