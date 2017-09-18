---
layout: default
title: {{ site.name }}
---

# <a name="auth" class="anchor">Installation and Setup</a>
 
## Install AEM
* Make two directories on your computer, one called author and another called publish.
* Put a copy of the AEM jar and your license file in each of the directories.
* Go into author directory and rename the AEM jar to cq-quickstart-6.2.0.jar to cq5-author-p4502.jar
* Go into publish directory and rename the AEM jar to cq-quickstart-6.2.0.jar to cq5-publish-p4503.jar
* Click on each to get them running
* There will be a browser window will open for both author and publish instances
* Author instance: <a href="http://localhost:4502/">localhost:4502</a>
* Publish instance: <a href="http://localhost:4503/">localhost:4503</a>
* Click both the links above and make sure you login to both (Username: admin Password: admin)

## Install We.Retail commons content
* Download the <a href="https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases">We.Retail source code 0.2.0</a>.
* Unzip we.retail.all-0.2.0.zip
* Go to <a href="http://localhost:4502/crx/packmgr/index.jsp">package manager</a> on author and upload the zip file at we.retail.all-0.2.0/jcr_root/etc/packages/adobe/aem6/we.retail.commons.content-0.2.0.zip.
* Once the package has been uploaded select the "Install" button on the package.
* After the package has been installed open the "More" dropdown and select "Replicate" to push the package to publish.

## Clone the We.Retail ATV repository from git
* Clone the repository at https://git.corp.adobe.com/aaa/we-retail-atv
* Using the autoInstallPackage profile push the application to author
* Do the same on publish using the autoInstallPackagePublish profile

## Apple TV (Simulator)
* Make sure you have XCode installed and launch the Xcode project at we-retail-atv/xcode_shell/we-retail-atv.xcworkspace
* Launch the Apple TV simulator and point the application at http://localhost:4503
* If <a href="authentication.html">device registration</a> is enabled you will need to go to <a href="http://localhost:4503/registration">http://localhost:4503/registration</a>, login and enter the registration code

## Apple TV (On Device)
* Connect the Apple TV device to your computer using a USB-C cable
* You should see the Apple TV under the device options for the scheme
* Click the "Play" button to install the application on the device
* Follow the instructions below to change the externalizer settings on publish so the images will load
* Launch the Apple TV simulator and point the application at http://localhost:4503
* If device registration is enabled you will need to go to http://localhost:4503/registration to login and enter the registration code

## Configure Publish Externalizer
* Find and write down the IP address of your Mac by going to <a href="http://osxdaily.com/2010/11/21/find-ip-address-mac/">this link</a> and follow the steps for "How to Find the IP Address on a Mac"
* Go to <a href="http:localhost:4503/system/console/configMgr">Sling console</a> on publish and configure the Externalizer 
* On this page search for “Externalizer” and look for the "Day CQ Link Externalizer" and click on it or the pencil icon
* In the domains section replace "localhost" with the IP address of your Mac