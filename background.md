---
layout: default
title: {{ site.name }}
---

![Alt text](images/atv.png)

# Overview
In late 2015, Apple released the 4th version of the Apple TV. One of the most exciting things about this new device is that Apple has opened up the platform for developers to create apps and distribute them on a new App Store built just for TV experiences. These applications can either be written in native languages such as Objective-C or Swift, or they can be written in a new language called TVML. TVML is similar to HTML in that it is a markup language that can be used in conjunction with JavaScript to build applications.

TVML applications work in a client-server model. The main application is responsible only for loading the application.js file and then hands off most of the presentation and application logic to TVMLKit. The UI &amp; application logic for these client-server applications can live on a server and are not required to be packaged with the application. Apple has created a collection of TVML templates that are used to create applications. TVML templates define what elements can be used and in what order. Each template is designed to display information in a specific way. For example, the loadingTemplate shows a spinner and a quick description of what is happening, while the ratingTemplate shows the rating for a product. While these templates can be very rigid in their ability to be customized there are a few areas where template authoring works and makes sense.

## TVML &amp; AEM

AEM is a world-class platform for creating authorable HTML experiences. Since TVML is similar to HTML, this project demonstrates that the features of AEM translates into the TVML world as well.