---
layout: default
title: {{ site.name }}
---

# <a name="how" class="anchor">How Does the Pattern Work?</a>
 
In this section, we introduce the pattern we followed to allow viewing AEM content on the 4th-generation Apple TV platform. This pattern involves using an Xcode shell application to load a TVMLKit application from an AEM server instance.  After the application (Javascript) logic is loaded we pull in the views which are rendered by AEM.

Here, you can see an overview of the system architecture of a TVMLKit client application and AEM server instance:

![System Architecture]({{site.baseurl}}/images/AEM_flow_diagram_2x.png "System Architecture")

## <a name="client-server" class="anchor">Client-Server Flow</a>
In a typical application, there is a native shell application holding icons and bootstrapping your TVMLKit application. The shell application will start a TVApplicationControllerContext which will point at the URL for your application.js. The application.js file contains your application logic. In our AEM use case we put application.js and other helper js files into an AEM Client-Side Library.

Here, you can see the user-client-server flow for the application:

![Client-Server Flow]({{site.baseurl}}/images/flow_diagram2_2x.png "Client-Server Flow")

User browses installed applications ->
User runs our Shell application ->
Our Shell application loads TVMLKit ->
TVMLKit requests application.js file from AEM server ->
Application.js gets first view from AEM server ->
User views Apple TV TVML view loaded from AEM server ->
User launches a video from AEM application ->
If video is standard video we load a native player (if it's a PrimeTime video we load the PrimeTime native video player view and play video) ->
User quits application ->
Application.js cleans up and stops

### <a name="aem_server" class="anchor">AEM Server</a>
The AEM server contains the TVMLKit javascript core application logic.  The application logic is contained in a client-side library and pulled in on the startup of the Swift XCode application startup.

### <a name="apple_tv_client" class="anchor">Apple TV / TVMLKit</a>
The core application logic controls which views are loaded and from where they are loaded. In our case the views are rendered with AEM and served remotely into the application navigation stack.
We can invalidate the views after they have been loaded by the Apple Tv by either setting the HTTP cache settings to expire after a period or by including some business logic to invalidate the locally cached rendered view.

## <a name="app_logic" class="anchor">Application Logic</a>
For the purposes of demonstration, the application logic resides in the designs directory in a client-side library.

[View the application.js code in the client-side library](https://git.corp.adobe.com/aaa/we-retail-atv/blob/master/aem/ui.apps/src/main/content/jcr_root/etc/designs/we-retail-atv/clientlib-atv/js/application.js)

Here, you can see where the static application.js file is stored on our AEM server inside the ATV clientlib.  This client-side library also includes the helper utilities Presenter.js and ResourceLoader.js:

<figure class="highlight"><pre>.
├── + apps
├── + bin
├── + conf
├── + content
├── etc
|   ├──  + blueprints
|   ├──  + clientcontext
|   ├──  + clientlibs
|   ├──  + cloudservices
|   ├──  + cloudsettings
|   ├──  + commerce
|   ├──  + community
|   ├──  + contentsync
|   ├──  + dam
|   ├──  + dashboards
|   ├──  designs
|   |   ├── we-retail-atv
|   |   |   ├── clientlib-atv
|   |   |   |   ├── js.txt
|   |   |   |   ├── js
<span class="open">|   |   |   |   |   ├── application.js</span>
|   |   |   |   |   ├── Presenter.js
|   |   |   |   |   ├── ResourceLoader.js
</pre></figure>

As stated, the application.js file contains all application logic, this file calls out the first TVML view template to be loaded.

## <a name="views_comps" class="anchor">Rendering AppleTV Views/Components</a>
AEM is generating the required view templates based on the [Apple TV Design Guidelines]( https://developer.apple.com/tvos/human-interface-guidelines/).

The following View Templates are being used in our pattern:

* [stackTemplate](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/StackTemplate.html#//apple_ref/doc/uid/TP40015064-CH21-SW4) (Home Page)
* [showcaseTemplate](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/ShowcaseTemplate.html#//apple_ref/doc/uid/TP40015064-CH27-SW1) (Catalog Page)
* [productBundleTemplate](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/ProductBundleTemplate.html#//apple_ref/doc/uid/TP40015064-CH38-SW1) (Section Page)
* [productTemplate](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/ProductTemplate.html#//apple_ref/doc/uid/TP40015064-CH8-SW4) (Product Page)
* [productTemplate](https://developer.apple.com/library/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/CompilationTemplate.html#//apple_ref/doc/uid/TP40015064-CH36-SW2) (Cart Page)

Below are the HTML/TVML compatible components that were created

* [Carousel](components.html#carousel)
* [Catalog Shelf](components.html#catalog)
* [Product Shelf](components.html#productShelf)
* [Product Grid](components.html#productGrid)
* [mBox Shelf](components.html#target)

## <a name="rendering_comps" class="anchor">Rendering TVML Views/Components</a>
In this use case we need to provide an HTML-based preview of the user interface as well as the TVML rendering of the views while complying to Apple TV Design Guidelines. This means that each AEM component needs a separate TVML rendering as well. This is accomplished using [Sling selectors](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html), in this case we use .tvml as the selector.

When we are done we have an HTML component mocking the appearance and style of the Apple TV view templates, allowing authors to see the content and structure of the application. Each component will support the .tvml selector giving us the Apple TV TVML compliant rendition of the same HTML component. The Apple TV application is only ever served the TVML content.
