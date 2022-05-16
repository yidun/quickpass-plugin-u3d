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

### iOS 

QuickpassHandler.setIOSUiConfig(json); 

预取号

- PreFetchNumber()

打开授权页

- OnPassLogin()



