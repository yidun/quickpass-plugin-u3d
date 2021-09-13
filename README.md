# 号码认证对应的 Unity package 工程

## 使用方法

下载并解压出 quickpass-plugin-u3d.unitypackage，在 Assets 目录右键选择 Import Package 导入 quickpass-plugin-u3d.unitypackage 资源包

其中 TestBehaviourScript.cs 是调用事例代码

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

### iOS 

QuickpassHandler.setIOSUiConfig(json); 

预取号

- PreFetchNumber()

打开授权页

- OnPassLogin()



