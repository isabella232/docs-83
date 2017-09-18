---
layout: default
title: {{ site.name }}
---

# <a name="target" class="anchor">Adobe Target</a>
The Adobe Analytics Mobile SDK also supports A/B testing in TVML with the integration of Adobe Target. The Mobile SDK registers a custom tag named ADBTarget which is configured by setting up the mBoxID of the activity for the A/B test. These A/B tests are configured in the <a href="http://mobilemarketing.adobe.com">Analytics Mobile Portal</a> and allow you to set up multiple experiences for an activity. 
Below is an example usage that embeds an A/B test called "bikingAB". If we find an A/B test with the mBoxID "bikingAB" then the content between &lt;ADBTarget&gt; and &lt;/ADBTarget&gt; will be replaced with one of the experiences defined in the A/B test. If nothing is found, then the default content inside the tag will be shown - in this case the title tag.

<pre><code>&lt;ADBTarget mbox="bikingAB"&gt; 
	&lt;title&gt;Target Load fail or Timeout&lt;/title&gt;
&lt;/ADBTarget&gt;
</code></pre>

To make Target integration easier with TVML and AEM we created a component called mBoxShelf which can be added to any parsys and configured with the mBoxId in author mode. 

![Target Config](images/targetConfig.png)

* <b>mBox Id:</b> Id of mBox
* <b>Target Page:</b> Target page that should be presented if the user selects the A/B test (Optional)

## <a name="targetSetup" class="anchor">Target Setup</a>

Since we are using the Adobe Mobile SDK for target integration A/B test must be created in the <a href="https://mobilemarketing.adobe.com/">Mobile Marketing Portal</a>

![Mobile Marketing Portal](images/mobileMarketingPortal.png)

For the bikingAB, we set up two experiences that will be distributed equally across all users (50%). We also specified the successLocation. 
We must embed another mBox component on the page we want to track as a success and use this success mBoxID to configure it.

![Target Setup](images/targetSetup.png)

The experiences themselves as just simply image tags, when the target component loads it will replace the content in the tag with these image tags.

![Target Ad](images/targetAd.png)

**Note: For demo purposes we are linking to an image in DropBox. Alternatively, you should be able to set a relative path to an image in the DAM.

# <a name="targetSuccess" class="anchor">Measuring Success</a>
If the experience contains a success action that directs the user to another page then another mBoxShelf component will need to be added to the target page. The mBoxShelf component will then need to be configured with the mBoxID of the success activity.

**Note, in order for this to work, you will need to create an Activity in the Mobile Marketing portal for the success mBox.