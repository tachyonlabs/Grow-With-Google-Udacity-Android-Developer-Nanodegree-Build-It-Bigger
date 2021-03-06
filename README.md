# Build it Bigger

My accepted submission for the fifth project in the "Grow With Google" scholarship Udacity/Google Android 
Developer Nanodegree program. The jokes in the app are all in-jokes or otherwise relevant to our program. 
:-) #GoogleUdacityScholars #GrowWithGoogle #MadeWithUdacity

## Video walkthrough of the free version/flavor

![Video walkthrough](https://github.com/tachyonlabs/Grow-With-Google-Udacity-Android-Developer-Nanodegree-Build-It-Bigger/blob/master/video_walkthrough.gif "Video walkthrough") 

## Notes

To run the project on my phone rather than an emulator, in MainActivity.EndpointsAsyncTask 
I changed setRootUrl to use my laptop's IP address, and in the backend module's build.gradle file 
I added 
```
appengine {
    run {
        host = "0.0.0.0"
        port = 8080
    }
}
```
So comment out the above from the backend build.gradle file if you're running on an emulator (plus 
changing setRootUrl to the emulator localhost IP address 10.0.2.2), or change setRootUrl to 
your own system's IP address if you're using a physical device.

Before running the app you'll also need to follow step 3 of the instructions below to set up a 
local Google Cloud Endpoints server and start the server via the Gradle Projects pane.

## About this project

In this project, you will create an app with multiple flavors that uses
multiple libraries and Google Cloud Endpoints. The finished app will consist
of four modules. A Java library that provides jokes, a Google Cloud Endpoints
(GCE) project that serves those jokes, an Android Library containing an
activity for displaying jokes, and an Android app that fetches jokes from the
GCE module and passes them to the Android Library for display.

## Why this Project

As Android projects grow in complexity, it becomes necessary to customize the
behavior of the Gradle build tool, allowing automation of repetitive tasks.
Particularly, factoring functionality into libraries and creating product
flavors allow for much bigger projects with minimal added complexity.

## What Will I Learn?

You will learn the role of Gradle in building Android Apps and how to use
Gradle to manage apps of increasing complexity. You'll learn to:

* Add free and paid flavors to an app, and set up your build to share code between them
* Factor reusable functionality into a Java library
* Factor reusable Android functionality into an Android library
* Configure a multi project build to compile your libraries and app
* Use the Gradle App Engine plugin to deploy a backend
* Configure an integration test suite that runs against the local App Engine development server

## How Do I Complete this Project?

### Step 0: Starting Point

This is the starting point for the final project, which is provided to you in
the [course repository](https://github.com/udacity/ud867/tree/master/FinalProject). It
contains an activity with a banner ad and a button that purports to tell a
joke, but actually just complains. The banner ad was set up following the
instructions here:

https://developers.google.com/mobile-ads-sdk/docs/admob/android/quick-start

You may need to download the Google Repository from the Extras section of the
Android SDK Manager.

You will also notice a folder called backend in the starter code. 
It will be used in step 3 below, and you do not need to worry about it for now.

When you can build an deploy this starter code to an emulator, you're ready to
move on.

### Step 1: Create a Java library

Your first task is to create a Java library that provides jokes. Create a new
Gradle Java project either using the Android Studio wizard, or by hand. Then
introduce a project dependency between your app and the new Java Library. If
you need review, check out demo 4.01 from the course code.

Make the button display a toast showing a joke retrieved from your Java joke
telling library.

### Step 2: Create an Android Library

Create an Android Library containing an Activity that will display a joke
passed to it as an intent extra. Wire up project dependencies so that the
button can now pass the joke from the Java Library to the Android Library.

For review on how to create an Android library, check out demo 4.03. For a
refresher on intent extras, check out;

http://developer.android.com/guide/components/intents-filters.html

### Step 3: Setup GCE

This next task will be pretty tricky. Instead of pulling jokes directly from
our Java library, we'll set up a Google Cloud Endpoints development server,
and pull our jokes from there. The starter code already includes the GCE module 
in the folder called backend.

Before going ahead you will need to be able to run a local instance of the GCE 
server. In order to do that you will have to install the Cloud SDK:

https://cloud.google.com/sdk/docs/

Once installed, you will need to follow the instructions in the Setup Cloud SDK
section at:

https://cloud.google.com/endpoints/docs/frameworks/java/migrating-android

Note: You do not need to follow the rest of steps in the migration guide, only
the Setup Cloud SDK.

Start or stop your local server by using the gradle tasks as shown in the following
screenshot:

<img src="https://github.com/udacity/ud867/blob/master/FinalProject/GCE-server-gradle-tasks.png" height="500">

Once your local GCE server is started you should see the following at 
[localhost:8080](http://localhost:8080)

<img src="https://raw.githubusercontent.com/GoogleCloudPlatform/gradle-appengine-templates/77e9910911d5412e5efede5fa681ec105a0f02ad/doc/img/devappserver-endpoints.png">

Now you are ready to continue! 

Introduce a project dependency between your Java library 
and your GCE module, and modify the GCE starter code to pull jokes from your Java library. 
Create an AsyncTask to retrieve jokes using the template included int these 
[instructions](https://github.com/GoogleCloudPlatform/gradle-appengine-templates/tree/77e9910911d5412e5efede5fa681ec105a0f02ad/HelloEndpoints#2-connecting-your-android-app-to-the-backend). 
Make the button kick off a task to retrieve a joke, 
then launch the activity from your Android Library to display it.


### Step 4: Add Functional Tests

Add code to test that your Async task successfully retrieves a non-empty
string. For a refresher on setting up Android tests, check out demo 4.09.

### Step 5: Add a Paid Flavor

Add free and paid product flavors to your app. Remove the ad (and any
dependencies you can) from the paid flavor.

## Optional Tasks

For extra practice to make your project stand out, complete the following tasks.

### Add Interstitial Ad

Follow these instructions to add an interstitial ad to the free version.
Display the ad after the user hits the button, but before the joke is shown.

https://developers.google.com/mobile-ads-sdk/docs/admob/android/interstitial

### Add Loading Indicator

Add a loading indicator that is shown while the joke is being retrieved and
disappears when the joke is ready. The following tutorial is a good place to
start:

http://www.tutorialspoint.com/android/android_loading_spinner.htm

### Configure Test Task

To tie it all together, create a Gradle task that:

1. Launches the GCE local development server
2. Runs all tests
3. Shuts the server down again

# Rubric

### Common Project Requirements

* [x] App is written solely in the Java Programming Language
* [x] App utilizes stable release versions of all libraries, Gradle, and Android Studio

### Required Components

* [x] Project contains a Java library for supplying jokes
* [x] Project contains an Android library with an activity that displays jokes passed to it as intent extras.
* [x] Project contains a Google Cloud Endpoints module that supplies jokes from the Java library. Project loads jokes from GCE module via an async task.
* [x] Project contains connected tests to verify that the async task is indeed loading jokes.
* [x] Project contains paid/free flavors. The paid flavor has no ads, and no unnecessary dependencies.
* [x] Ads are required in the free version

### Required Behavior

* [x] App retrieves jokes from Google Cloud Endpoints module and displays them via an Activity from the Android Library.
* [x] App conforms to common standards found in the [Android Nanodegree General Project Guidelines](http://udacity.github.io/android-nanodegree-guidelines/core.html)

### Optional Components

Once you have a functioning project, consider adding more features to test your Gradle and Android skills. Here are a few suggestions:

* [x] Make the free app variant display interstitial ads between the main activity and the joke-displaying activity.
* [x] Have the app display a loading indicator while the joke is being fetched from the server.
* [ ] Write a Gradle task that starts the GCE dev server, runs all the Android tests, and shuts down the dev server.

# Acknowledgments

### Joke credits

Most of the jokes were made up by me or adapted from old jokes that are all over the place, but here's 
where I got/adapted some of the others:

* [https://hackernoon.com/30-jokes-only-programmers-will-get-a901e1cea549](https://hackernoon.com/30-jokes-only-programmers-will-get-a901e1cea549)
* [https://www.facebook.com/programmingjokes/](https://www.facebook.com/programmingjokes/)
* [https://github.com/EugeneKay/git-jokes/blob/lulz/Jokes.txt](https://github.com/EugeneKay/git-jokes/blob/lulz/Jokes.txt)
* [https://www.hongkiat.com/blog/programming-jokes/](https://www.hongkiat.com/blog/programming-jokes/)
