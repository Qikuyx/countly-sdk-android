# 奇酷工场统计SDK的安卓版本集成说明

## 前期准备：

- SDK下载地址：到 [https://github.com/Countly/countly-sdk-android]
- 服务器地址：[https://github.com/Qikuyx/countly-sdk-android/tree/master/release]
- 游戏APPKEY： <由奇酷工场分配>

## 集成说明：

### 1、在项目中添加Countly SDK
通过 [https://github.com/Countly/countly-sdk-android/releases/latest] 下载最新的JAR包，添加到lib文件夹中。

### 2、修改manifest及声明权限
在manifest中添加以下代码：
```xml
<service android:name="org.openudid.OpenUDID_service" />
<intent-filter>
<action android:name="org.openudid.GETUDID" />
</intent-filter>
</service>
```

并声明权限：
```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
```

### 3、代码集成

在集成的应用的主Activity中，做如下修改：

（1） 在onCreate方法中调用：
```java
Countly.sharedInstance().init(context, "http://api.qiku.mobi", "YOUR_APP_KEY"，region, server, channel)
```
`YOUR_APP_KEY请替换成由奇酷分配的KEY，region为当前分区，server为当前分服，channel为当前渠道。

（2）在onStart方法中调用：

```java
Countly.sharedInstance().onStart()
```

（3）在onStop方法中调用：

```java
Countly.sharedInstance().onStop()
```

（4）调用以下方法之一上报用户行为：
- ```Countly.sharedInstance().recordEvent(String key)```

  其中key代表事件名；

- ```Countly.sharedInstance().recordEvent(String key, int count)```

  其中key代表事件名，count代表个数或该事件的某一属性，比如购买两个沙漏参数key为”BUY_ITME_5”，count为2；

- ```Countly.sharedInstance().recordEvent(String key, int count, double sum)```

  其中key代表事件名， count代表个数或该事件的某一属性，sum代表该事件的某一属性如售价，比如用户购买了价格为1.50的沙漏两个， 参数key为”BUY_ITME_5”，count为2， sum为1.50；

- ```Countly.sharedInstance().recordEvent(String key, Map<String,String> segmentation, int count)```

  其中key代表事件名，count代表个数或该事件的某一属性，segmentation可用来保存该事件相关的一系列属性，比如用户完成某个任务后获得一些奖励；

- ```Countly.sharedInstance().recordEvent(String key, Map<string,String> segmentation, int count, double sum)```

  其中key代表事件名，count代表个数或该事件的某一整型值属性，sum代表该事件的某一浮点型属性，segmentation可用来保存该事件相关的一系列属性。

## 统计说明：

基础的统计项目包括：

- 注册角色
```java
Countly countly = Countly.sharedInstance();
Map<String,String> segmentation = new HashMap\<String,String\>();
segmentation.put("channel", "Google Play");
segmentation.put("server", "新开一服");
countly.recordEvent("register", segmentation, 1);
```

- 充值
```java
Countly countly = Countly.sharedInstance();
countly.recordEvent("charge", 1, 6); //1为购买次数，6为购买金额
```

- 升级
```java
Countly countly = Countly.sharedInstance();
countly.recordEvent("levelup",1); //1为等级
```


