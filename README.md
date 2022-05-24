# 号码认证对应的 Unity package 工程

## 使用方法

下载并解压出 quickpass-plugin-u3d.unitypackage，在 Assets 目录右键选择 Import Package 导入 quickpass-plugin-u3d.unitypackage 资源包

其中 TestBehaviourScript.cs 是调用示例代码

## 所有 Api

- Init(string businessId, int timeout = 6000, bool debug = false)

初始化 

businessId：业务id

timeout：预取号超时时间

debug：是否开启 debug 日志打印

- SetUiConfig(QuickpassUiConfig uiConfig)

设置授权页样式

### Android

QuickpassUiConfig 是可配置项，具体的配置项看注释

```
public struct QuickpassUiConfig
{
    public string statusBarColor; // 状态栏颜色
    public bool isStatusBarDarkColor;// 设置状态栏字体图标颜色是否为暗色(黑色)
    public string navBackIcon;// 导航栏返回按钮
    public int navBackIconWidth;// 导航栏返回按钮宽
    public int navBackIconHeight;// 导航栏返回按钮高
    public bool isHideBackIcon; // 是否隐藏导航栏返回按钮
    public int navHeight; // 导航栏高度
    public string navBackgroundColor; // 导航栏背景颜色
    public string navTitle; // 导航栏标题
    public int navTitleSize;// 导航栏标题字体大小
    public bool isNavTitleBold; // 导航栏标题是否为粗体
    public string navTitleColor; // 导航栏标题颜色
    public bool isHideNav; // 是否隐藏导航栏
    public string logoIconName; // 应用 logo 图标
    public int logoWidth; // logo宽度
    public int logoHeight; //  logo 高度
    public int logoTopYOffset; //  logo 顶部 Y 轴偏移
    public int logoBottomYOffset; //  logo 距离屏幕底部偏移
    public int logoXOffset; //  logo 水平方向的偏移
    public bool isHideLogo; // 是否隐藏 logo
    public string maskNumberColor; // 手机掩码颜色
    public int maskNumberSize; // 手机掩码字体大小
    public int maskNumberDpSize; // 手机掩码字体大小 dp
    public int maskNumberTopYOffset; // 手机掩码顶部Y轴偏移
    public int maskNumberBottomYOffset; // 手机掩码距离屏幕底部偏移
    public int maskNumberXOffset; // 手机掩码水平方向的偏移
    public int sloganSize; // 认证品牌字体大小
    public int sloganDpSize; // 认证品牌字体大小 dp
    public string sloganColor; // 认证品牌颜色
    public int sloganTopYOffset; // 认证品牌顶部 Y 轴偏移
    public int sloganBottomYOffset; // 认证品牌距离屏幕底部偏移
    public int sloganXOffset; // 认证品牌水平方向的偏移
    public string loginBtnText; // 登录按钮文本
    public int loginBtnTextSize; // 登录按钮文本字体大小
    public int loginBtnTextDpSize; // 登录按钮文本字体大小 dp
    public string loginBtnTextColor; // 登录按钮文本颜色
    public int loginBtnWidth; // 登录按钮宽度
    public int loginBtnHeight; // 登录按钮高度
    public string loginBtnBackgroundRes; // 登录按钮背景图标
    public int loginBtnTopYOffset; // 登录按钮顶部Y轴偏移
    public int loginBtnBottomYOffset; // 登录按钮距离屏幕底部偏移
    public int loginBtnXOffset; // 登录按钮水平方向的偏移
    public string privacyTextColor; // 隐私栏文本颜色，不包括协议
    public string privacyProtocolColor; // 隐私栏协议颜色 
    public int privacySize; // 隐私栏区域字体大小
    public int privacyDpSize; // 隐私栏区域字体大小 dp
    public int privacyTopYOffset; // 隐私栏顶部Y轴偏移
    public int privacyBottomYOffset; // 隐私栏距离屏幕底部偏移
    public int privacyTextMarginLeft; // 隐私栏文本和复选框的距离
    public int privacyMarginLeft; // 设置隐私栏左侧边距
    public int privacyMarginRight; // 设置隐私栏右侧边距
    public bool privacyState; // 隐私栏协议复选框勾选状态
    public bool isHidePrivacySmh; // 是否隐藏隐私协议书名号《》
    public bool isHidePrivacyCheckBox; // 是否隐藏隐私栏勾选框
    public bool isPrivacyTextGravityCenter; // 协议文本是否居中
    public int checkBoxGravity; // 隐私栏勾选框与文本协议对齐方式
    public string checkedImageName; // 隐私栏复选框选中时的图片资源
    public string unCheckedImageName; // 隐私栏复选框未选中时的图片资源
    public string privacyTextStart; // 隐私栏声明部分起始文案
    public string protocolText; // 设置隐私栏协议文本
    public string protocolLink; // 设置隐私栏协议链接
    public string protocol2Text; // 设置隐私栏协议 2 文本
    public string protocol2Link;  // 设置隐私栏协议 2 链接
    public string privacyTextEnd; // 隐私栏声明部分尾部文案
    public string protocolNavTitle; // 协议 Web 页面导航栏标题
    public string protocolNavBackIcon; // 协议 Web 页面导航栏返回图标
    public int protocolNavHeight; // 协议 Web 页面导航栏高度
    public string protocolNavTitleColor; // 协议Web页面导航栏标题颜色
    public int protocolNavTitleSize; // 协议Web页面导航栏标题大小
    public int protocolNavTitleDpSize; // 协议Web页面导航栏标题大小 dp
    public int protocolNavBackIconWidth; // 协议 Web 页面导航栏返回按钮宽度
    public int protocolNavBackIconHeight; // 协议 Web 页面导航栏返回按钮高度
    public string protocolNavColor; // 协议Web页面导航栏颜色
    public string backgroundImage; // 登录页面背景
    public string backgroundGif; // 登录页面背景为 Gif
    public string backgroundVideo; // 登录页面背景为视频
    public string backgroundVideoImage; // 视频背景时的预览图
    public bool isLandscape; // 是否横屏
    public bool isDialogMode; // 是否弹窗模式
    public int dialogWidth; // 授权页弹窗宽度
    public int dialogHeight; // 授权页弹窗高度
    public int dialogX; // 授权页弹窗 X 轴偏移量，以屏幕中心为原点
    public int dialogY; // 授权页弹窗 Y 轴偏移量，以屏幕中心为原点
    public bool isBottomDialog; // 授权页弹窗是否贴于屏幕底部
};
```
图片资源放在 Assets/plugins/Android/res/drawable 目录下

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

```

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

#### config 可配置项说明： iOS版

设计规范概览
**<font color=red>开发者不得通过任何技术手段，将授权页面的隐私栏、手机掩码号、供应商品牌内容隐藏、覆盖</font>**<br>
**<font color=red>网易易盾与运营商会对应用授权页面进行审查，若发现上述违规行为，网易易盾有权将您的一键登录功能下线</font>**
![iOS设计规范](https://nos.netease.com/cloud-website-bucket/58fca2df814059b54171724b7702b06f.jpg)
![自定义展示图](https://nos.netease.com/cloud-website-bucket/410d6012173c5531b1065909c9484d36.jpg)

##### 基础配置
| 属性 | 说明 |
| :-------- | -------- |
| presentDirectionType   | presentDirectionType = 1 表示从底部弹出|
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
| 属性 | 说明 |
| :-------- | -------- |
| widgets | 设置授权界面自定义控件<br>例如 ： "widgets": [
        {
            "type": "UIButton", 
            "UIButtonType": 0, 
            "image": "static/weixin.png",
            "title": "",    
            "titleColor": "#000000",
            "titleFont": 12,
            "cornerRadius": 20,
            "action": "handleCustomEvent1",
            "frame": {"mainScreenLeftDistance":100,"mainScreenTopDistance":360,"width":32,"height":32},
            "backgroundImage":"static/yidun_logo.png"
        },
        {
            "type": "UIButton", 
            "UIButtonType": 0, 
            "image": "static/qq.png",
            "title": "",    
            "titleColor": "#FFFFFF",
            "titleFont": 12,
            "cornerRadius": 20,
            "action": "handleCustomEvent2",
            "frame": {"mainScreenCenterXWithLeftDistance":0,"mainScreenTopDistance":360,"width":32,"height":32},
            "backgroundImage": "static/yidun_logo.png"
        }]|

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
| appPrivacyText| 设置隐私的内容模板：全句可自定义但必须保留"《默认》"字段表明SDK默认协议,否则设置不生效。必设置项（参考SDK的demo）appPrivacyText设置内容：登录并同意《默认》和易盾协议1、网易协议2登录并支持一键登录，展示：登录并同意中国移动条款协议和易盾协议1、网易协议2登录并支持一键登录 |
| appFPrivacyText| 设置开发者隐私条款协议名称（第一个协议）|
| appFPrivacyURL| 设置开发者隐私条款协议url（第一个协议）|
| appSPrivacyText| 设置开发者隐私条款协议名称（第二个协议）|
| appSPrivacyURL| 设置开发者隐私条款协议url（第二个协议）|
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


