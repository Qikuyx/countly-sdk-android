##What's Countly?
[Countly](http://count.ly) is an innovative, real-time, open source mobile analytics application. 
It collects data from mobile devices, and visualizes this information to analyze mobile application 
usage and end-user behavior. There are two parts of Countly: the server that collects and analyzes data, 
and mobile SDK that sends this data. Both parts are open source with different licensing terms.

This repository includes the SDK for Android.

##Installing Android SDK

Installing Android SDK requires two very easy steps. Countly Android SDK uses OpenUDID (which comes ready with the zip file). First step is about OpenUDID requirement and second step is integrating Countly SDK to your project:

###1. Add Countly SDK to your project

#### Gradle users:
Add Maven Central repository:
<pre class="prettyprint">
repositories {
    mavenCentral()
}
</pre>

Add Countly SDK dependency:
<pre class="prettyprint">
dependencies {
    compile 'ly.count:sdk-android:+'
}
</pre>


#### Maven users:
<pre class="prettyprint">
&lt;dependency&gt;
    &lt;groupId&gt;ly.count&lt;/groupId&gt;
    &lt;artifactId&gt;sdk-android&lt;/artifactId&gt;
    &lt;version&gt;13.10&lt;/version&gt;
&lt;/dependency&gt;
</pre>

#### Eclipse users:
Download [Latest JAR](https://github.com/Countly/countly-sdk-android/releases/latest) and put it into your lib folder.

###2. Add this to your manifest

Add OpenUDID_manager.java and OpenUDID_service.java to your project under Eclipse.

<pre class="prettyprint">
&lt;service android:name=&quot;org.openudid.OpenUDID_service&quot;&gt;
    &lt;intent-filter&gt;
        &lt;action android:name=&quot;org.openudid.GETUDID&quot; /&gt;
    &lt;/intent-filter&gt;
&lt;/service&gt;</pre>

###3. Set up SDK

* Call `Countly.sharedInstance().init(context, "https://YOUR_SERVER", "YOUR_APP_KEY")` in onCreate, which requires your App key and the URL of your Countly server (use `https://cloud.count.ly` for Countly Cloud).
* Call `Countly.sharedInstance().onStart()` in onStart.
* Call `Countly.sharedInstance().onStop()` in onStop.

Additionally, make sure that *INTERNET* permission is set if there's none in your manifest file.

**Note:** Make sure you use App Key (found under Management -> Applications) and not API Key. Entering API Key will not work. 

**Note:** Call init only once during onCreate of main activity. After that, for each onStart and onStop for 
each activity, call Countly onStart and onStop. 

###4. Other

Check Countly Server source code here: 

- [Countly Server (countly-server)](https://github.com/Countly/countly-server)

There are also other Countly SDK repositories below:

- [Countly iOS SDK](https://github.com/Countly/countly-sdk-ios)
- [Countly Android SDK](https://github.com/Countly/countly-sdk-android)
- [Countly Windows Phone SDK](https://github.com/Countly/countly-sdk-windows-phone)
- [Countly Blackberry Webworks SDK](https://github.com/Countly/countly-sdk-blackberry-webworks)
- [Countly Blackberry Cascades SDK](https://github.com/craigmj/countly-sdk-blackberry10-cascades) (Community supported)
- [Countly Mac OS X SDK](https://github.com/mrballoon/countly-sdk-osx) (Community supported)
- [Countly Appcelerator Titanium SDK](https://github.com/euforic/Titanium-Count.ly) (Community supported)
- [Countly Unity3D SDK](https://github.com/Countly/countly-sdk-unity) (Community supported)

##How can I help you with your efforts?
Glad you asked. We need ideas, feedbacks and constructive comments. All your suggestions will be taken care with upmost importance. 

We are on [Twitter](http://twitter.com/gocountly) and [Facebook](http://www.facebook.com/Countly) if you would like to keep up with our fast progress!

For community support page, see [http://support.count.ly](http://support.count.ly "Countly Support").
