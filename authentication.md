---
layout: default
title: {{ site.name }}
---

# <a name="auth" class="anchor">Authenticating and Device Provisioning</a>
 
A common use case for some types of applications is to require the user to register their device before they can view the content in the app - think Netflix or HBO Go. Although this use case wouldn't necessarily apply to We.Retail we have included code in this sample to enable this feature. By default this is disabled but it can be turned on by setting deviceRegistrationRequired to true in /etc/designs/we-retail-atv/clientlib-atv.

![Auth flow]({{site.baseurl}}/images/registrationRequired.png)

## <a name="bootstrapping" class="anchor">Bootstrapping Process</a>
Below is a diagram of the bootrapping process in We.Retail. 

![Auth flow]({{site.baseurl}}/images/AuthFlow.png)

* A request is made for the application configuration using the AtvAppConfigurationServlet. This configuration notifies the application if device registration is required and the default view location.

* If registration is required the application checks to see if the device has been authorized with the server by calling CheckDeviceRegistrationServlet. If it has not been authorized, the CheckDeviceRegistrationServlet will track the device under /var/atv-devices. 

![Device Registration]({{site.baseurl}}/images/atv-devices.png)

* The user will then be shown a screen with a registration code they will need to enter on the website.

![Device Registration]({{site.baseurl}}/images/registrationScreen.png)

* The user will navigate to http://{domain}/registration in a browser, login to their account, and enter the registration code that is displayed on the Apple TV.

![Device Registration]({{site.baseurl}}/images/registrationCodeEntry.png)

* Once the device has been authorized, the entry is moved from /var/atv-device and put under the user's account in /home/users by the RegisterDeviceServlet.

![Device Registration]({{site.baseurl}}/images/authorizedDevice.png)

* The application checks every 5 seconds to see if the device has been authorized, once the CheckDeviceRegistrationServlet returns true the servlet will return the deviceId and devicePasscode. These two values will be used to call the AtvAuthHandler and set the shared session for all future calls.

* The registration code screen will then disappear and the application will request the default view specified by the AtvAppConfigurationServlet at launch.

This diagram shows the communication flow from the Swift shell.  As you can see, all network communications are flowing through our AemJsUtils.  This allows us to setup a session and share that session with all calls made.

![Bootstrap overview]({{site.baseurl}}/images/bootstrapOverview.png)

# <a name="servlets" class="anchor">Provided Servlets</a>

### AtvAppConfigurationServlet
Servlet that loads the configurable properties on an Apple TV JS application and sends those properties back to the shell application to allow it to bootstrap itself.

###RegisterDeviceServlet
Servlet that registers a device based on the passed in registrationCode. When the users visit the registration page and enters their registration token this servlet will find the device associated to the token and move it under the user's profile in /home directory.

###CheckDeviceRegistrationServlet
Servlet that checks if a device has been registered based on the applicationId and deviceId. If the passed in deviceId passed is unknown it will add the device to /var/atv-devices and set its registration status to unregistered.

If the device is found and has been registered the servlet will return the devicePasscode that can be used to authenticate future calls to AEM.

## <a name="registrationPage" class="anchor">Registration Page</a>