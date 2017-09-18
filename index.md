---
layout: default
title: {{ site.name }}
---

# Introduction
This project aims to demonstrate how Adobe Experience Manager (AEM) can be used to create authorable applications for the 4th-generation Apple TV. It includes templates and components that can be rendered as both HTML and TVML, as well as hooks into other Adobe Marketing Cloud products such as Adobe Primetime, Adobe Analytics, and Adobe Target.

# Why is this Awesome?
It opens up a new third-party platform (Apple TV) for creating novel, innovative, immersive application experiences. It pushes the boundaries of Adobe's products by allowing AEM customers to keep up with emerging technologies like the 4th-generation Apple TV.
This pattern allows existing and new AEM customers to re-purpose their AEM content and extend their reach onto the quickly growing Apple TV platform. This approach requires only a few modifications to the AEM module design to include files containing Apple TV compliant views/components with TVML selectors (.tvml).
An experienced AEM developer should be able to get a working demo up and running fairly easily using our repository for reference.

# Sections

* [<b>Background</b>](background.html)  
* [<b>Installation and Setup</b>](demosetup.html) 
* [<b>How Does the Pattern Work?</b>](how.html)  
    * [Client-Server Flow](how.html#client-server)
        * [AEM Server](how.html#aem_server)
        * [Apple TV / TVMLKit](how.html#apple_tv_client)
    * [Application Logic](how.html#app_logic)
    * [Rendering Apple TV Views/Components](how.html#rendering_comps) 
* [<b>Authenticating &amp; Device Provisioning</b>](authentication.html)  
    * [Bootstrapping Process](authentication.html#bootstrapping)
    * [Provided Servlets](authentication.html#servlets)
    * [Registration Page](authentication.html#registrationPage)
* [<b>We.Retail Templates</b>](templates.html) 
	* [Home](templates.html#home)
	* [Catalog](templates.html#catalog)
	* [Section](templates.html#section)
	* [Product](templates.html#product)
	* [Cart](templates.html#cart)
* [<b>We.Retail Components</b>](components.html) 
	* [Carousel](components.html#carousel)
	* [Catalog Shelf](components.html#catalogShelf)
	* [Product Shelf](components.html#productShelf)
	* [Product Grid](components.html#productGrid)
	* [mBox Shelf](components.html#target)
* [<b>Adobe PrimeTime Integration</b>](primetime.html) 
	* [Setup](primetime.html#setup)
	* [How it Works](primetime.html#how)
* [<b>Adobe Analytics Integration</b>](analytics.html) 
	* [Page Tracking](anaytics.html#pageTracking)
	* [Action Tracking](anaytics.html#actionTracking) 
* [<b>Adobe Target Integration</b>](target.html)
	* [Setup](target.html#targetSetup)
	* [Measuring Success](target.html#targetSuccess)

## <a name="future_improvements" class="anchor">Future Improvements</a>

* Add in shopping cart support
* Add shoppable video support
* Better support for video (Video Shelf)