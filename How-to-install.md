1、	在项目中添加Countly SDK
（1）对于使用Eclipse构建项目的用户
通过https://github.com/Countly/countly-sdk-android/releases/latest下载最新的JAR包，添加到lib文件夹中
（2）对于使用Maven构建项目的用户
添加Countly SDK依赖：
<dependency>
    <groupId>ly.count</groupId>
    <artifactId>sdk-android</artifactId>
    <version>13.10</version>
</dependency>
（3）对于使用Gradle构建项目的用户
添加Maven中央库：
repositories {
    mavenCentral()
}
添加Countly SDK依赖：
dependencies {
    compile 'ly.count:sdk-android:+'
}

2、	修改manifest
在ECLIPSE中将OpenUDID_manager.java和OpenUDID_service.java加入到项目中：
<service android:name="org.openudid.OpenUDID_service">
    <intent-filter>
        <action android:name="org.openudid.GETUDID" />
    </intent-filter>
</service>

3、	代码集成
（1）	在onCreate方法中调用：
Countly.sharedInstance().init(context, "https:// api.qiku.mobi", "YOUR_APP_KEY"，region, server, channel)
YOUR_APP_KEY请替换成由奇酷分配的KEY，region为当前分区，server为当前分服，channel为当前渠道。
（2）	在onStart方法中调用：
Countly.sharedInstance().onStart()
（3）	在onStop方法中调用：
Countly.sharedInstance().onStop()
请确保manifest文件中设置了internet许可。另外，仅仅在main activity的onCreate中调用一次init方法，而之后的每个activity的onStart调用Countly的onStart方法，onStop调用Countly的onStop方法。
