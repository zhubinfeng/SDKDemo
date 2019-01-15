>第一步,cocopods安装如下三方库 

```
use_frameworks!

# Pods for LTGameSDK
pod 'GoogleSignIn'
pod 'AFNetworking'
pod 'FacebookCore'
pod 'FacebookLogin'
pod 'FBSDKCoreKit', '~> 4.38.0'
pod 'FBSDKLoginKit', '~> 4.38.0'
pod 'WechatOpenSDK'
```
>第二步，初始化LT应用

1，在APPdelegate.h文件中导入头文件

```
#import <LTGameSDK/LTSDKLoginManager.h>
```
2,初始化应用<br>
```
[[LTSDKLoginManager sharedInstance] registLTPlatformAppID:@"xxxx" withAppkey:@"xxxx"];
```

>第三步，集成对应的第三平台<br>

>URL Schemes 的添加方法

>![](https://github.com/zhubinfeng/SDKDemo/blob/master/URL_Schemes.png?raw=true)
>
>配置-ObjC方法 Build Setting -> Other Linker Flags 添加-ObjC
>![](https://github.com/zhubinfeng/SDKDemo/blob/master/otherLinkerFlags.png?raw=true)

>**一 Facebook集成**
>>1,添加URL scheme fbxxxx
>>
>>2，在info.plist中添加
>>
>>
         <key>FacebookAppID</key>
         <string>xxxx</string>
         <key>FacebookDisplayName</key>
         <string>应用的名称</string>
         <key>LSApplicationQueriesSchemes</key>
         <array>
         <string>fbapi</string>
         <string>fb-messenger-share-api</string>
         <string>fbauth2</string>
         <string>fbshareextension</string>
         </array>
>>
>>
>>3，配置-ObjC
>>4,在APPdelegate.h文件中添加
>>
>>```
>>-(BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options{
    [[LTSDKLoginManager sharedInstance] application:app openURL:url options:options];
    return YES;
}
>>```
>>
>>5，在APPdelegate.h中初始化
>>
>>```
>>[[LTSDKLoginManager sharedInstance] registWeChatPlatform:@"xxx"];
>>```
>>
>>6，登录调用
>>```
>>[[LTSDKLoginManager sharedInstance] facebookLogin:^(LTUser * _Nonnull loginUser) {
        NSString *lt_UID = loginUser.LT_UID;
        NSString *apiToken = loginUser.apiToken;
    } withUIViewController:self];
>>```
>>

>**二 Google集成**
>>1,添加URL scheme com.googleusercontent.apps.xxxx
>>
>>3，配置-ObjC
>>
>>4，在APPdelegate.h中初始化
>>
>>```
>>[[LTSDKLoginManager sharedInstance] registGooglePlatform:@"xxxx.apps.googleusercontent.com" withUIViewController:self];
>>```
>>
>>6，登录调用
>>```[[LTSDKLoginManager sharedInstance] googleLoginGetLTID:^(LTUser * _Nonnull loginUser) {
        NSString *lt_UID = loginUser.LT_UID;
        NSString *apiToken = loginUser.apiToken;
    }];
>>```

>**三 微信集成**
>>1,添加URL schemes xxxx
>>2,在APPdelegate.h文件中添加
>>
>>```
>>-(BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options{
    [[LTSDKLoginManager sharedInstance] application:app openURL:url options:options];
    return YES;
}
>>```
>>
>>3，在APPdelegate.h中初始化
>>
>>```
>>[[LTSDKLoginManager sharedInstance] registWeChatPlatform:@"xxx"];
>>```
>>
>>4，登录调用
>>```
>>[[LTSDKLoginManager sharedInstance] weChatLogin:^(LTUser * _Nonnull loginUser) {
        NSString *lt_UID = loginUser.LT_UID;
        NSString *apiToken = loginUser.apiToken;
    }];
>>```


>**四 QQ集成**
>>1,将QQ的TencentOpenAPI.framework拖到工程中，选中图中三项
>>![](https://github.com/zhubinfeng/SDKDemo/blob/master/frameworkAdd.png?raw=true)
>>
>>2，配加依赖包
>>>“Security.framework”,“libiconv.tdb”，“SystemConfiguration.framework”，“CoreGraphics.Framework”、“libsqlit.3.tdb”、“CoreTelephony.framework”、“libz.tdb”
>>![](https://github.com/zhubinfeng/SDKDemo/blob/master/addLinkFramework.png?raw=true)
>>
>>3，配置-fobjc-arc(与配置-ObjC方法相同)
>>
>>4,添加URL schemes tencentxxxx
>>
>>5,在info.plist中 LSApplicationQueriesSchemes字段添加如下字段
>>
>>
         <string>mqqapi</string>
         <string>mqq</string>
         <string>mqqOpensdkSSoLogin</string>
         <string>mqqconnect</string>
         <string>mqqopensdkdataline</string>
         <string>mqqopensdkgrouptribeshare</string>
         <string>mqqopensdkfriend</string>
         <string>mqqopensdkapi</string>
         <string>mqqopensdkapiV2</string>
         <string>mqqopensdkapiV3</string>
         <string>mqzoneopensdk</string>
         <string>mqqopensdkapiV3</string>
         <string>mqqopensdkapiV3</string>
         <string>mqzone</string>
         <string>mqzonev2</string>
         <string>mqzoneshare</string>
         <string>wtloginqzone</string>
         <string>mqzonewx</string>
         <string>mqzoneopensdkapiV2</string>
         <string>mqzoneopensdkapi19</string>
         <string>mqzoneopensdkapi</string>
         <string>mqzoneopensdk</string>
>>
>>6,在APPdelegate.h文件中添加
>>
>>```
>>-(BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options{
    [[LTSDKLoginManager sharedInstance] application:app openURL:url options:options];
    return YES;
}
>>```
>>
>>7，在APPdelegate.h中初始化
>>
>>```
>>[[LTSDKLoginManager sharedInstance] registQQPlatform:@"xxxx"];
>>```
>>
>>8，登录处调用
>>```
>>[[LTSDKLoginManager sharedInstance] QQLogin:^(LTUser * _Nonnull loginUser) {
        NSString *lt_UID = loginUser.LT_UID;
        NSString *apiToken = loginUser.apiToken;
    }];
>>```
