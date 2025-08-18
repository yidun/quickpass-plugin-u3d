# 号码认证
直连三大运营商，一步校验手机号与当前 SIM 卡号一致性。优化注册/登录/支付等场景验证流程

## 平台支持（兼容性）
  | Android | iOS |  
  | ---- | ----- |
  | 适用版本区间：4.4以上|适用版本区间：9 - 14 | 

## 资源引入/集成

下载并解压出 quickpass-plugin-u3d.unitypackage，在 Assets 目录右键选择 Import Package 导入 quickpass-plugin-u3d.unitypackage 资源包

其中 TestBehaviourScript.cs 是调用示例代码

### 项目开发配置

Android release 包需要添加混淆规则

```
-dontwarn com.cmic.sso.sdk.**
-keep class com.cmic.sso.**{*;}
-dontwarn com.sdk.**
-keep class com.sdk.** { *;}
-keep class cn.com.chinatelecom.account.**{*;}
-keep public class * extends android.view.View
-keep class com.netease.nis.quicklogin.entity.**{*;}
-keep class com.netease.nis.quicklogin.listener.**{*;}
-keep class com.netease.nis.quicklogin.QuickLogin{
    public <methods>;
    public <fields>;
}
-keep class com.netease.nis.quicklogin.helper.UnifyUiConfig{*;}
-keep class com.netease.nis.quicklogin.helper.UnifyUiConfig$Builder{
     public <methods>;
     public <fields>;
 }
-keep class com.netease.nis.quicklogin.utils.LoginUiHelper$CustomViewListener{
     public <methods>;
     public <fields>;
}
-keep class com.netease.nis.basesdk.**{
    public *;
    protected *;
}
```

## 插件方法说明

## Android

### 初始化

```
Init(businessId, timeout, debug)
```

#### 参数说明：
*   入参说明：

    |参数|类型|是否必填|默认值|描述|
    |----|----|--------|------|----|
    | businessId | string | 是 | 无 | 易盾分配的业务 id |
    | timeout | int |否| 6000 |运营商预取号和授权登录接口的超时时间，单位毫秒|
    | debug | boolean |否| false |是否打开debug开关|

### 当前环境是否支持号码认证

```
CheckVerifyEnable()
```

### 预取号

```
PreFetchNumber()
```

预取号的回调在 QuickpassPreCallback()中，预取号可以加快后面取号的速度，建议尽量提前

```
public class QuickpassPreCallback : AndroidJavaProxy
{
    public QuickpassPreCallback() : base("com.netease.nis.quicklogin.listener.QuickLoginPreMobileListener") { }

    public void onGetMobileNumberSuccess(string YDToken, string mobileNumber)
    {
        // 预取号成功，YDToken：易盾token mobileNumber：掩码
        Debug.Log("onGetMobileNumberSuccess" + YDToken);
        Debug.Log("onGetMobileNumberSuccess" + mobileNumber);
    }

    public void onGetMobileNumberError(string YDToken, string msg)
    {
        // 预取号失败 msg 中有详细的失败信息
        Debug.Log("onGetMobileNumberError" + YDToken);
        Debug.Log("onGetMobileNumberError" + msg);
    }
}

```

### 设置授权页样式

```
SetUiConfig(QuickpassUiConfig uiConfig)
```

QuickpassUiConfig 是可配置项，具体的配置项看注释

**<font color=red>开发者不得通过任何技术手段，将授权页面的隐私栏、手机掩码号、供应商品牌内容隐藏、覆盖</font>**<br>
**<font color=red>网易易盾与运营商会对应用授权页面进行审查，若发现上述违规行为，网易易盾有权将您的一键登录功能下线</font>**

![安卓规范示意图](https://nos.netease.com/cloud-website-bucket/fc608fc8c376e8b384e947e575ef8b5f.jpg)
![自定义展示图](https://nos.netease.com/cloud-website-bucket/410d6012173c5531b1065909c9484d36.jpg)

##### 状态栏
| 配置项                        | 说明                                   |
|----------------------------| -------------------------------------- |
| statusBarColor:string      |     设置状态栏背景颜色，十六进制RGB值，如 "#ff0000"|
| isStatusBarDarkColor:bool  | 设置状态栏字体图标颜色是否为暗色(黑色)，默认false |

##### 导航栏

| 配置项                                             | 说明                                                         |
|:------------------------------------------------| ------------------------------------------------------------ |
| navBackIcon:string                              | 导航栏图标，图标资源放在 Assets/plugins/Android/CustomAndroidResource.androidlib/res/drawable 目录下，这里配置图标名字 |
| navBackIconWidth:int                            | 设置导航栏返回图标的宽度，单位 dp                                     |
| navBackIconHeight:int                           | 设置导航栏返回图标的高度，单位 dp                                     |
| navBackIconGravity:int                          | 设置导航栏返回图标位置，居左 3，居右 5，默认居左                                    |
| navBackIconMargin:int                           | 设置导航栏返回图标上下左右边距，单位 dp                                     |
| isHideBackIcon:bool                             | 设置是否隐藏导航栏返回按钮，默认 false                                       |
| navBackgroundColor:string                       | 设置导航栏背景颜色，十六进制RGB值，如 "#ff0000"                                           |
| navHeight:int                                   | 设置导航栏高度，单位 dp                                       |
| navTitle:string                                 | 设置导航栏标题                                               |
| navTitleColor:string                            | 设置导航栏标题颜色，十六进制RGB值，如 "#ff0000"                                          |
| navTitleSize:int                                | 设置导航栏标题大小，单位 sp                                   |
| navTitleDpSize:int                                | 设置导航栏标题大小，单位 dp                                   |
| isNavTitleBold:bool                             | 设置导航栏标题是否为粗体，默认false                                     |
| isHideNav:bool                                  | 设置是否隐藏导航栏，默认 false                                           |

##### 应用 Logo

| 配置项                                       | 说明                                                         |
|:------------------------------------------| ------------------------------------------------------------ |
| logoIconName:string                       | 应用 logo 图标，图标资源放在 Assets/plugins/Android/CustomAndroidResource.androidlib/res/drawable 目录下，这里配置图标名字 |
| logoWidth:int                             | 设置应用logo宽度，单位dp                                     |
| logoHeight:int                            | 设置应用 logo 高度，单位 dp                                     |
| logoTopYOffset:int                        | 设置 logo 顶部 Y 轴偏移，单位 dp                                  |
| logoBottomYOffset:int                     | 设置 logo 距离屏幕底部偏移，单位 dp                             |
| logoXOffset:int                           | 设置 logo 水平方向的偏移，单位 dp                               |
| isHideLogo:bool                           | 设置是否隐藏 logo，默认 false                                             |

##### 手机掩码

| 配置项                                                        | 说明                                                         |
|:-----------------------------------------------------------| ------------------------------------------------------------ |
| maskNumberColor:string                                     | 设置手机掩码颜色，十六进制RGB值，如 "#ff0000"                                      |
| maskNumberSize:int                                         | 设置手机掩码字体大小，单位 px                                |
| maskNumberXOffset:int                                      | 设置手机掩码水平方向的偏移，单位 dp                           |
| maskNumberDpSize:int                                       | 设置手机掩码字体大小，单位 dp                                 |
| maskNumberTopYOffset:int                                   | 设置手机掩码顶部Y轴偏移，单位 dp                         |
| maskNumberBottomYOffset:int                                | 设置手机掩码距离屏幕底部偏移，单位 dp                           |
| maskNumberBackgroundRes:string                             | 设置手机掩码背景图                                           |
| maskNumberBold:bool                                        | 手机掩码是否加粗                                           |

##### 认证品牌

| 配置项                                           | 说明                                 |
|:----------------------------------------------| ------------------------------------ |
| sloganSize:int                                | 设置认证品牌字体大小，单位 px         |
| sloganDpSize:int                              | 设置认证品牌字体大小，单位 dp         |
| sloganColor:string                            | 设置认证品牌颜色，十六进制RGB值，如 "#ff0000"                     |
| sloganTopYOffset:int                          | 设置认证品牌顶部 Y 轴偏移，单位 dp      |
| sloganBottomYOffset:int                       | 设置认证品牌距离屏幕底部偏移，单位 dp |
| sloganXOffset:int                             | 设置认证品牌水平方向的偏移，单位 dp   |
| sloganBold:bool                               | 认证品牌字体是否加粗   |

##### 登录按钮

| 配置项                                                  | 说明                                                 |
|:-----------------------------------------------------| ---------------------------------------------------- |
| loginBtnText:string                                  | 设置登录按钮文本                                     |
| loginBtnTextSize:int                                 | 设置登录按钮文本字体大小，单位 px                     |
| loginBtnTextDpSize:int                               | 设置登录按钮文本字体大小，单位 dp                     |
| loginBtnTextColor:string                             | 设置登录按钮文本颜色，十六进制RGB值，如 "#ff0000"                                 |
| loginBtnWidth:int                                    | 设置登录按钮宽度，单位 dp                             |
| loginBtnHeight:int                                   | 设置登录按钮高度，单位 dp                             |
| loginBtnBackgroundRes:string                         | 设置登录按钮背景图标，图标资源放在 Assets/plugins/Android/CustomAndroidResource.androidlib/res/drawable 目录下，这里配置图标名字 |
| loginBtnTopYOffset:int                               | 设置登录按钮顶部Y轴偏移，单位 dp                      |
| loginBtnBottomYOffset:int                            | 设置登录按钮距离屏幕底部偏移，单位 dp                 |
| loginBtnXOffset:int                                  | 设置登录按钮水平方向的偏移，单位 dp                   |
| loginBtnMarginLeft:int                               | 设置登录按钮距离屏幕左边距离，单位 dp                   |
| loginBtnMarginRight:int                              | 设置登录按钮距离屏幕右边距离，单位 dp                   |
| loginBtnBold:bool                                    | 设置登录按钮文本是否加粗                 |

##### 隐私协议

| 配置项                                                        | 说明                                                         |
|:-----------------------------------------------------------| ------------------------------------------------------------ |
| privacyTextColor:string                                    | 设置隐私栏文本颜色，不包括协议 ，如若隐私栏协议文案为：登录即同意《中国移动认证条款》且授权 QuickLogin 登录， 则该API对除协议‘《中国移动认证条款》’区域外的其余文本生效 |
| privacyDialogTextColor:string                              | 协议未勾选弹窗隐私栏文本颜色，不包括协议                                                                              |
| privacyProtocolColor:string                                | 设置隐私栏协议颜色 。例如：登录即同意《中国移动认证条款》且授权 QuickLogin 登录 ， 则该 API 仅对‘《中国移动认证条款》’文案生效 |
| privacyDialogProtocolColor:string                          | 协议未勾选弹窗隐私栏协议颜色                                                                              |
| privacySize:int                                            | 设置隐私栏区域字体大小，单位 px                               |
| privacyDpSize:int                                          | 设置隐私栏区域字体大小，单位 dp                               |
| privacyBold:bool                                           | 设置隐私栏区域字体是否加粗                              |
| privacyWidth:int                                           | 设置隐私栏区域宽度，单位 dp                               |
| privacyTopYOffset:int                                      | 设置隐私栏顶部Y轴偏移，单位 dp                                |
| privacyBottomYOffset:int                                   | 设置隐私栏距离屏幕底部偏移，单位 dp                           |
| privacyTextMarginLeft:int                                  | 设置隐私栏复选框和文字内边距，单位 dp                             |
| privacyMarginLeft:int                                      | 设置隐私栏水平方向的偏移，单位 dp                             |
| privacyMarginRight:int                                     | 设置隐私栏右侧边距，单位 dp                                   |
| privacyState:bool                                          | 设置隐私栏协议复选框勾选状态，true 勾选，false 不勾选，默认 false          |
| isHidePrivacyCheckBox:bool                                 | 设置是否隐藏隐私栏勾选框，默认 false                                     |
| isPrivacyTextGravityCenter:bool                            | 设置隐私栏文案换行后是否居中对齐，如果为true则居中对齐，否则左对齐，默认 false |
| checkBoxGravity:int                                        | 设置隐私栏勾选框与文本协议对齐方式，可选择顶部（48），居中（17），底部（80）等 |
| checkBoxWith:int                                           | 设置隐私栏复选框宽度，单位 dp|
| checkBoxHeight:int                                         | 设置隐私栏复选框高度，单位 dp |
| checkedImageName:string                                    | 设置隐私栏复选框选中时的图片资源，图标资源放在 Assets/plugins/Android/CustomAndroidResource.androidlib/res/drawable 目录下，这里配置图标名字 |
| unCheckedImageName:string                                  | 设置隐私栏复选框未选中时的图片资源，图标资源放在 Assets/plugins/Android/CustomAndroidResource.androidlib/res/drawable 目录下，这里配置图标名字 |
| privacyTextStart:string                                    | 设置隐私栏声明部分起始文案 。如：隐私栏声明为"登录即同意《隐私政策》和《中国移动认证条款》且授权易盾授予本机号码"，则可传入"登录即同意" |
| privacyTextStartSize:float                                 | 设置隐私栏声明部分起始文案大小                                         |
| privacyLineSpacingAdd:float                                | 设置隐私文本行间距                                        |
| privacyLineSpacingMul:float                                | 设置隐私文本行间距倍数                                         |
| protocolConnect:string                                     | 设置运营商协议与自定义隐私栏协议连接符"和"                                |
| userProtocolConnect:string                                 | 设置自定义隐私栏协议之间连接符"、"                                |
| isOperatorPrivacyAtLast:bool                               | 设置运营商协议的位置是否在末尾 ，默认 false                               |
| privacyTextStartSize:float                                 | 设置隐私栏声明部分起始文案大小                                         |
| isHidePrivacySmh:bool                                      | 是否隐藏运营商协议书名号，默认 false                                          |
| protocolText:string                                        | 设置隐私栏协议文本                                           |
| protocolLink:string                                        | 设置隐私栏协议链接                                           |
| protocol2Text:string                                       | 设置隐私栏协议 2 文本                                          |
| protocol2Link:string                                       | 设置隐私栏协议 2 链接                                          |
| protocol3Text:string                                       | 设置隐私栏协议 3 文本                                          |
| protocol3Link:string                                       | 设置隐私栏协议 3 链接                                          |
| privacyTextEnd:string                                      | 设置隐私栏声明部分尾部文案。如：隐私栏声明为"登录即同意《隐私政策》和《中国移动认证条款》且授权易盾授予本机号码"，则可传入"且授权易盾授予本机号码" |
| privacyDialogWidth:int                                     | 协议未勾选隐私弹窗宽度                                         |
| privacyDialogHeight:int                                    | 协议未勾选隐私弹窗高度                                          |
| privacyDialogBg:string                                     |  协议未勾选隐私弹窗背景                                          |
| privacyDialogTitle:string                                  |  协议未勾选隐私弹窗标题                                          |
| privacyDialogTitleSize:float                               | 协议未勾选隐私弹窗标题字体大小                                         |
| privacyDialogTitleColor:string                             | 协议未勾选隐私弹窗标题颜色                                          |
| privacyDialogTitleMarginTop:int                            |  协议未勾选隐私弹窗标题距离顶部的距离                                          |
| privacyDialogTitleBold:bool                                | 协议未勾选隐私弹窗标题是否加粗                                          |
| privacyDialogContentStart:string                           |  协议未勾选隐私弹窗开始文本                                        |
| privacyDialogContentEnd:string                             | 协议未勾选隐私弹窗结束文本                                          |
| privacyDialogContentBold:bool                              | 协议未勾选隐私弹窗文本是否加粗                                          |
| privacyDialogContentMarginLeft:int                         | 协议未勾选隐私弹窗文本距离左边的距离                                          |
| privacyDialogContentMarginRight:int                        | 协议未勾选隐私弹窗文本距离右边的距离                                         |
| privacyDialogContentMarginTop:int                          | 协议未勾选隐私弹窗文本距离顶部的距离                                         |
| privacyDialogBtnTextSize:float                             | 协议未勾选隐私弹窗按钮文本大小                                          |
| privacyDialogBtnTextBold:bool                              | 协议未勾选隐私弹窗按钮文本是否加粗                                          |
| privacyDialogBtnWidth:int                                  | 协议未勾选隐私弹窗按钮宽度                                          |
| privacyDialogBtnHeight:int                                 | 协议未勾选隐私弹窗按钮高度                                          |
| privacyDialogBtnMarginLeft:int                             |  协议未勾选隐私弹窗按钮距离左边距离                                  |
| privacyDialogBtnMarginRight:int                            | 协议未勾选隐私弹窗按钮距离右边距离                                         |
| privacyDialogBtnMarginTop:int                              |  协议未勾选隐私弹窗按钮距离顶部距离                                       |
| privacyDialogBtnMarginBottom:int                           | 协议未勾选隐私弹窗按钮距离底部距离                                          |
| privacyDialogBtnAgreeText:string                           | 协议未勾选隐私弹窗按钮同意文本                                          |
| privacyDialogBtnAgreeTextColor:string                      |  协议未勾选隐私弹窗按钮同意文本颜色                                          |
| privacyDialogBtnAgreeBg:string                             | 协议未勾选隐私弹窗按钮同意文本背景                                         |
| privacyDialogBtnDisagreeText:string                        |  协议未勾选隐私弹窗按钮拒绝文本                                          |
| privacyDialogBtnDisagreeTextColor:string                   | 协议未勾选隐私弹窗按钮拒绝文本颜色                                         |
| privacyDialogBtnDisagreeBg:string                          | 协议未勾选隐私弹窗按钮拒绝文本背景                                          |
| isPrivacyDialogAuto:bool                                   | 协议未勾选弹窗点击是否自动登录，默认 false                                    |
| privacyDialogText:string                                   | 协议未勾选弹窗自定义message                                          |
| privacyDialogTextSize:float                                | 协议未勾选弹窗文本字体大小                                         |

##### 协议详情 Web 页面导航栏

| 配置项                                                        | 说明                                                  |
|:-----------------------------------------------------------| --------------------------------------------------- |
| protocolNavTitleCm:string                                  | 设置移动协议 Web 页面导航栏标题，需要配合protocolNavTitleCu和protocolNavTitleCt一起使用|
| protocolNavTitleCu:string                                  | 设置联通协议 Web 页面导航栏标题，需要配合protocolNavTitleCm和protocolNavTitleCt一起使用|
| protocolNavTitleCt:string                                  | 设置电信协议 Web 页面导航栏标题，需要配合protocolNavTitleCm和protocolNavTitleCu一起使用|
| protocolNavBackIcon:string                                 | 设置协议 Web 页面导航栏返回图标，图标资源放在 Assets/plugins/Android/CustomAndroidResource.androidlib/res/drawable 目录下，这里配置图标名字 |
| protocolNavColor:string                                    | 设置协议Web页面导航栏颜色                                    |
| protocolNavTitleColor:string                               | 协议Web页面导航栏标题颜色                                    |
| protocolNavHeight:int                                      | 设置协议 Web 页面导航栏高度                                    |
| protocolNavTitleSize:int                                   | 设置协议Web页面导航栏标题大小，单位 px                        |
| protocolNavTitleDpSize:int                                 | 设置协议 Web 页面导航栏标题大小，单位 dp                        |
| protocolNavBackIconWidth:int                               | 设置协议 Web 页面导航栏返回按钮宽度，单位 dp                    |
| protocolNavBackIconHeight:int                              | 设置协议 Web 页面导航栏返回按钮高度，单位 dp                    |
| protocolNavBackIconMargin:int                              | 设置协议 Web 页面导航栏返回按钮距离左边距离，单位 dp                    |
| protocolNavTitleBold:bool                                  | 设置协议 Web 页面导航栏标题是否加粗                    |

##### 其他

| 配置项                         | 说明                                                                                     |
|:----------------------------|----------------------------------------------------------------------------------------|
| backgroundImage:string      | 设置登录页面背景，图片资源放在 Assets/plugins/Android/CustomAndroidResource.androidlib/res/drawable 目录下，这里配置图片名字                       |
| backgroundGif:string        | 设置登录页面背景为 Gif，Gif 资源需要放置到Assets/plugins/Android/CustomAndroidResource.androidlib/res/drawable 目录下，传入资源名称即可             |
| backgroundVideo:string      | 设置登录页面背景为视频，视频放在 Assets/plugins/Android/CustomAndroidResource.androidlib/res/raw 文件夹下，这里配置视频文件名字。必须同时配置 backgroundVideo |
| backgroundVideoImage:string | 设置视频背景时的预览图，图片放在 Assets/plugins/Android/res/drawable 下，这里配置图标名字，配合 backgroundVideo 使用  |
| enterAnimation:string       | 设置授权页进场动画，enterAnimation 进场动画xml无后缀文件名。放置在 Assets/plugins/Android/CustomAndroidResource.androidlib/res/anim 目录下         |
| exitAnimation:string        | 设置授权页退出动画，exitAnimation 进场动画xml无后缀文件名。放置在 Assets/plugins/Android/CustomAndroidResource.androidlib/res/anim 目录下          |
| isLandscape:bool            | 是否横屏，默认 false                                                                                   |
| isDialogMode:bool           | 是否弹窗模式，默认 false                                                                                 |
| dialogWidth:int             | 授权页弹窗宽度，单位 dp                                                                          |
| dialogHeight:int            | 授权页弹窗高度，单位 dp                                                                          |
| dialogX:int                 | 授权页弹窗 X 轴偏移量，以屏幕中心为原点                                                                  |
| dialogY:int                 | 授权页弹窗 Y 轴偏移量，以屏幕中心为原点                                                                  |
| isBottomDialog:bool         | 授权页弹窗是否贴于屏幕底部<br>true：显示在屏幕底部，dialogY 失效<br> false：不显示在屏幕底部，以 dialogY 参数为准，默认 false             |
| isProtocolDialogMode:bool   | 协议详情页是否开启弹窗模式，默认 false                                                                          |
| isShowLoading:bool           | 授权页授权登录是否显示loading，默认 false                                                                     |
| backPressedAvailable:bool   | 授权页物理返回键是否可用，默认 false                                                                     |
| virtualButtonHidden:bool    | 是否隐藏虚拟按键，默认 false                                                                          |

##### 自定义view

| 配置项                       | 说明                                                         |
|:--------------------------|------------------------------------------------------------|
| widgets:List<Widget>      | 自定义view数组                                                  |
|  ∟ viewId:string          | 控件 id                                                      |
|  ∟ type:string            | 控件类型，可选值为 TextView、Button、ImageView                        |
|  ∟ top:int                | 控件距离顶部的偏移，单位 dp                                            |
|  ∟ left:int               | 控件距离左侧的偏移，单位 dp                                            |
|  ∟ right:int              | 控件距离右侧的偏移，单位 dp                                            |
|  ∟ bottom:int             | 控件距离底部的偏移，和top互斥，单位 dp                                     |
|  ∟ width:int              | 控件宽度，单位 dp，默认自适应内容                                         |
|  ∟ height:int             | 控件高度，单位 dp，默认自适应内容                                         |
|  ∟ text:string            | 控件文本                                                       |
|  ∟ textSize:int           | 控件文本大小，单位 px                                               |
|  ∟ isGravityCenter:bool   | 文本内容是否居中，默认 false                                             |
|  ∟ textColor:string       | 控件文本颜色，十六进制颜色码                                             |
|  ∟ backgroundColor:string | 控件背景颜色，十六进制颜色码                                             |
|  ∟ backgroundImage:string | 控件背景图片，图片放在 Assets/plugins/Android/res/drawable 下，这里配置图片名字 |
|  ∟ positionType:int       | 添加控件的位置类型，1表示位于导航栏部分，0表示位于导航栏下方的body部分，默认为0                |

自定义 view 的点击事件回调到 CustomViewListener 脚本中

```
public class CustomViewListener : AndroidJavaProxy
{
    public CustomViewListener() : base("com.netease.nis.quicklogin.utils.LoginUiHelper$CustomViewListener") { }

    public void onClick(AndroidJavaObject context, AndroidJavaObject view)
    {
        AndroidJavaObject tag = view.Call<AndroidJavaObject>("getTag");
        //获取的 tag 即前面设置的 viewId
    }
}
```

#### 授权页 view 的点击事件回调到 ClickEventListener 中。viewType 为 1 时表示隐私协议，2 表示复选框，3 表示左上角返回按钮，4 表示登录按钮。当 viewType 为 2 或 4 时，code 字段为1 则表示复选框勾选，为 0 则表示复选框未勾选

```
public class ClickEventListener : AndroidJavaProxy
{
    public ClickEventListener() : base("com.netease.nis.quicklogin.listener.ClickEventListener") { }

    public void onClick(int viewType, int code)
    {
        Debug.Log("被点击的view为：" + viewType + "协议复选框状态为：" + code);
    }
}

```

### 取号

```
OnPassLogin()
```
即打开授权页，取号的回调在 QuickpassCallback()中。取号之前务必设置授权页样式，否则打开的是默认的授权页

```
public class QuickpassCallback : AndroidJavaProxy
{
    public QuickpassCallback() : base("com.netease.nis.quicklogin.listener.QuickLoginTokenListener") { }
    public void onGetTokenSuccess(string YDToken, string accessCode)
    {
        // 取号成功，YDToken：易盾token accessCode：运营商校验码。这两个参数用于从服务端获取真实手机号
        Debug.Log("onGetTokenSuccess" + YDToken);
        Debug.Log("onGetTokenSuccess" + accessCode);
        QuickpassHandler.CloseLoginAuthView();
    }

    public void onGetTokenError(string YDToken, string msg)
    {
        // 取号失败 msg 中有详细的失败信息
        Debug.Log("onGetTokenError" + YDToken);
        Debug.Log("onGetTokenError" + msg);
        QuickpassHandler.CloseLoginAuthView();
    }

    public void onCancelGetToken()
    {
        // 取消取号，包括点击返回按钮和物理返回键
        Debug.Log("onCancelGetToken");
    }
}

```

### 关闭授权页

```
CloseLoginAuthView()
```

## iOS

### 初始化SDK

```
init(businessId,timeout);

```

#### 参数说明：
*   入参说明：

    |参数|类型|是否必填|默认值|描述|
    |----|----|--------|------|----|
    | businessId | String | 是 | 无 | 易盾分配的业务 id |
    | timeout | int |否| 3 |运营商预取号和授权登录接口的超时时间，单位秒|

### 预取号

```
/// 预取号调用
PreFetchNumberHandler handler = new PreFetchNumberHandler(preFetchNumberHandler);
IntPtr fp = Marshal.GetFunctionPointerForDelegate(handler);
preFetchNumber(fp);

 /// 预取号值的回调
[AOT.MonoPInvokeCallback(typeof(PreFetchNumberHandler))]
static void preFetchNumberHandler (string resultStr) {
    Debug.Log(resultStr);
}
```

#### 参数说明：
*  回调参数说明：

    |回调参数|类型|描述|
    |----|----|----|
    | success | Boolean |预取号是否成功|
    | token | String |如果预取号成功则返回易盾 token，否则无此字段，有效期2分钟|
    | securityPhone | String |手机掩码|
    | desc | String |预取号成功信息描述|

### 设置授权页UI

授权页面的 ios-light-config.json 放到 Xcode工程的 Resources 下; iOS 资源图片，放到iOS Xcode 工程的 Images.xcassets 中

```
StreamReader sr = new StreamReader(Application.dataPath + "/Resources/ios-light-config.json");
string uiConfig = sr.ReadToEnd();
string json = JsonUtility.ToJson(uiConfig);
setupUiConfig(json);

// 授权页面UI事件回调
[UnmanagedFunctionPointer(CallingConvention.Cdecl)]
public delegate void UiConfigHandler(string resultString);
    
[AOT.MonoPInvokeCallback(typeof(UiConfigHandler))]
static void uiConfigHandler (string resultStr) {
    Debug.Log(resultStr);
}

```

*  回调参数说明：

    |回调参数|类型|描述|
    |----|----|----|
    | action | String |appDPrivacy 表示点击了默认协议<br>appFPrivacy 表示点击了议第一个协议点击 <br> appSPrivacy 表示点击了第二个协议 <br> loginAction 表示点击了登录按钮，data.checked = true 表示在点击登录按钮时复选框选已选中反之<br> checkedAction 表示点击了复选框，data.checked = true 表示复选框已选中反之<br>其他自定义的action|

###  取号，即打开授权页

注：设置授权页UI和取号接口，都要在预取号成功的回调之后执行。

```
/// 打开授权页面
OnPassLoginHandler handler = new OnPassLoginHandler(onPassLoginHandler);
IntPtr fp = Marshal.GetFunctionPointerForDelegate(handler);
OnPassLogin(fp);

/// 点击登录按钮，回调值
static void onPassLoginHandler (string resultStr) {
Debug.Log(resultStr);
}

```

#### 参数说明：
*  回调参数说明：

    |回调参数|类型|描述|
    |----|----|----|
    | success | Boolean |取号是否成功|
    | accessToken | String |如果取号成功则返回运营商 token，否则无此字段|
    | resultCode | String |运营商返回的请求码|
    | desc | String |取号成功信息描述|
    
###  关闭授权页

```
closeAuthController()

```


#### config 可配置项说明： iOS版

设计规范概览
**<font color=red>开发者不得通过任何技术手段，将授权页面的隐私栏、手机掩码号、供应商品牌内容隐藏、覆盖</font>**<br>
**<font color=red>网易易盾与运营商会对应用授权页面进行审查，若发现上述违规行为，网易易盾有权将您的一键登录功能下线</font>**
![iOS设计规范](https://nos.netease.com/cloud-website-bucket/58fca2df814059b54171724b7702b06f.jpg)
![自定义展示图](https://nos.netease.com/cloud-website-bucket/410d6012173c5531b1065909c9484d36.jpg)

##### 基础配置
| 属性 | 说明 |
| :-------- | -------- |
| backgroundColor   |设置授权页面背景颜色|
| authWindowPop | 设置窗口类型<br>0 表示全屏模式<br> 1 表示窗口在屏幕的中间<br> 2 表示窗口在屏幕的底部(不支持横屏)|
| faceOrientation   |设置授权页面方向<br> 0 表示设备方向未知<br>1 表示设置保持直立<br>2 表示设备上下颠倒 <br>3 表示设备向左旋转 <br> 4 表示设备向右旋转 |
| bgImage   |设置授权转背景图片，例如 ："图片名.后缀"|
| contentMode   |设置背景图片显示模式 0 表示 UIViewContentModeScaleToFill，1表示UIViewContentModeScaleAspectFit ，2表示UIViewContentModeScaleAspectFill|


##### 转场动画
| 属性 | 说明 |
| :-------- | -------- |
| modalTransitionStyle | 设置授权转场动画<br> 0 表示下推<br>1 表示翻转<br>2 表示淡出|

##### 自定义控件
#### 事例,注意：授权页面的图片需放到iOS项目 Assets.xcassets 中

```
"widgets": [
        {
            "type": "UIButton",
            "image": "weixin",
            "title": "",    
            "titleColor": "#000000",
            "titleFont": 12,
            "cornerRadius": 20,
            "action": "handleCustomEvent1",
            "frame": {"mainScreenLeftDistance":70,"mainScreenTopDistance":340,"width":40,"height":40},
            "backgroundImage":""
        },
        {
            "type": "UIButton",
            "image": "qq",
            "title": "",    
            "titleColor": "#FFFFFF",
            "titleFont": 12,
            "cornerRadius": 20,
            "action": "handleCustomEvent2",
            "frame": {"mainScreenCenterXWithLeftDistance":0,"mainScreenTopDistance":340,"width":40,"height":40},
            "backgroundImage": ""
        },
        {
            "type": "UIButton",
            "image": "weibo",
            "title": "",    
            "titleColor": "#FFFFFF",
            "titleFont": 12,
            "cornerRadius": 20,
            "action": "handleCustomEvent3",
            "frame": {"mainScreenRightDistance":70,"mainScreenTopDistance":340,"width":40,"height":40},
            "backgroundImage": ""
        },
        {
            "type": "UIButton",
            "image": "",
            "title": "其他登录方式",
            "titleColor": "#000000",
            "titleFont": 14,
            "cornerRadius": 20,
            "action": "handleCustomLabel",
            "backgroundImage": "login_btn_normal",
            "backgroundColor": "#000000",
            "frame": {"mainScreenLeftDistance":80,"mainScreenRightDistance":80,"mainScreenTopDistance":280,"height":40}
        },
        {
            "type": "UILabel",
            "textColor": "#FFFFFF",
            "font": 15,
            "cornerRadius": 20,
            "action": "handleCustomLabel1",
            "text": "其他登录方式",
            "textAlignment": 1,
            "backgroundColor": "#000000",
            "frame": {"mainScreenLeftDistance":80,"mainScreenRightDistance":80,"mainScreenBottomDistance":400,"height":40}
        }
    ]
```

| 配置项                                            | 说明                                 |
| :---------------------------------------------- | ------------------------------------ |
| widgets:JsonArray                   | 自定义view数组        |
|  ∟ type:String          |控件类型，可选值为 UILabel、UIButton|
|  ∟ image:String       |UIButton显示的图片。内容为图片名，不需要加图片后缀|
|  ∟ title:String       |UIButton显示的文字|
|  ∟ titleColor:String  |UIButton显示的字体颜色|
|  ∟ titleFont:int      |字体的大小|
|  ∟ cornerRadius:int   |控件的圆角|
|  ∟ backgroundImage:String  |UIButton的背景图片|
|  ∟ backgroundColor:String  | 控件背景颜色|
|  ∟ mainScreenLeftDistance:int |距离屏幕左边的距离，默认为0 |
|  ∟ mainScreenRightDistance:int |距离屏幕右边的距离，默认为0 |
|  ∟ mainScreenTopDistance:int |距离屏幕顶部的距离，默认为0 |
|  ∟ mainScreenCenterXWithLeftDistance:int |为0时，居中显示。大于0，向屏幕左侧偏移。小于0，向右侧偏移|
|  ∟ width:int          |控件的宽度，默认为0 |
|  ∟ height:int         |控件的高度，默认为0 |
|  ∟ textAlignment:int  |0，文本左对齐。1，文本居中显示。2文本右对齐|
|  ∟ text:String        |UILabel显示的文字|
|  ∟ textColor:String   |UILabel的字体颜色|
|  ∟ action:String      |设置可点击控件的点击事件，在监听中回调。详见事件监听 |

##### 背景设置视频

| 属性 | 说明 |
| :-------- | -------- |
| localVideoFileName | 设置视频本地名称 例如xx.mp4* |
| isRepeatPlay   | 设置是否重复播放视频，YES 表示重复播放，NO 表示不重复播放|
| videoURL   | 设置网络视频的地址|

##### 背景设置 Gif

| 属性 | 说明 |
| :-------- | -------- |
| animationRepeatCount | 设置动画重复的次数 -1无限重复 |
| animationImages   | 设置图片数组|
| animationDuration   | 设置动画的时长|

##### 状态栏
| 属性                                              | 说明                                                         |
| :-------- | -------- |
| statusBarStyle | 设置状态栏样式<br> iOS13之前 0表示文字黑色，1表示文字白色<br> iOS13之后 0表示自动选择黑色或白色，3 表示文字黑色，2 表示文字白色|

##### 导航栏

| 属性                                              | 说明                                                         |
| :-------- | -------- |
| navBarHidden | 导航栏是否隐藏 |
| navBgColor   | 设置导航栏背景颜色 |
| navText      | 设置导航栏标题 |
| navTextFont  | 设置导航栏标题字体大小|
| navTextColor | 设置导航栏标题字体颜色|
| navTextHidden| 设置导航栏标题是否隐藏，默认不隐藏|
| navReturnImg | 设置导航返回图标，例如："back-1" |
| navReturnImgLeftMargin | 设置导航返回图标距离屏幕左边的距离，默认0  |
| navReturnImgBottomMargin | 设置导航返回图标距离屏幕底部的距离，默认0 |
| navReturnImgWidth  | 设置导航返回图标的宽度，默认44 |
| navReturnImgHeight| 设置导航返回图标的高度 ,  默认44 |                                 |

##### 应用 Logo


| 属性                                              | 说明                                                         |
| :-------- | -------- |
| logoImg | 设置logo图片, 例如 ："图片名.后缀"]|
| logoWidth   | 设置logo图片宽度 |
| logoHeight  | 设置logo图片高度 |
| logoOffsetTopY  |设置logo图片沿Y轴偏移量， logoOffsetTopY为距离屏幕顶部的距离 ，默认为20|
| logoOffsetX | 设置logo图片沿X轴偏移量，logoOffsetX = 0居中显示|
| logoHidden| 设置logo图片是否隐藏，默认不隐藏|


##### 手机掩码

| 属性                                              | 说明                                                         |
| :-------- | -------- |
| numberColor | 设置手机号码字体颜色|
| numberFont   | 设置手机号码字体大小， 默认18 |
| numberOffsetTopY  | 设置手机号码沿Y轴偏移量，  numberOffsetTopY为距离屏幕顶部的距离 ，默认为100|
| numberOffsetX | 设置logo图片沿X轴偏移量，logoOffsetX = 0居中显示|
| numberHeight| 设置手机号码框的高度 默认27|
| numberBackgroundColor| 设置手机号码的背景颜色|
| numberCornerRadius| 设置手机号码的控件的圆角|
| numberLeftContent| 设置手机号码的左边描述内容，默认为空|
| numberRightContent| 设置手机号码的右边描述内容，默认为空色|


##### 认证品牌

| 属性                                              | 说明                                                         |
| :-------- | -------- |
| brandColor | 设置认证服务品牌文字颜色|
| brandBackgroundColor   | 设置认证服务品牌背景颜色|
| brandFont  | 设置认证服务品牌文字字体 默认12|
| brandWidth | 设置认证服务品牌的宽度， 默认200|
| brandHeight| 设置认证服务品牌的高度， 默认16|
| brandOffsetX| 设置认证服务品牌X偏移量 ，brandOffsetX = 0居中显示|
| brandOffsetTopY| 设置认证服务品牌Y偏移量, brandOffsetTopY为距离屏幕顶部的距离 ，默认为150|
| brandHidden| 设置是否隐藏认证服务品牌，默认显示|

##### 登录按钮


| 属性                                              | 说明                                                         |
| :-------- | -------- |
| logBtnText | 设置登录按钮文本|
| logBtnTextFont   | 设置登录按钮字体大小|
| logBtnTextColor  | 设置登录按钮文本颜色|
| logBtnOffsetTopY | 设置登录按钮Y偏移量 ，logBtnOffsetTopY为距离屏幕顶部的距离 ，默认为200|
| logBtnRadius| 设置登录按钮圆角，默认8|
| logBtnUsableBGColor| 设置登录按钮背景颜色|
| logBtnEnableImg| 设置登录按钮可用状态下的背景图片|
| logBtnHighlightedImg| 登录按钮高亮状态下的背景图片|
| logBtnOriginLeft| 登录按钮的左边距 ，横屏默认40 ，竖屏默认260|
| logBtnOriginRight| 设置登录按钮的左边距，横屏默认40 ，竖屏默认260|
| logBtnHeight| 设置登录按钮的高度，默认44|

##### 隐私协议

若勾选框需要展示，请务必设置勾选框的选中态图片与未选中态图片
协议未勾选时，登录按钮是否可点击可以自定义设置，弹窗提示的样式也可以自定义

| 属性                                              | 说明                                                         |
| :-------- | -------- |
| unCheckedImageName | 例如：static/图片名.后缀|
| checkedImageName | 例如：static/图片名.后缀|
| checkboxWH| 设置复选框大小（只能正方形) ，默认 12|
| privacyState| 设置复选框默认状态 默认:NO |
| checkBoxAlignment| 设置隐私条款check框位置 <br> 0 表示相对协议顶对齐<br> 1 表示相对协议中对齐 <br> 2 表示相对协议下对齐 默认顶对齐|
| checkedSelected| 设置复选框勾选状态，YES:勾选，NO:取消勾选状态|
| checkBoxMargin| 设置复选框距离隐私条款的边距 默认 8|
| appPrivacyOriginLeftMargin| 设置隐私条款距离屏幕左边的距离 默认 60|
| appPrivacyOriginRightMargin| 设置隐私条款距离屏幕右边的距离 默认 40|
| appPrivacyOriginBottomMargin| 设置隐私条款距离屏幕的距离 默认 40|
| privacyNavReturnImg| 设置用户协议界面，导航栏返回图标，默认用导航栏返回图标|
| appPrivacyText| 设置隐私的内容模板：全句可自定义但必须保留"《默认》"字段表明SDK默认协议,否则设置不生效。必设置项（参考SDK的demo）appPrivacyText设置内容：登录即同意《默认》并授权获得《用户政策》和《用户隐私协议》以及《用户行为准则》和《用户相关条令》 |
| appFPrivacyText| 设置开发者隐私条款协议名称（第一个协议）|
| appFPrivacyURL| 设置开发者隐私条款协议url（第一个协议）|
| appSPrivacyText| 设置开发者隐私条款协议名称（第二个协议）|
| appSPrivacyURL| 设置开发者隐私条款协议url（第二个协议）|
| appTPrivacyText| 设置开发者隐私条款协议名称（第三个协议）|
| appTPrivacyURL| 设置开发者隐私条款协议url（第三个协议）|
| appFourPrivacyText| 设置开发者隐私条款协议名称（第四个协议）|
| appFourPrivacyURL| 设置开发者隐私条款协议url（第四个协议）|
| shouldHiddenPrivacyMarks| 设置是否隐藏"《默认》" 两边的《》，默认不隐藏|
| privacyColor| 设置隐私条款名称颜色|
| privacyFont| 设置隐私条款字体的大小|
| protocolColor| 设置协议条款协议名称颜色|
| appPrivacyLineSpacing| 设置隐私协议的行间距, 默认是1|
| appPrivacyWordSpacing| 设置隐私协议的字间距, 默认是0|
| progressColor| 设置用户协议界面，进度条颜色|

##### 弹窗模式

| 属性                                              | 说明                                                         |
| :-------- | -------- |
| popBackgroundColor   | 设置窗口模式的背景颜色|
| authWindowWidth  | 设置弹窗的宽度，竖屏状态下默认是 300，横屏状态下默认是 335 |
| authWindowHeight | 设置弹窗高度，竖屏状态下默认是335， 横屏状态下默认是300  ⚠️底部半屏弹窗模式的高度可通过修改 authWindowHeight，调整高度 默认335pt|
| closePopImg| 设置弹窗模式下关闭按钮的图片，⚠️(必传)|
| closePopImgWidth| 设置弹窗模式下关闭按钮图片的宽度 默认20*|
| closePopImgHeight| 设置弹窗模式下关闭按钮图片的高度 默认20|
| closePopImgOriginY| 设置关闭按钮距离顶部的距离，默认距离顶部10，距离 = 10 + closePopImgOriginY|
| closePopImgOriginX| 设置关闭按钮距离父视图右边的距离，默认距离为10，距离 = 10 + closePopImgOriginX|
| authWindowCenterOriginY| 设置居中弹窗沿Y轴移动的距离。例如 ：authWindowCenterOriginY = 10 表示中间点沿Y轴向下偏移10个像素|
| authWindowCenterOriginX| 设置居中弹窗沿X轴移动的距离。例如 ：authWindowCenterOriginX = 10 表示中间点沿X轴向右偏移10个像素|
| popCenterCornerRadius| 设置居中弹窗模式下，弹窗的圆角，默认圆角为16|
| popBottomCornerRadius| 设置底部弹窗模式下，弹窗的圆角，默认圆角为16，注：只可修改顶部左右二边的值|
| isOpenSwipeGesture| 设置底部弹窗模式下，是否开启轻扫手势，向下轻扫关闭弹窗。默认关闭|
