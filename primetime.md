---
layout: default
title: {{ site.name }}
---

# <a name="primetime" class="anchor">Adobe PrimeTime</a>

We.Retail ATV can use the Adobe Primetime player for playing HLS streams. The Primetime player does not support TVML but instead you can push a native view onto the screen which has the primetime player embedded in it. 

For We.Retail any lockup which has the ptvideo attribute specified as a property on the tag will use the primetime player to play the video. The ptvideo tag should contain a link to an HLS stream. Below you will see an example of the tag that is used to play the biking promo video in We.Retail ATV.

<pre><code>&lt;buttonlockup ptvideo="http://adobetv-vh.akamaihd.net/i/adobetv2/_images/avp/vr/4c1fbc20-2c90-47be-9ea3-741347e7c40a/7e566a40-3e57-4823-b513-9bb35c3c70da/be5c4c3a-3cea-47d9-9c03-bcde4cb94077_20160407032410.1280x720at2400_h264.mp4/master.m3u8"&gt;
	&lt;badge src="resource://button-play" class="whiteButton"&gt;
		&lt;title>Video&lt;/title&gt;
	&lt;/badge&gt;
&lt;/buttonlockup&gt;
</code></pre>

# <a name="setup" class="anchor">Setup</a>

Currently adding video's is only supported on the catalog pages. A video can be added by updating the catalog properties tab of the page properties. In the future we plan on adding a new Video Shelf component which will allow more options for embedding videos.

![Primetime Configuration]({{site.baseurl}}/images/primetimeConfiguration.png)

# <a name="how" class="anchor">How it works?</a>

When the application launches the AppDelegate will register a method in TVJS that will facilitate playing a video using Primetime. 
<pre><code>//this creates a function in the javascript context called "pushVideoView".
//calling pushVideoView(url) in javascript will call the block we created above.
evaluation.setObject(unsafeBitCast(pushPrimetimeVideoView, AnyObject.self), forKeyedSubscript: "pushPrimetimeVideoView")
}, completion: {(Bool) -> Void in
</code></pre>

When the user clicks the lockup Presenter.js will look to see if the item selected contains the ptvideo tag.

<pre><code>if(ptVideoURL) {
	pushPrimetimeVideoView(ptVideoURL);
}
</code></pre>

If if the ptvideo property is found we call the the native method which will handle pushing the Primetime Player ViewController on the stack.

<pre><code>//this is the block that will be called when javascript calls pushVideoView(url)
let pushPrimetimeVideoView : @convention(block) (String) -> Void = {
	(url : String) -> Void in
                
    let storyboard = UIStoryboard(name: "Storyboard", bundle: nil)
    let vc = storyboard.instantiateViewControllerWithIdentifier("AAAPrimetimePlayerViewController") as? AAAPrimetimePlayerViewController
    vc?.videoURL = url
    self.appController?.navigationController.presentViewController(vc!, animated: true, completion: nil)
    
    //prints the string passed in from javascript
    print(url)
}
</code></pre>