---
layout: default
title: {{ site.name }}
---

# <a name="setup" class="anchor">Setup</a>
 
These instructions are intended for users of Mac OS X or other Linux/Unix systems. You will need to have commandline git and Ruby installed (which we will not cover here). Mac OS X comes with git and Ruby installed however you may need a newer version of Ruby (upgrading the system's default Ruby is not recommended). In this case, you can try using [RVM](https://rvm.io/rvm/install) or another Ruby version manager to install a different version of Ruby on your machine.

## <a name="" class="anchor">Cloning the Repository</a>
In terminal, navigate to your code repository directory. In our case, let's call it codeProj. We are going to then clone our documentation template repository into a directory called gh-pages.

```
#Navigate to the directory
cd ~/user/Development/codeProj/
#Add the submodule in the gh-pages directory
git submodule add git@git.corp.adobe.com/pages/aaa/gh-pages-boilerplate.git gh-pages/

git checkout --orphan gh-pages
git commit -m "Initial gh-pages commit"
git push origin gh-pages
git checkout master
git submodule add <the clone url for your repo> build
cd build
git checkout gh-pages
cd ../
git commit -am "Set up gh-pages as a submodule"
```

Next, we initialize the submodule:

```
cd /gh-pages
git init
```

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