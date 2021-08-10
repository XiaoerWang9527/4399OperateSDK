
4399运营SDK Android客户端接入说明
======================

## 修改记录

版本号  |   修改日期    |   修改者  |   修改内容
--------|---------------|-----------|-------------------------
v1.0.0  |   2014-07-08  |   张生    |   创建文档
v1.0.1  |   2014-07-14  |   张生    |   增加部分接口参数的说明
v2.0.0  |   2014-08-22  |   郑旭    |   增加全局监听、修改SDK部署配置、修改部分接口调用方式
v2.1.0  |   2014-10-14  |   郑旭    |   移除悬浮窗配置接口，移除自动更新接口，新增自定义更新接口，替换移动短代运营商配置
v2.1.1.12	|   2014-11-21  |   张生    |   增加充值测试模式，游戏退出接口，获取SDK版本号接口说明，mark字符扩展，充值金额改为整型
v2.1.1.13|  2014-11-22  |   张生    |   增加游戏圈不存在时游戏退出的弹框  
v2.2.0.2 |  2014-12-22  |   张生    |   调整移动短代策略，登出接口和帐号切换接口合并到初始化全局接口里  
v2.3.0.0 |  2015-01-27  |   张生    |   支付宝升级和优化，增加充值审核模式，去除冗余的参数配置，新增意见反馈和消息推送入口  
v2.4.0.5 |  2015-04-25  |   张生    |   优化消息中心与用户反馈功能，增加用户中心维护公告，增加历史订单查看功能  
v2.4.2.1 |  2015-06-16  |   张生    |   增加短代退费功能，升级支付宝，对Android5.0进行一些兼容  
v2.4.3.0 |  2015-07-20  |   张生    |   新增微信充值（如需测试或接入请联系运营）  
v2.5.0.0 |  2015-08-15  |   张生    |   补充游戏退出时的说明，修改关联资源工程处的错误说明，优化一些代码格式
v2.6.0.4 |  2015-10-30	|   张生    |   增加微信接入的说明
v2.7.0.2 |  2016-01-20  |   张生    |   为新渠道‘优易付’修改接入流程   
v2.7.1.0 |  2016-05-12  |   张生    |   移除AndroidManifest里launchMode配置  
v2.8.0.2 |  2016-06-30  |   张生    |   更新AndroidManifest组件配置，和proguard配置  
v2.25.0.1 |  2019-04-15  |   涂仕聪    |   修改AndroidManifest
v2.25.0.2 |  2019-06-17  |   张生    |   增加服务器ID规范的说明
v2.26.0.0 |  2019-06-17  |   涂仕聪    |   删除权限并修改文档错误
v2.26.0.8 |  2019-07-29  |   涂仕聪    |   修改AndroidManifest里的FileProvider
v2.28.0.0 |  2019-09-17  |   涂仕聪    |   提供实名认证入口
v2.29.0.0 |  2019-11-01  |   涂仕聪    |   android Q兼容
v2.31.0.8 |  2020-04-14  |   涂仕聪    |   修改混淆和AndroidManifest，新增版本更新提示
v2.37.0.205 |  2021-03-24  |   涂仕聪    |   新增违规举报接口
v2.37.0.211 |  2021-04-27  |   涂仕聪    |   新增Android 11兼容，声明所要进行交互的应用包名，主要用于外部授权登录

# 目录

[1 文档说明](#文档说明)  
&nbsp;&nbsp;&nbsp;&nbsp;[1.1 功能描述](#功能描述)  
&nbsp;&nbsp;&nbsp;&nbsp;[1.2 阅读对象](#阅读对象)  
&nbsp;&nbsp;&nbsp;&nbsp;[1.3 开发包内容](#开发包内容)  
[2 集成流程](#集成流程)  
&nbsp;&nbsp;&nbsp;&nbsp;[2.1 接入前期准备](#接入前期准备)  
&nbsp;&nbsp;&nbsp;&nbsp;[2.2 SDK集成流程](#SDK集成流程)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2.2.1 关联资源工程](#关联资源工程)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2.2.2 配置AndroidManifest.xml文件](#%E9%85%8D%E7%BD%AEandroidmanifestxml%E6%96%87%E4%BB%B6)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2.2.3 代码混淆配置](#代码混淆配置)  
[3 接入流程](#接入流程)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.1 初始化【必接】](#初始化)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.2 用户登录【必接】](#用户登录)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.3 登录状态查询](#登录状态查询)   
&nbsp;&nbsp;&nbsp;&nbsp;[3.4 获取当前登录用户信息](#获取当前登录用户信息)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.5 用户切换](#用户切换)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.6 用户注销](#用户注销)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.7 游戏关闭【必接】](#游戏关闭)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.8 设置用户所在服务器ID【必接】](#%E8%AE%BE%E7%BD%AE%E7%94%A8%E6%88%B7%E6%89%80%E5%9C%A8%E6%9C%8D%E5%8A%A1%E5%99%A8id)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.9 检查更新](#检查更新)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.10 充值【必接】](#充值)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.11 获取SDK版本号](#获取SDK版本号)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.12 获取状态信息](#获取状态信息)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.13 绑定手机](#绑定手机)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.14 检查手机绑定状态](#检查手机绑定状态)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.15 跳转到游戏圈帖子详情页面](#跳转到游戏圈帖子详情页面)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.16 跳转到游戏评论页面](#跳转到游戏评论页面)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.17 跳转到游戏圈页面](#跳转到游戏圈页面)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.18 User类内部方法含义说明](#User类内部方法含义说明)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.19 实名认证](#实名认证)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.20 违规举报](#违规举报)  
# 文档说明
## 功能描述
4399运营SDK（以下简称：SDK）主要用来向第三方游戏开发者提供便捷、安全一级可靠的4399账户登录、多渠道充值付费、版本升级检测等功能。本文主要描述SDK接口的使用方法，供合作伙伴的开发者接入使用。

## 阅读对象
本文档面向具有一定Android客户端开发能力，了解Android客户端的开发和管理人员。

## 开发包内容
 - <font color = green>v2.36.0+183版本开始，运营SDK提供的是完整android studio project（不再是eclipse版本，如开发者伙伴们使用的是eclipse需自行转换项目目录结构）</font>
 - operate：SDK资源文件工程内含SDK jar包
 - samples：Demo工程  
 - 其它一些project工程配置文件

# 集成流程
## 接入前期准备
1. 向4399运营人员提供游戏名称、游戏内货币名称、人民币与游戏币的兑换率
2. 4399运营人员会提供接入时需要的`GameKey`和`Secrect`。
3. GameKey为接入客户端SDK时使用，在初始化SDK时传入。请勿将Secrect写入游戏客户端。
4. GameKey，Secrect同时需要配置在服务端，详见[服务端接口文档](https://github.com/4399SDKDev/4399OperateSDK/blob/master/Document/ServerDocument.md)。

## <span id = "SDK集成流程">SDK集成流程</span>
假设现在你的工程目录名字叫project，下面将具体介绍如何将SDK接入project中。

### 关联资源工程  

#### Android Studio
* 将operate导入到Android Studio中
* 游戏主module依赖operate

#### Eclipse
* 将operate导入到eclipse中
* 拷贝assets目录下的`uniaccount_classez.jar`到应用工程的assets目录下
* 右键点击operate工程名→Properties→Android
* 勾选Is Library→OK
* 右键点击project工程名→Properties→Add
* 在弹出的对话框中点选资源工程operate→OK  

*注意：如果游戏使用Eclipse作为开发IDE，需要手动拷贝`uniaccount_classez.jar`到应用工程下*

#### so 对齐
若游戏仅支持部分abi的so，应使SDK保持一致，假设是armeabi：
- Android Studio：使用`abiFilters`过滤，选择需要的so
- Eclipse：将`m4399OperateSDK/lib`目录下未使用的so文件夹删除，即将其余的x86、arm64-v8a、armeabi-v7a文件夹删除。


### 配置AndroidManifest.xml文件
- 添加SDK所需的权限与Android 11兼容（声明所要进行交互的应用包名，主要用于外部授权登录）
``` xml
    <!--
       4399 运营SDK：
       以下是权限配置，包括第三方SDK需要的，以jar+res 方式接入需要打开以下内容，aar则不需
    -->
   <!-- 一般性权限 -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES" />
    <!-- 一键登录 -->
    <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE" />
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <!--suppress DeprecatedClassUsageInspection -->
    <uses-permission android:name="android.permission.GET_TASKS" />

    <!-- 4399 运营SDK：Android 11兼容，声明所要进行交互的应用包名，主要用于外部授权登录 -->
    <queries>
        <package android:name="com.m4399.gamecenter" />
        <package android:name="com.tencent.mobileqq" />
        <package android:name="com.sina.weibo" />
        <package android:name="com.tencent.mm" />
    </queries>
```
- 注册SDK相关Activity&Service，注意必须放入`<application>`元素区块内
``` xml
    
<!-- 
    4399 运营SDK： 游戏application要注意对 android 9.+ 系统的http请求的兼容配置，参考
    android:networkSecurityConfig="@xml/m4399_network_policy"
 -->
<application
    android:allowBackup="false"
    android:networkSecurityConfig="@xml/m4399_network_policy">

    <!--  4399 运营SDK：旧的http请求库的兼容  -->
    <uses-library
        android:name="org.apache.http.legacy"
        android:required="false" />

    <!--  兼容7.0+ 文件访问权限变更 android:authorities="游戏包名.operate.FileProvider"-->
    <provider
        android:authorities="{APP_PACKAGE_NAME}.operate.FileProvider"
        android:exported="false"
        android:grantUriPermissions="true"
        android:name="cn.m4399.operate.OpeFileProvider">
        <meta-data
            android:name="android.support.FILE_PROVIDER_PATHS"
            android:resource="@xml/m4399_ope_file_paths" />
    </provider>

    <!--
            4399 运营SDK：
            以下是 Activity 配置，以jar+res 方式接入需要打开以下内容，aar则不需
            另外，第三方页面方向有时候需要明确设置，比如支付宝h5页面，可以设置为横屏

            activity的配置不能少于orientation|screenSize|keyboardHidden，这些配置是为了防止Activity被系统或第三方界面强
            拉成竖屏时，发生重建而加入的。SDK的Activity支持横屏或竖屏，但不支持横竖屏切换，否则会包初始化问题
        -->
        <activity
            android:name="cn.m4399.operate.component.OperateActivity"
            android:configChanges="orientation|screenSize|keyboardHidden"
            android:screenOrientation="behind"
            android:theme="@style/m4399TranslucentFullscreenActivityTheme" />
        <activity
            android:name="cn.m4399.operate.recharge.RechargeActivity"
            android:configChanges="orientation|screenSize|keyboardHidden"
            android:screenOrientation="behind"
            android:theme="@android:style/Theme.NoTitleBar.Fullscreen" />

        <!-- 4399 运营SDK：以下是支付宝 H5 页面Activity，请游戏方根据游戏的横竖屏要求手工配置landscape|portrait -->
        <activity
            android:name="com.alipay.sdk.app.H5PayActivity"
            android:configChanges="orientation|keyboardHidden|navigation|screenSize"
            android:exported="false"
            android:screenOrientation="behind"
            android:windowSoftInputMode="adjustResize|stateHidden" />
        <!-- 4399 运营SDK：以下是一键登录SDK，请游戏方根据游戏的横竖屏要求手工配置landscape|portrait -->
        <activity
            android:name="cn.com.chinatelecom.account.sdk.ui.AuthActivity"
            android:exported="false"
            android:screenOrientation="behind"
            android:theme="@android:style/Theme.Light.NoTitleBar.Fullscreen" />
        <activity
            android:name="cn.com.chinatelecom.account.sdk.ui.PrivacyWebviewActivity"
            android:exported="false"
            android:screenOrientation="behind"
            android:theme="@android:style/Theme.Light.NoTitleBar.Fullscreen" />
        <activity
            android:name="cn.m4399.operate.account.onekey.wo.WoLoginActivity"
            android:exported="false"
            android:screenOrientation="behind"
            android:theme="@android:style/Theme.Light.NoTitleBar.Fullscreen" />

</application>
```
* 注意：<font color = green>第三方支付SDK与电信/移动一键登录的Activity需在AndroidManifest.xml中强制配置横竖屏，请游戏方根据游戏的横竖屏要求手工配置`landscape`|`portrait`  </font>
* 游戏Activity的配置不能少于orientation|screenSize|keyboardHidden这三项，这些配置是为了防止Activity被系统或第三方界面强
        拉成竖屏时，发生重建而加入的。因为Activity重建有可能会因为某些初始化不全，发生crash。  
* SDK的Activity支持横屏或竖屏，但不支持横竖屏切换，缺少orientation|screenSize|keyboardHidden有可能发生初始化问题。  
* 关于渠道开关：接入4399SDK的游戏，又希望在多个渠道投放apk，可以打开Manifest中的开关，并且联系运营使用专用打包工具打入渠道标识，但不需要游戏再针对每个渠道单独打包；如果不需渠道标识，请勿打开开关，否则会增加SDK初始化时间。

### 代码混淆配置
如果游戏有需要进行代码混淆，请不要混淆联编的jar包下的类，可以在`proguard.cfg`文件里追加以下配置

```
-dontwarn android.support.v4.**
-keep class android.support.v4.** { *; }
-keep public class * extends android.support.v4.**

-dontwarn cn.m4399.operate.**
-keep class cn.m4399.operate.** {*;}
-keepclassmembers class cn.m4399.operate.R$* {*;}
-keep class com.m4399.gamecenter.** {*;}

-dontwarn android.net.**
-keep class android.net.SSLCertificateSocketFactory{*;}
-keep class com.ishumei.** { *; }

-keep class cn.com.chinatelecom.account.** {*;}
-dontwarn com.unicom.xiaowo.account.shield.**
-keep class com.unicom.xiaowo.account.shield.**{*;}
```
# 接入流程
## 初始化
初始化推荐在游戏初始化过程中进行。
```java
mOpeCenter = OperateCenter.getInstance();
mOpeConfig = new OperateCenterConfig.Builder(this)
	.setGameKey("GAME_KEY")     //设置GameKey
	.setDebugEnabled(false)     //设置DEBUG模式,用于接入过程中开关日志输出，发布前必须设置为false或删除该行。默认为false。
	.setOrientation(ActivityInfo.SCREEN_ORIENTATION_PORTRAIT)  //设置横竖屏方向，默认为横屏，现支持横竖屏，和180度旋转
	.setSupportExcess(true)     //设置服务端是否支持处理超出部分金额，默认为false
	.setPopLogoStyle(PopLogoStyle.POPLOGOSTYLE_ONE) //设置悬浮窗样式，现有四种可选
	.setPopWinPosition(PopWinPosition.POS_LEFT)	//设置悬浮窗默认显示位置，现有四种可选
        .compatNotch(true)	// 设置游戏是否兼在高于Android 9.0版本系统容全面屏，默认值false（不兼容）
	.build();
mOpeCenter.setConfig(mOpeConfig);
mOpeCenter.init(new OperateCenter.OnInitGloabListener() {
	// 初始化结束执行后回调
	@Override
	public void onInitFinished(boolean isLogin, User userInfo) {
		assert(isLogin == mOpeCenter.isLogin());
	}

	// 注销帐号的回调， 包括个人中心里的注销和logout()注销方式
	// fromUserCenter区分是否是从悬浮窗-个人中心("4399游戏助手页面")注销的，若是则为true，不是为false
	@Override
	public void onUserAccountLogout(boolean fromUserCenter) {
	}

 // 切换帐号的回调 
 //fromUserCenter区分是否是从"4399游戏助手页面"切换的，若是则为true，不是为false
    @Override
    public void onSwitchUserAccountFinished(boolean fromUserCenter,User userInfo) {
       
    }
});
```

`是否支持处理超出部分金额`也可单独设置
```java
mOpeCenter.setSupportExcess(support);
```
`能否支持处理超出部分金额`指在使用SDK充值时，由于用户选择的充值渠道不同，可能造成实际充值金额超出游戏下单时传入的金额。如果游戏服务端能够正确处理超出部分的金额，则本接口传入true。如果无法支持处理超出部分的金额，则传入false，SDK将会根据传入金额自动隐藏无法满足充值金额的渠道（例：开发者设置SupportExcess为false，充值时传入7元，此时4399一卡通中无7元面额的充值卡，此时4399一卡通的充值渠道将自动隐藏）。*SupportExcess*默认为false。

*注：代码中`MainActivity`为当前Activity.下文的`mOpeCenter`指`OperateCenter`实例，通过`getInstance()`静态方法获得。*  

* 悬浮窗  
悬浮窗会在用户登录后显示在游戏最前端，用户可通过悬浮窗进入个人中心和游戏圈。个人中心包含切换用户、修改密码、绑定手机、注销、游币余额显示功能。游戏圈依赖1.4.1以上版本的4399游戏盒，当用户有安装4399游戏盒时，会自动弹出本游戏的游戏圈页面。  

* 悬浮窗类型  
游戏开发者可根据游戏的风格自由选择合适的悬浮窗样式，在配置SDK时设置。 

|样式类型|图示|
|--------|----|
|PopLogoStyle.POPLOGOSTYLE_ONE|<img src="res/m4399_ope_pop_logo_one_normal.png" alt="POPLOGOSTYLE_ONE" />|
|PopLogoStyle.POPLOGOSTYLE_TWO|<img src="res/m4399_ope_pop_logo_two_normal.png" alt="POPLOGOSTYLE_TWO" />|
|PopLogoStyle.POPLOGOSTYLE_THREE|<img src="res/m4399_ope_pop_logo_three_normal.png" alt="POPLOGOSTYLE_THREE" />|
|PopLogoStyle.POPLOGOSTYLE_FOUR|<img src="res/m4399_ope_pop_logo_four_normal.png" alt="POPLOGOSTYLE_FOUR" />|

* 悬浮窗默认位置
游戏开发者可根据游戏的风格自由选择合适的悬浮窗初始化的默认位置，在配置SDK时设置。 
默认有四种位置 ：

|样式类型|位置|
|--------|----|
|PopWinPosition.POS_LEFT（默认位置）| 屏幕左侧|
|PopWinPosition.POS_RIGHT|屏幕右侧|
|PopWinPosition.POS_TOP|屏幕上侧|
|PopWinPosition.POS_BOTTOM|屏幕下侧|

## 用户登录
用户在触发登录时，调用该接口，如果SDK内已包含未注销的用户凭证，将自动返回用户信息。如需强制调出登录界面，请使用【用户切换】接口。
```java
mOpeCenter.login(MainActivity.this, new OnLoginFinishedListener() {

	@Override
	public void onLoginFinished(boolean success, int resultCode, User userInfo) {
	    //登录结束后的游戏逻辑
	}
});
```
SDK会自动识别用户手机中是否安装了新版的4399游戏盒1.4.1以上版本，如果已安装，自动跳转至游戏盒授权登录。如果未安装，则弹出Web版4399统一登录界面。
在登录成功后，监听器返回的`User`类型的用户信息中将包含`State`登录凭证，该信息可用于游戏服务端进行[用户信息二次验证](https://github.com/4399SDKDev/4399OperateSDK/blob/master/Document/ServerDocument.md#%E7%99%BB%E5%BD%95%E5%87%AD%E8%AF%81%E9%AA%8C%E8%AF%81%E6%8E%A5%E5%8F%A3)

*注：登录后如果未注销，登录状态将一直保持直至登录凭证过期或失效（若用户修改平台账户密码，所有游戏授权凭证将失效，需重新登录）。建议游戏在初始化完成后调用[登录状态查询](#登录状态查询)接口查询用户当前登录状态。*

## 登录状态查询
查询当前客户端是否有账号登录
```java
boolean isLogin = mOpeCenter.isLogin();
```

## 获取当前登录用户信息
在SDK处于登录状态时，可通过该接口获取当前用户的信息（`UID`、`用户名`、`昵称`、`登录凭证`）。

**注意：SDK返回的uid是字符串类型，转换成整型后取值范围是（0～2^32-1）；若开发者要以整型值方式使用它，需要注意溢出的可能性**
```java
User user = mOpeCenter.getCurrentAccount();
```

## 用户切换
用户只有在登录成功之后，才会注销旧账号
```java
mOpeCenter.switchAccount(MainActivity.this, new OnLoginFinishedListener() {

	@Override
	public void onLoginFinished(boolean success, int resultCode, User userInfo) {
	    //用户账号切换结束后的游戏逻辑
	}
});
```

## 用户注销  
当用户需要注销当前登录状态时，使用本接口，其回调函数在OnInitGloabListener中
```java
mOpeCenter.logout();
```

## 游戏关闭
```java
// 如果游戏已经配置游戏圈、攻略、礼包等功能弹窗内容区域会显示以上功能的相关item
// 在关闭前，SDK会弹出对话框询问“退出游戏”还是“继续游戏”
mOpeCenter.shouldQuitGame(MainActivity.this, new OnQuitGameListener() {
	@Override
	public void onQuitGame(boolean shouldQuit) {
		// 点击“退出游戏”时，shouldQuit为true，游戏处理自己的退出业务逻辑
		// 点击“游戏圈”内容区域时，SDK会进入游戏圈（攻略、礼包同上）
		// 点击“继续游戏”时，shouldQuit为false，SDK和游戏都不做任何处理
        if (shouldQuit) {
            //这边做退出游戏操作
        }
	}
});
```

## 设置用户所在服务器ID
当游戏有分服时，在用户选择角色进入分服时，请务必立即通过本接口设置所在服的ID。如果无分服，则可不设置。  
__服务器ID规范：不超过10位的数字字符串__
```java
ServerSelector.select(this);
```
## 检查更新
SDK将检查后台是否有新版本游戏上线，如果有，则显示更新内容，并提示用户升级。该升级为`增量升级`，后台在提交新版游戏时自动制作差分包，更新时用户只需下载APK文件中新旧版本有差异的部分。相关更新内容和版本提交事宜，请联系4399相关运营对接人员。  
4399SDK的增量升级分为  
- 全自动增量更新（无需操作，默认初始化完成）
- 自定义界面增量更新 （当游戏选择使用该策略时，上线前需与4399运营人员沟通）

自定义界面增量更新接入方法详见：[4399运营SDK增量升级说明](https://github.com/4399SDKDev/4399OperateSDK/blob/master/Document/DeltaUpdate.md)

## 充值
当用户需要充值时，可调用本接口启动充值中心界面。  
```java
mOpeCenter.recharge(MainActivity.this,
	je,     	//整型，充值金额（元）
	mark,   	//游戏方订单号
	productName,    //商品名称
	new OnRechargeFinishedListener() {
		@Override
		public void onRechargeFinished(boolean success, int resultCode, String msg) {
			if (success) {
				//请求游戏服，获取充值结果
			} else {
				//充值失败逻辑
			}
		}
});
```
* `je`充值金额：整型数字，4399充值中心仅支持整数金额充值，最小充值金额`1`元，最大不超过`50000`元。
* `mark`订单号：最大长度32位，支持大小写字母、数字、‘|’(竖线)、‘-’（中划线）、‘_’（下划线），该字段*不可为空，不可为字符串“0”，不可重复*。
* `productName`商品名称：最长不超过8个字符。 如果传入商品名，充值中心将直接显示改商品名称，如果充值金额大于下单时传入的`je`时，将显示商品名+XXX游戏币，相关游戏币的兑换比例在接入时提供给运营人员配置。如果未传入商品名，则直接显示XXX游戏币。

<b>关于客户端回调模式</b>

当使用充值，需要客户端来发放物品时，需要设置此回调方式
```
/**
 * 设置发放物品回调
 *
 * 设置此方法后，发放物品的方式，将由客户端决定
 *
 * 注意：使用客户端回调有较高安全风险，应用应使用服务端回调，实在条件不允许才能使用此方式
 *
 * @param listener 回调对象
 */
public void setDeliveringGoodsListener(@NonNull OnDeliveringGoodsListener listener) {
    ApiRecharge.singleton().setDeliverListener(listener);
}
```

```
public interface OnDeliveringGoodsListener {
        /**
         * 通知游戏方是否要发放物品
         *
         * @param of             充值订单
         * @return 游戏派发物品成功，返回true， 否则返回false
         * @see Order
         */
        boolean onDelivering(OrderFinished of);
    }
```

使用示例：设置相应的回调，监听客户端是否发放物品
```
operateCenter.setDeliveringGoodsListener(new OperateCenter.OnDeliveringGoodsListener() {
    @Override
    public boolean onDelivering(OrderFinished of) {
        toast(mActivity, getString(R.string.demo_fmt_distribution_of_goods, of));
        Pair<String, Integer> conclusion = of.conclude();
        mGoodsList.add(getString(R.string.demo_fmt_recharge_detail,
                of.money(), conclusion.first, conclusion.second));
        // 如果游戏因为某些原因发放失败，应返回false
        return true;
    }
});
```

<b>关于充值审核模式</b>
- 充值审核模式主要是用于游戏方测试充值回调  
- 充值审核模式可以在后台配置，具体请咨询相关运营人员  
- 充值审核模式下，没有正常的充值界面，充值渠道与参数都是固定的  

## <span id = "获取SDK版本号">获取SDK版本号</span>
示例：“2.36.0.183”，2.36.0是版本名(versionName)，185是版本号(versionCode)
```java
mOpeCenter.getVersion();
```

## 获取状态信息
工具接口，用于将回调函数中的`resultCode`解析为中文的说明(充值接口recharge的resultCode对应的中文是回调中的msg)。
```java
String resultMessage = OperateCenter.getResultMsg(resultCode);
```

## 绑定手机
```java
/*
*返回值：
*resultCode：
* -4：进程被系统（或用户）关闭
* -3：用户取消绑定
* -2：服务器异常
* -1：网络异常
* 0：用户未登录（或被踢出） 
* 1：已绑定
* 2：绑定成功
* 3：已绑定，游戏关闭绑定功能（无需绑定） 
* 4：未绑定，游戏关闭绑定功能（无需绑定） 
*msg：绑定成功或失败的描述信息
**/ 
mOpeCenter.bindPhone(this, new OnPhoneBindResultListener() {
	    @Override
	    public void onPhoneBindResult(int resultCode, String msg) {
		Log.v(TAG, "bindPhone resultCode=" + resultCode+",msg="+msg);
	    }
	});

```
## 检查手机绑定状态
```java
/*
*该接口为异步接口
*返回值：
*resultCode：
* -2：服务器异常
* -1：网络异常
* 0：用户未登录（或被踢出） 
* 1：游戏开启绑定手机功能，用户已绑定手机号
* 2：游戏开启绑定手机功能，用户未绑定手机号
* 3：游戏未开启绑定手机功能，用户已绑定手机号
* 4：游戏未开启绑定手机功能，用户未绑定手机号
*msg：查询结果的描述信息
**/ 
mOpeCenter.checkBindPhoneState(new OnCheckPhoneBindStateListener() {
            @Override
            public void onCheckPhoneBindState(int resultCode, String msg) {
                Log.v(TAG, "check bindPhone resultCode=" + resultCode+",msg="+msg);
            }
    });
```

## 跳转到游戏圈帖子详情页面
```java
/**
* 打开游戏盒游戏圈指定帖子，若没有游戏圈toast提示用户，若没有下载游戏盒则提示下载
*/
mOpeCenter.showGameCircleDetail(MainActivity.this,9998);

```

## 跳转到游戏评论页面
```java
/**
* 打开游戏盒该游戏的评论页面
* 若没有初始化或者初始化失败，调用此方法，会弹出toast提示“参数为空，请先初始化”
* 若未安装游戏盒，则出现提示下载游戏盒的弹窗
*/
mOpeCenter.showGameCommentArea(MainActivity.this);

```

## 跳转到游戏圈页面
```java
/**
* 打开游戏盒该游戏的游戏圈页面
* 若没有初始化或者初始化失败，调用此方法，会弹出toast提示“参数为空，请先初始化”
* 若未安装游戏盒，则出现提示下载游戏盒的弹窗
*/
mOpeCenter.showGameForum(MainActivity.this);

```

## 跳转到游戏盒主页
```java
/**
* 打开游戏盒主页面
* 若未安装游戏盒，则出现提示下载游戏盒页面
*/
mOpeCenter.StartGameBox(MainActivity.this);

```
## <span id = "User类内部方法含义说明">User类内部方法含义说明</span>
```java
public final class User {
   ...
   
   /**
     * Description: v2.30.0.28及之前版本， 0 未实名，1 小于8岁，2 小于18岁，3、4 18岁及以上
     *              v2.30.0.28之后版本， 0 未实名，1 小于8岁，2 8-15岁，3、4 18岁及以上，5 16-17岁
     */
    public int getIdCardState() {
        return idCardState;
    }

    /**
     * Description: 是否通过实名认证 true:通过（身份信息可能是未成年人），false：不通过
     */
    public boolean isIdCheckedReal() {
        return idCheckedReal;
    }

    /**
     * Description: 控制游戏中“实名认证”UI显示/隐藏 true:显示，false：隐藏
     *              idcardEditable字段已关联实名状态（有奖实名调用仅需这么一个判断就够了）
     */
    public boolean isIdCardEditable() {
        return idcardEditable;
    }
}
```

## 实名认证 

- 该接口不可以在SDK登录回调中调用，否则会与防沉迷机制冲突。 

- 使用场景举例：可用于游戏内“有奖实名”的功能支持，需要搭配游戏内部UI实现（User类中isIdCardEditable（）值为true显示UI，false隐藏），通过该UI的点击事件调用mOpeCenter.nameAuthentication接口。

- 注意：本接口主要为游戏功能提供支持，防沉迷功能由SDK内部实现，不需要调用此方法，无此需求开发者请自行忽略。

```java
mOpeCenter.authReward(this, new OperateCenter.NameAuthSuccessListener() {
            @Override
            public void onAuthSuccess(int idCardState) {
	    	/**
     		* idCardState: 0 未实名，1 小于8岁，2 8-15岁，3、4 18岁及以上，5 16-17岁	
     		*/
                Toast.makeText(MainActivity.this, "name auth success , idCardState: " + idCardState, Toast.LENGTH_SHORT).show();
            }

	    @Override
            public void onCancel() {
	    	//关闭实名认证弹窗回调
                Toast.makeText(MainActivity.this, "name auth onCancel", Toast.LENGTH_SHORT).show();
            }
        });
```

## 违规举报 

- 使用场景举例：在游戏内玩家聊天内容后（或点击玩家头像出现的用户信息详情弹窗中）放置一个举报按钮。

- 注意：本接口主要向游戏方开发者提供聊天举报功能支持，无此需求开发者请自行忽略。

```java
   /**
     * @param violation 违规信息，各字段必须且名称固定如下，若确实没有可留空，但不能不传
     *          
     * Map<String, String> violation = new HashMap<String, String>();
     *                    violation.put("g_uid", "被举报人uid");
     *                    violation.put("g_tid", "聊天频道ID");
     *                    violation.put("g_sid", "服务器ID");
     *                    violation.put("g_rid", "角色ID");
     *                    violation.put("g_role", "角色名称");
     *                    violation.put("g_gname", "公会名");
     *                    violation.put("g_cname", "宠物名");
     *                    violation.put("g_content", "聊天内容");
     */                
mOpeCenter.reportViolation(MainActivity.this, violation);
```

