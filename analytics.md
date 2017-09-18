---
layout: default
title: {{ site.name }}
---

# <a name="analytics" class="anchor">Adobe Analytics Integration</a>
Support for Apple TV and TVML applications is available in the Adobe Analytics Mobile SDK.

## <a name="pageTracking" class="anchor">Page Tracking</a>
To simplify page tracking we created a custom TVML element <ADBTrackView>. This TVML element is backed by a native Swift class <ADBTrackStateElement>. At application startup, this view is registered with the TVElementFactory which allows us to place the "ADBTrackView" tag on any page.

<pre><code>TVElementFactory.registerViewElementClass(ADBTrackStateElement.self, forElementName: "ADBTrackState")</code></pre>

Whenever the ADBTrackState tag is found on a page the TVMLApplicationController will defer rendering back to the native Swift class. The ADBTrackView tag expects a property called "state" which contains the state name which is used for tracking purposes in our analytics suite. All other properties on the ADBTrackView tag will be treated as context data and passed to the analytics engine. Below is an example of the ADBTrackState element being used on a page.

<pre><code>&lt;ADBTrackState state="section" section="Pants"&gt;&lt;/ADBTrackState&gt;</code></pre>

## <a name="actionTracking" class="anchor">Action Tracking</a>
To track actions (or events) we used the Adobe Mobile TVJS API. When an element tagged "action" is selected, an event is fired and Presenter.js listens for these events. The example provided looks for the action "addToCart", if found we also expect the tag to contain a property called productId. The data is then passed to Adobe Analytics the API.

<pre><code>var self = this, 
    ele = event.target, 
    action = ele.getAttribute("action"), 
    productId = ele.getAttribute("productId");

if(action){
    if(action == "addToCart"){
        ADBMobile.trackActionData("scAdd", {'productId':productId});

		var alert = createAlert("Success", productName + " has been added to your shopping cart!");
        alert.addEventListener("select", self.load.bind(self));
        navigationDocument.presentModal(alert);
    }
}
</code></pre>