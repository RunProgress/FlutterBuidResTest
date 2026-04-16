# FlutterTestHybrid 仓库指南

## 仓库概览

FlutterTestHybrid 是一个结合了 Flutter 和 iOS 原生开发的混合项目框架，旨在帮助开发者在 iOS 应用中集成 Flutter 功能。

- **混合开发**：无缝集成 Flutter 和 iOS 原生代码
- **模块化设计**：清晰的目录结构，便于维护和扩展
- **CocoaPods 支持**：通过 CocoaPods 轻松集成到现有 iOS 项目

## 目录结构

```
├── Example/                 # 示例项目
│   ├── FlutterTestHybrid.xcodeproj/   # Xcode 项目文件
│   ├── FlutterTestHybrid.xcworkspace/ # Xcode 工作空间
│   ├── Pods/                # CocoaPods 依赖
│   ├── Tests/               # 测试文件
│   ├── Podfile              # Podfile 配置
│   └── Podfile.lock         # Podfile 锁定文件
├── FlutterTestHybrid/       # 主框架目录
│   ├── Assets/              # 资源文件
│   ├── Classes/             # 源代码
│   │   └── FlutterPluginRegistrant/  # Flutter 插件注册
│   └── Framework/           # 框架文件
│       ├── App.framework/   # Flutter 应用框架
│       └── Flutter.framework/ # Flutter 核心框架
├── .gitignore              # Git 忽略文件
├── .travis.yml             # Travis CI 配置
├── FlutterTestHybrid.podspec # CocoaPods 配置
├── LICENSE                 # 许可证文件
└── README.md               # 项目说明
```

## 核心组件

### 1. Flutter 框架集成

FlutterTestHybrid 包含了完整的 Flutter 框架，位于 `FlutterTestHybrid/Framework/` 目录下：

- **Flutter.framework**：Flutter 核心框架，提供 Flutter 运行时环境
- **App.framework**：包含编译后的 Flutter 应用代码和资源

### 2. 插件注册

`FlutterTestHybrid/Classes/FlutterPluginRegistrant/` 目录包含了 Flutter 插件的注册代码，确保 Flutter 插件能够在 iOS 原生环境中正常工作。

## 安装与集成

### 前提条件

- iOS 8.0 或更高版本
- Xcode 10.0 或更高版本
- CocoaPods 1.8.0 或更高版本

### 通过 CocoaPods 集成

1. 在你的 Podfile 中添加以下内容：

```ruby
pod 'FlutterTestHybrid'
```

2. 运行以下命令安装依赖：

```bash
pod install
```

3. 打开生成的 `.xcworkspace` 文件开始使用。

### 运行示例项目

1. 克隆仓库：

```bash
git clone https://github.com/zhangxiao/FlutterTestHybrid.git
cd FlutterTestHybrid
```

2. 进入 Example 目录并安装依赖：

```bash
cd Example
pod install
```

3. 打开 `FlutterTestHybrid.xcworkspace` 并运行示例应用。

## 使用指南

### 在 iOS 项目中集成 Flutter 视图

1. 导入必要的头文件：

```objective-c
#import <Flutter/Flutter.h>
```

2. 创建 Flutter 引擎和视图控制器：

```objective-c
// 创建 Flutter 引擎
FlutterEngine *flutterEngine = [[FlutterEngine alloc] initWithName:@"my flutter engine"];
[flutterEngine runWithEntrypoint:nil];

// 创建 Flutter 视图控制器
FlutterViewController *flutterViewController = [[FlutterViewController alloc] initWithEngine:flutterEngine nibName:nil bundle:nil];

// 推送或呈现 Flutter 视图控制器
[self.navigationController pushViewController:flutterViewController animated:YES];
```

### 原生与 Flutter 通信

FlutterTestHybrid 支持通过 MethodChannel 进行原生与 Flutter 之间的通信：

#### 在 iOS 原生代码中：

```objective-c
// 创建 MethodChannel
FlutterMethodChannel *channel = [FlutterMethodChannel methodChannelWithName:@"com.example.channel" binaryMessenger:flutterViewController.binaryMessenger];

// 设置方法处理
[channel setMethodCallHandler:^(FlutterMethodCall *call, FlutterResult result) {
    if ([call.method isEqualToString:@"getPlatformVersion"]) {
        result([@"iOS " stringByAppendingString:[[UIDevice currentDevice] systemVersion]]);
    } else {
        result(FlutterMethodNotImplemented);
    }
}];
```

#### 在 Flutter 代码中：

```dart
// 创建 MethodChannel
final MethodChannel _channel = MethodChannel('com.example.channel');

// 调用原生方法
Future<String> get platformVersion async {
  final String version = await _channel.invokeMethod('getPlatformVersion');
  return version;
}
```

## 开发与调试

### Flutter 代码开发

Flutter 代码通常位于单独的 Flutter 项目中，开发完成后通过 `flutter build ios-framework` 命令生成框架文件，然后替换到 `FlutterTestHybrid/Framework/` 目录。

### 调试技巧

1. **查看 Flutter 日志**：在 Xcode 控制台中查看 Flutter 输出的日志
2. **热重载**：在开发过程中使用 Flutter 的热重载功能加快开发速度
3. **性能监控**：使用 Flutter DevTools 监控应用性能

## 常见问题与解决方案

### 1. Flutter 框架版本不匹配

**问题**：运行时出现 Flutter 框架版本不匹配的错误

**解决方案**：确保使用的 Flutter 框架版本与 Flutter 应用编译时使用的版本一致

### 2. 插件注册失败

**问题**：Flutter 插件无法正常工作

**解决方案**：检查 `FlutterPluginRegistrant` 目录中的注册代码，确保所有插件都已正确注册

### 3. 内存使用过高

**问题**：应用内存使用过高

**解决方案**：合理管理 Flutter 引擎的生命周期，避免创建过多的 Flutter 引擎实例

## 许可证

FlutterTestHybrid 使用 MIT 许可证，详情请查看 [LICENSE](file:///workspace/LICENSE) 文件。

## 贡献

欢迎提交 Issue 和 Pull Request 来改进这个项目。

## 联系方式

- **作者**：zhangxiao
- **邮箱**：zhangxiao@xiaozhu.com
- **GitHub**：https://github.com/zhangxiao/FlutterTestHybrid
