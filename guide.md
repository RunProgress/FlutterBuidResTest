# FlutterTestHybrid 仓库指南

## 仓库概览

FlutterTestHybrid 是一个混合 Flutter 和原生 iOS 代码的库，旨在提供一种在 iOS 应用中集成 Flutter 功能的解决方案。

- **混合开发**：结合 Flutter 的跨平台能力和 iOS 原生开发的性能优势
- **模块化设计**：通过 CocoaPods 管理，易于集成到现有 iOS 项目中
- **完整框架**：包含 Flutter 框架和必要的原生代码

## 目录结构

```
├── Example/              # 示例项目
│   ├── FlutterTestHybrid.xcodeproj/  # Xcode 项目文件
│   ├── FlutterTestHybrid.xcworkspace/ # Xcode 工作空间
│   ├── Pods/              # CocoaPods 依赖
│   ├── Tests/             # 测试文件
│   ├── Podfile            # Podfile 配置
│   └── Podfile.lock       # Podfile 锁定文件
├── FlutterTestHybrid/     # 主要库代码
│   ├── Assets/            # 资源文件
│   ├── Classes/           # 原生 iOS 代码
│   │   └── FlutterPluginRegistrant/  # Flutter 插件注册
│   └── Framework/         # Flutter 框架
│       ├── App.framework/  # 应用框架
│       └── Flutter.framework/ # Flutter 核心框架
├── .gitignore             # Git 忽略文件
├── .travis.yml            # Travis CI 配置
├── FlutterTestHybrid.podspec # CocoaPods 规格文件
├── LICENSE                # 许可证文件
├── README.md              # 项目说明
└── guide.md               # 仓库指南（本文档）
```

## 核心功能

### Flutter 集成

FlutterTestHybrid 提供了完整的 Flutter 框架集成，包括：

- **Flutter.framework**：Flutter 核心框架，提供跨平台 UI 渲染能力
- **App.framework**：包含 Flutter 应用代码和资源
- **FlutterPluginRegistrant**：负责注册 Flutter 插件

### 原生 iOS 集成

- 通过 CocoaPods 管理依赖，易于集成到现有 iOS 项目
- 支持 iOS 8.0 及以上版本
- 提供模块化的代码结构，便于维护和扩展

## 安装与使用

### 安装方法

1. 在项目的 Podfile 中添加以下行：

```ruby
pod 'FlutterTestHybrid'
```

2. 运行以下命令安装依赖：

```bash
pod install
```

### 运行示例项目

1. 克隆仓库：

```bash
git clone https://github.com/zhangxiao/FlutterTestHybrid.git
```

2. 进入 Example 目录并安装依赖：

```bash
cd FlutterTestHybrid/Example
pod install
```

3. 打开 `FlutterTestHybrid.xcworkspace` 并运行示例项目

## 技术栈

- **开发语言**：Objective-C、Dart
- **构建工具**：CocoaPods
- **测试框架**：XCTest
- **持续集成**：Travis CI

## 开发流程

1. **修改 Flutter 代码**：在 Flutter 项目中进行开发
2. **构建 Flutter 框架**：将 Flutter 代码构建为 App.framework
3. **更新原生代码**：在 Classes 目录中修改原生代码
4. **测试**：运行 Tests 目录中的测试
5. **发布**：更新版本号并发布到 CocoaPods

## 许可证

FlutterTestHybrid 使用 MIT 许可证，详见 [LICENSE](file:///workspace/LICENSE) 文件。

## 作者

- **zhangxiao** - [zhangxiao@xiaozhu.com](mailto:zhangxiao@xiaozhu.com)

## 贡献

欢迎提交 Issue 和 Pull Request 来改进这个项目。

## 联系方式

- GitHub 仓库：[https://github.com/zhangxiao/FlutterTestHybrid](https://github.com/zhangxiao/FlutterTestHybrid)
- CocoaPods 页面：[https://cocoapods.org/pods/FlutterTestHybrid](https://cocoapods.org/pods/FlutterTestHybrid)