ThreeCircles: step by step tutorial
--------------------------
This github repository holds all the step by step tutorial to illustrate how to use 
[3musket33rs](http://3musket33rs.github.com/) html5-mobile-scaffolding Grails plugin. 

Do you want to see step by step how to build a single page web app? This workshop was 
presented at [ConFESS](https://2013.con-fess.com/sessions/-/details/97/Hybrid-Mobile-App-in-Minutes-Not-Days) and [Gr8Conf US] (http://gr8conf.us/Presentations/Mobile-App-in-minutes--not-day)
with the following abstract:

***Hybrid Mobile App in minutes not days***

*Can you build your own version of Foursquare in minutes? Yes, you can.*
*To survive offline your presentation logic should reside on the client. Using HTML5 power and jQuery mobile responsive UI your web app becomes Mobile.*
*Ready to take the mobile challenges: geolocation, offline caching, data synchronization, server side event push, camera and packaging as Hybrid using PhoneGap.*
*At the end of the session, you will have a clone of Foursquare on your mobile, with a REST backend in Grails running on the cloud. All that with one goal in mind: have fun!* 

You will find [associated presentation](http://corinnekrych.github.com/Gr8ConfUSMobile) in github 
find source code https://github.com/corinnekrych/Gr8ConfUSMobile

## Setup

### Virtual box
- Install the virtual box: 
 * in the USB drive you will find for your operating system, virtual box and 7z intallation packages. Install them!
 * copy ubuntu.vdi.7z into a temporary directory
 * unpack it with 7z
- Open virtual box: 
- click on new icon on the upper tool bar
  * pick a name,
  * choose the type __linux__, version __ubuntu__, press continue
  * choose at least 1Gb for memory size, press continue
  * check __use an existing virtual hard drive file__, select __VDI__ pick the directory where you unpacked ubuntu.vdi, press finish

Once created, click on start, the virtual is started. Username / password is gr8conf / gr8conf.
Open a terminal, in your home directory
```java
cd work
```
In this directory there 3 git hub repos as listed below.
### (Optional) GitHub Repos
If you dont have the gr8conf USB key, fork or clone this repo but also the 3musket33rs plugins
```java
git clone https://github.com/3musket33rs/html5-mobile-scaffolding
git clone https://github.com/3musket33rs/ThreeCircles.git
git clone https://github.com/3musket33rs/BrowserPush.git
```
You will need also grails 2.2.3, jdk1.7, cordova 2.9.0, Android sdk and emulator, a modern browser (no IE6!)

### Working with tutorial

The tutorial is divided into 10 steps. For each steps, we splitted it into 4 sections:
- Get source code: where you fetch stepXX_todo
- We've DONE it for you: here you have nothing to do yourself, just read what have being setup for you. 
This is to speed up the tutorial.
- Your TODO: this is where you do some work. Each todo is numbered so you can easily search for it in the source code.
- Get source code: the solution to the TODO can be found in this branch stepXX_done.

### Working with branches
The step by step tutorial works with git branches. For each step you will find a branch **stepXX_todo** and **stepXX_done**
Here will be the list of git commands you will need to know

- Configure your env with your github account

```java
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

- Commit your changes

```java
git checkout stepXX_todo // To enter in the stepXX_todo branch
git branch               // to check in which branch you are
git status               // to know which files you modified in the current branch
git add -A               // to add files to be committed
git commit -m "Some usefull comments" //To commit locally your changes
git pull                 // to fetch the latest changes from the remote repo
git push                 // to send your committed changes to the remote repo if you did a fork
```

## Step1: Scaffolding

### 1. Get source code from repo
```java
git checkout step1_todo
```
### 2. We've DONE it for you
#### 2.1 Create app
In this branch, we have created a Grails app ThreeCircles with this command
```java
grails create-app ThreeCircles
```

#### 2.2 Configure app
Now let's start looking at the configuration added

In BuildConfig.groovy
```java
  grails.plugin.location."html5-mobile-scaffolding" = "../html5-mobile-scaffolding"
```
to get the latest from source code.

in plugins section
```java
    plugins {
        runtime ":hibernate:$grailsVersion"
        runtime ":jquery:1.9.1"
        build ":tomcat:$grailsVersion"
        compile ":webxml:1.4.1"
    }
```
in resolution **legacyResolve** has been changed
```java
    grails.project.dependency.resolution = {    
    ....
        legacyResolve true
    ...
    }
```
to fetch Platform Core plugins.

in UrlMappings.groovy
line removed
```java
    "/"(view:"/index")
```

#### 2.3 Domain classes
We've added the following domain classes. Look at the class diagram
![class diagram](https://github.com/fabricematrat/ThreeCircles/raw/master/imagesTutorial/classDiagram.png "class diagram")

### 3. Your TODO
This is where you start doing some work!

#### TODO 1: Generate HTML5 scaffolding
for both controller and views using 3musketeers plugin script

```java
grails html-generate-all threecircles.User
grails html-generate-all threecircles.Place
grails html-generate-all threecircles.Comment
grails html-generate-all threecircles.Checkin
```
#### TODO 2: Run the app
```java
grails run-app
```

#### TODO 3: Go to URL
```java
http://localhost:8080/ThreeCircles/index.html?_debugResources=y
```
Note: adding _debugResources=y to reload JavaScript/CSS/HTML updates for resources plugins

Add your favorites places and lokk at geolocation.

### 4. Get source code from repo
Before you get the solution push your changes
```java
git status                   // to check the list of files changed or added
git add -A                   // to accept all changes
git commit -m "your changes" // to commit to local repo
git push                     // to push to remote repo if you did fork
```
and if you want to check the solution
```java
git checkout step1_done
```
## Step2: Boostrap
### 1. Get source code from repo
```java
git checkout step2_todo
```

### 2. We've DONE it for you
Search for TODO in grails-app/conf/Bootstrap.groovy

### 3. Your TODO 

#### 3.1 In BootStrap.groovy
- add several users
- add some places with coordinate. Choose your favorite places like:

```java
        Place minneapolis = new Place(name: "Minneapolis Convention Center",
                latitude: 44.96930003941189,
                longitude: -93.27280524253842,
                address:  "1301 2nd avenue S, MN55403" )
        minneapolis.save()
```
- add a checkin at Gr8Conf!

#### 3.2 Run the app
```java
grails run-app
```
- Test the application
- Try the offline mode (best support is in Firefox File-> Work Offline)
- Add/Delete Checkin
- Get back online (uncheck in Firefox File-> Work Offline)

### 4. Get source code from repo
```java
git checkout step2_done
```

## Step3: Render timeline with mock picture

### 1. Get source code from repo
```java
git checkout step3_todo
```
### 2. We've DONE it for you

you will get new folders and files containing mock screen for timeline
- added new cool CSS in web-app/css/my.css
- and images in web-app/img/
- delete index.html, this default page listing all controller available in Grails. 
- rename checkin-index.html into index.html. Checkin will become our main view with a timeline of all checkins
- in index.html, section with id **section-list-checkin** revisit footer 

### 3. Your TODO 
Search for TODO in the project

#### TODO 1: Transform your index.html with css
- in index.html (search "TODO header"), in section with id **section-list-checkin** add cool header using jQuery Mobile

#### TODO 2: Display dynamic content
The js file **web-app/js/threecircles/checkin-view.js** contains the JavaScript associated with your view. 
Let's make the content dynamic!
In index.html (search "TODO render timeline"):

1. remove hard coded string'Gr8Conf US in Minneapolis' by dynamic value coming from element
To help you know what JSON is returned by Controller server side, put a break point in your browser in this method and inspect element.
2. remove hard coded value for 'Corinne Krych' by value coming from element etc...
Leave harcoded place holder for pictures.

### 4. Get source code from repo
```java
git checkout step3_done
```

## Step4: Get timeline with time information

### 1. Get source code from repo
```java
git checkout step4_todo
```
### 2. We've DONE it for you
You will get a new file timeline.js.

### 3. Your TODO
- go to timeline.js
Note 3musket33rs JS coding à la Crockford (function first!).
Add a method which takes a Date as long and returns information like:
*just now* (when under 10mins), *11 min ago*, *2h23 min*, *2 days ago*, *3 months ago* and we don't care when it's over one year.
- go to checkin-view.js (search for //TODO) add call to newly created method to add time information.
- go to index.html to include new js file

### 4. Get source code from repo
```java
git checkout step4_done
```

## Step5: Google places

### 1. Get source code from repo
```java
git checkout step5_todo
```
### 2. We've DONE it for you
- you will get a new file geolocation.js that you will complete.
- in index.html, google API  and geolocation.js has been included
- in index.html, section with id "section-show-checkin" has been refactored to apply CSS and match our use case. 
- in checkin-view.js, we initialized our maps with
- in geolocation.js, a google map is created from canvas from canvas id
Using Google API: [google.maps.Map](https://developers.google.com/maps/documentation/javascript/reference#Map)

```java
    $("#section-show-checkin").on( "pageshow", function (event) {
        geolocationSearch.showMapWithPlaces('map_canvas2', "list-place", storeLatLng);
    });
```
### 3. Your TODO
In geolocation.js, seach "TODO search places". The goal of this step is
to make you discover useful Google services when doing feolocation stuff.
Once navigator got our current position with HTML5 **navigator.geolocation**, use google places API
#### 3.1 TODO 1: initialise google places service
See API documentation
Use Google places API: [google.maps.places](https://developers.google.com/maps/documentation/javascript/reference#PlacesService)
#### 3.2 TODO 2: In PlacesService find the places close by with all details
#### 3.3 TODO 3: In search callback method, calculate the distance between you current
location and the point of interest
Use Google geometry API: [google.maps.geometry.spherical](https://developers.google.com/maps/documentation/javascript/reference#spherical)
#### 3.4 TODO 4: Create a marker and add it to the map
Use Google Marker API: [google.maps.Marker](https://developers.google.com/maps/documentation/javascript/reference#Marker)

Use Google position API: [google.maps.LatLng](https://developers.google.com/maps/documentation/javascript/reference#LatLng)

### 4. Get source code from repo

```java
git checkout step5_done
```
## Step6: Checkin!

### 1. Get source code from repo
```java
git checkout step6_todo
```
### 2. We've DONE it for you
- In index.html, section with id **checkin** has been refactored to apply CSS and match our use case
- In checkin-view.js, we initialize on pageshow jqm event our third map **map_canvas3** with

```java
    $("#checkin").on( "pageshow", function (event) {
        geolocationCheckin.showMap('map_canvas3', that.selectedPlace);
    });
```
- In checkin-view.js, **addAndSort** method added to render timeline with latest checkin first.
- In geolocation.js, use [google info window](https://developers.google.com/maps/documentation/javascript/reference#InfoWindow) to render bubble.

### 3. Your TODO
#### 3.1 TODO 1: Add behaviour when click on checkin button
In checkin-view.js, search TODO 1
- format the object before sending

```java
            {
               checkin: "{
                  description: description,
                  'owner.id': "1",
                   place: placeObj,
                  when: new Date().getTime()
               }"
           }
```

#### 3.2 TODO 2: Save place server side
In CheckinController.groovy, search TODO 2
Once a place is found with Google Places, save it to ThreeCircles database.
Look at **event** method that triggers the event push (we'll use event push next step on view)

#### 3.2 TODO 3: Visualize data in time line
On created, in checkin-view.js, deal with event push. 

Let's test event push. To simulate 2 users open 2 different browsers (Chrome and Firefox for example, it has to be 2 different instance of browsers).

- In Chrome, click on "check in" button on footer. 
- Same in Firefox, click on "check in" button.
- in chrome select a place, add a description and checkin
- notice how Firefox get notified

Event push (Grails plugin using Atmosphere framework) is doing broadcast to all browsers.  
3musket33rs PushManager is dealing with excluding "myself".

In order to know in your code if you're the one triggering 
created callback you can user the NOTIFIED tag. NOTIFIED boolean is set true when you are notidied of somebody else event.
In **that.model.createdItem** callback change page only when needed.

### 4. Get source code from repo
```java
git checkout step6_done
```

## Step7: Let's take a picture

### 1. Get source code from repo
```java
git checkout step7_todo
```
### 2. We've DONE it for you

### 3. Your TODO
#### 3.1 TODO 1: Add a new attribute in domain class
In Checkin.groovy, by convention every attribute of type **byte[]** is considerered as a photo. 
Create one field called photo
No need to re-generate scaffolded view: be carefull not to loose all your work on checkin view!

#### 3.2 TODO 2: Photo should be optional. 
See how to add to define 
[constraints](http://grails.org/doc/latest/ref/Constraints/Usage.html) in Grails.
Photo should have a maximun size of 20Mb

#### 3.3 TODO 3: add input for photo
In geolocation.js, in the bubble window, add an input of type **file** with id **input-checkin-photo**

#### 3.4 TODO 4: take picture polyfill
In geolocation.js, use 3musketeers plugin camera service in grails.mobile.camera to take the picture and display it.

#### 3.5 TODO 5: Retrieve photo from input
In checkin-view.js, on **checkin-submit** uncomment line.

#### 3.6 TODO 6: Display picture on timeline
In checkin-view.js, modify **createListItemCustom** to display picture if present

### 4. Get source code from repo
```java
git checkout step7_done
```

## Step8: Put all together
This step ** does not ** have a TO DO section.

You can rest a bit ;-)

### 1. Get source code from repo
```java
git checkout step8_done
```
### 2. We've DONE it for you

Here is what was done for you:

- in checkin-view.js, generated code has been cleaned to leave only what's needed
- place-index.html & user-index.html has been merge in a single page index.html
- place-view.js & user-view.js has been cleaned. 

### 3. Your TODO
Nothing! just test it to see where we are...

## Step9: Spring Security for login

### 1. Get source code from repo
```java
git checkout step9_todo
```

### 2. We've DONE it for you
You will get:
- in BuildConfig.groovy, Spring Security dependency was added
- in **index.html** a new section with id **login-page** has been added for the login form.
- in **checkin-view.js**, login\logout methods and callbacks have been implemented.
- **checkin-model.js** and **checkin-controller.js** new files. If you want to know more on those two files read note below.

**NOTE: ** 3musket33rs includes a very easy custom MCV in JavaScript. As we've seen ealier this MCV catters for the default CRUD operations.
Most of the time those CRUD operations would be enough for your need. Now that we want to add a new operation to login. We need to extend Controller to do our cutom ajax call. If we want to add data to the model (like let's say the firstname of the user logged)
we need to extend Model.

If you run your app in step9_todo, you get a new login page but on login, you bump into 500. Your turn to fix that...
### 3. Your TODO
#### TODO 1: Generate User and UserRole
run 
```java
grails s2-quickstart threecircles User Role
```
when prompted to overwrite User, answer yes, but once User is generated add back those fields:
```java
 String firstname
 String lastname
 static hasMany = [friends:User]
```
See [Spring Security plugin documentation page](http://grails.org/plugin/spring-security-core) for more details.

#### TODO 2: Adding @Secured
In CheckinController.groovy, 
- add annotation at class level with IS_AUTHENTICATED_REMEMBERED rule. 
- inject springsecurity service
See [Peter simplified spring source with Grails blog post] (http://blog.springsource.com/2010/08/11/simplified-spring-security-with-grails/) for more details.

#### TODO 3: Only my friends checkins in my timeline
In CheckingController.groovy,
- retrieved user logged
- find all checkins for me
- find all checkins of my friends
- send back JSON with JsonBuilder

#### TODO 4: Boostrap revisited
In Boostrap.groovy, register yourself with you name and password and add your friends too.

### 4. Get source code from repo
```java
git checkout step9_done
```

## Step10: Apache Cordova

git clone https://github.com/3musket33rs/BrowserPush.git

### 1. Get source code from repo
```java
git checkout step10_done
```
### 2. Your TODO
#### TODO 1: create cordova project
```java
grails run-app
cordova create ThreeCircles
cd ThreeCircles
```
#### TODO 2: Add android platform

```java
cordova platform add android
```

#### TODO 3: Add ThreeCircles JS
```java
cp -r ../web-app/* www
```

#### TODO 4: use 3musket33rs BrowserPush cordova plugin
```java
cordova plugin add ../../BrowserPush
cp plugins/org.threemusketeers.cordova.plugin.browserpush/www/browserpush.js www/
```

#### TODO 5: Android does not understand localhost!
```
subl www/js/threecircles/configuration-bootstrap.js
```

change for baseURL: "http://10.0.2.2:8080/ThreeCircles/

#### TODO 6: Build your project anf launch it!
```java
cordova build
cordova emulate
```
To see Android logs
```java
adb logcat
```

#### TODO 7: Emulator and geolocation
See [Android Emulator section Geo] (http://developer.android.com/tools/devices/emulator.html). 
To emulate brwoser geolocation using the emulator control console:
```java
telnet localhost 5554

geo fix 2.16 41.38
```

```
adb -d install bin/ThreeCircles-debug.apk
```

## Step: Now Have FUN !!

![3musket33rs MVC](https://github.com/fabricematrat/ThreeCircles/raw/master/imagesTutorial/final_app.png "3musket33rs MVC")
