<!-- Copyright 2019 The FlutterCandies author. All rights reserved.
Use of this source code is governed by an Apache license
that can be found in the LICENSE file. -->

# Flutter WeChat Camera Picker

[![pub package](https://img.shields.io/pub/v/wechat_camera_picker?logo=dart&label=%E7%A8%B3%E5%AE%9A%E7%89%88&style=flat-square)](https://pub.flutter-io.cn/packages/wechat_camera_picker)
[![pub package](https://img.shields.io/pub/v/wechat_camera_picker?color=42a012&include_prereleases&label=%E5%BC%80%E5%8F%91%E7%89%88&logo=dart&style=flat-square)](https://pub.flutter-io.cn/packages/wechat_camera_picker)
[![GitHub stars](https://img.shields.io/github/stars/fluttercandies/flutter_wechat_camera_picker?logo=github&style=flat-square)](https://github.com/fluttercandies/flutter_wechat_camera_picker/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/fluttercandies/flutter_wechat_camera_picker?logo=github&style=flat-square)](https://github.com/fluttercandies/flutter_wechat_camera_picker/network)
[![Build status](https://img.shields.io/github/actions/workflow/status/fluttercandies/flutter_wechat_camera_picker/runnable.yml?branch=main&label=CI&logo=github&style=flat-square)](https://github.com/fluttercandies/flutter_wechat_camera_picker/actions/workflows/runnable.yml)
[![CodeFactor](https://img.shields.io/codefactor/grade/github/fluttercandies/flutter_wechat_camera_picker?logo=codefactor&label=%E4%BB%A3%E7%A0%81%E8%B4%A8%E9%87%8F&logoColor=%23ffffff&style=flat-square)](https://www.codefactor.io/repository/github/fluttercandies/flutter_wechat_camera_picker)
[![GitHub license](https://img.shields.io/github/license/fluttercandies/flutter_wechat_camera_picker?style=flat-square&label=%E5%8D%8F%E8%AE%AE)](https://github.com/fluttercandies/flutter_wechat_camera_picker/blob/master/LICENSE)
<a target="_blank" href="https://jq.qq.com/?_wv=1027&k=5bcc0gy"><img border="0" src="https://pub.idqqimg.com/wpa/images/group.png" alt="FlutterCandies" title="FlutterCandies"></a>

Language: [English](README.md) | 中文简体

基于微信界面的相机选择器，可单独运行，是
[**仿微信资源选择器**](https://pub.flutter-io.cn/packages/wechat_assets_picker) 的扩展。
选择器基于 `camera` 实现相机相关功能，`photo_manager` 实现资源相关内容。

当前的界面设计基于的微信版本：**8.3.x**
界面更新将在微信版本更新后随时进行跟进。

查看 [迁移指南][] 了解如何从破坏性改动中迁移为可用代码。

<details>
  <summary>Table of content</summary>

<!-- TOC -->
* [Flutter WeChat Camera Picker](#flutter-wechat-camera-picker)
  * [特性 ✨](#特性-)
  * [截图 📸](#截图-)
  * [开始前的注意事项 ‼️](#开始前的注意事项-)
  * [准备工作 🍭](#准备工作-)
    * [版本兼容](#版本兼容)
    * [配置](#配置)
      * [Android 13 (API 33) 权限配置](#android-13-api-33-权限配置)
  * [使用方法 📖](#使用方法-)
    * [国际化](#国际化)
    * [简单的使用方法](#简单的使用方法)
    * [使用配置](#使用配置)
    * [简单的使用方法](#简单的使用方法-1)
    * [使用自定义的 `State`](#使用自定义的-state)
  * [常见问题 💭](#常见问题-)
    * [iOS 上的预览在旋转时行为诡异](#ios-上的预览在旋转时行为诡异)
<!-- TOC -->
</details>

## 特性 ✨

- ♿ 完整的无障碍支持，包括 **TalkBack** 和 **VoiceOver**
- ♻️ 支持基于 `State` 重载的全量自定义
- 🎏 完全可自定义的基于 `ThemeData` 的主题
- 💚 复刻微信风格（甚至优化了更多的细节）
- ⚡️ 根据配置调节的性能优化
- 📷 支持拍照
- 🎥 支持录像
  - ⏱ 支持限制录像时间
  - 🔍 支持录像时缩放
- ☀️ 支持设置曝光参数
- 🔍️ 支持捏合缩放
- 💱 国际化支持
  - ⏪ RTL 语言支持
- 🖾 支持自定义前景 widget 构建
- 🕹️ 保存时拦截自定义操作

## 截图 📸

| ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggtt6yrdqej30u01t017w.jpg) | ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggtt6yh3x4j30u01t0wuo.jpg) |
|-------------------------------------------------------------------------|-------------------------------------------------------------------------|
| ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggtt6z1h7xj30u01t01kx.jpg) | ![](https://tva1.sinaimg.cn/large/007S8ZIlgy1ggtt6zarvhj30u01t0x5f.jpg) |

## 开始前的注意事项 ‼️

在开始一切之前，请明确以下两点：
- 由于理解差异和篇幅限制，并不是所有的内容都会明确地在文档中指出。
  当你遇到没有找到需求和无法理解的概念时，请先运行项目的示例 example，
  它可以解决 90% 的常见需求。
- 该库与 [photo_manager][photo_manager pub] 有强关联性，
  大部分方法的行为是由 photo_manager 进行控制的，
  所以请尽可能地确保你了解以下两个类的概念：
  - 资源（图片/视频/音频） [`AssetEntity`](https://pub.flutter-io.cn/documentation/photo_manager/latest/photo_manager/AssetEntity-class.html)
  - 资源合集（相册或集合概念） [`AssetPathEntity`](https://pub.flutter-io.cn/documentation/photo_manager/latest/photo_manager/AssetPathEntity-class.html)

当你有与相关的 API 和行为的疑问时，你可以查看
[photo_manager API 文档][] 了解更多细节。

众多使用场景都已包含在示例中。
在你提出任何问题之前，请仔细并完整地查看和使用示例。

## 准备工作 🍭

### 版本兼容

该插件仅保证能与 **stable 渠道的 Flutter SDK** 配合使用。
我们不会为其他渠道的 Flutter SDK 做实时支持。

|        | 2.8.0 | 3.3.0 |
|--------|:-----:|:-----:|
| 4.0.0+ |   ❌   |   ✅   |
| 3.0.0+ |   ✅   |   ❌   |

如果在 `flutter pub get` 时遇到了 `resolve conflict` 失败问题，
请使用 `dependency_overrides` 解决。

### 配置

执行 `flutter pub add wechat_camera_picker`，
或者将 `wechat_camera_picker` 手动添加至 `pubspec.yaml` 引用。

```yaml
dependencies:
  wechat_camera_picker: ^latest_version
```

最新的 **稳定** 版本是:
[![pub package](https://img.shields.io/pub/v/wechat_camera_picker?logo=dart&label=stable&style=flat-square)](https://pub.flutter-io.cn/packages/wechat_camera_picker)

最新的 **开发** 版本是:
[![pub package](https://img.shields.io/pub/v/wechat_camera_picker?color=9d00ff&include_prereleases&label=dev&logo=dart&style=flat-square)](https://pub.flutter-io.cn/packages/wechat_camera_picker)

在你的代码中导入：

```dart
import 'package:wechat_camera_picker/wechat_camera_picker.dart';
```

更多配置步骤：
- [wechat_assets_picker#准备工作](https://github.com/fluttercandies/flutter_wechat_assets_picker/blob/master/README-ZH.md#preparing-for-use-)
- [camera#installation](https://pub.flutter-io.cn/packages/camera#installation)

#### Android 13 (API 33) 权限配置

在使用这个 package 时，请确保
`compileSdkVersion` 和 `targetSdkVersion` 升级到 `33`。
否则，在 Android 13 设备上将有可能无法加载任何资源。

如果你不需要拍照或录像，你可以考虑将对应权限移除：

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- 如果需要拍照，添加该权限 -->
    <uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />
    <!-- 如果需要录像，添加该权限 -->
    <uses-permission android:name="android.permission.READ_MEDIA_VIDEO" />
</manifest>
```

## 使用方法 📖

### 国际化

当你在选择资源的时候，package 会通过你的 `BuildContext`
读取 `Locale?`，返回对应语言的文字代理实现。
请确保你可以通过 `BuildContext` 获取到 `Locale`，否则将会 **默认展示中文文字**。

内置的语言文字实现有：
* 简体中文 (默认)
* English
* Tiếng Việt

如果你想使用自定义或固定的文字实现，请通过
`CameraPickerConfig.textDelegate` 传递调用。

### 简单的使用方法

```dart
final AssetEntity? entity = await CameraPicker.pickFromCamera(context);
```

### 使用配置

你可以使用 `CameraPickerConfig` 来调整选择时的行为。

```dart
final AssetEntity? entity = await CameraPicker.pickFromCamera(
  context,
  pickerConfig: const CameraPickerConfig(),
);
```

`CameraPickerConfig` 的成员说明：

### 简单的使用方法

```dart
final AssetEntity? entity = await CameraPicker.pickFromCamera(context);
```

你可以使用 `CameraPickerConfig` 来调整选择时的行为。

```dart
final AssetEntity? entity = await CameraPicker.pickFromCamera(
  context,
  pickerConfig: const CameraPickerConfig(),
);
```

`CameraPickerConfig` 的成员说明：

| 参数名                           | 类型                          | 描述                                                 | 默认值                                        |
|-------------------------------|-----------------------------|----------------------------------------------------|--------------------------------------------|
| enableRecording               | `bool`                      | 选择器是否可以录像                                          | `false`                                    |
| onlyEnableRecording           | `bool`                      | 选择器是否仅可以录像。只在 `enableRecording` 为 `true` 时有效。      | `false`                                    |
| enableTapRecording            | `bool`                      | 选择器是否可以单击录像。只在 `onlyEnableRecording` 为 `true` 时生效。 | `false`                                    |
| enableAudio                   | `bool`                      | 选择器是否需要录制音频。只在 `enableRecording` 为 `true` 时有效。     | `true`                                     |
| enableSetExposure             | `bool`                      | 用户是否可以在界面上通过点击设定曝光点                                | `true`                                     |
| enableExposureControlOnPoint  | `bool`                      | 用户是否可以根据已经设置的曝光点调节曝光度                              | `true`                                     |
| enablePinchToZoom             | `bool`                      | 用户是否可以在界面上双指缩放相机对焦                                 | `true`                                     |
| enablePullToZoomInRecord      | `bool`                      | 用户是否可以在录制视频时上拉缩放                                   | `true`                                     |
| shouldDeletePreviewFile       | `bool`                      | 返回页面时是否删除预览文件                                      | `false`                                    |
| shouldAutoPreviewVideo        | `bool`                      | 在预览时是否直接播放视频                                       | `false`                                    |
| maximumRecordingDuration      | `Duration?`                 | 录制视频最长时长                                           | `const Duration(seconds: 15)`              |
| minimumRecordingDuration      | `Duration`                  | 录制视频最短时长                                           | `const Duration(seconds: 1)`               |
| theme                         | `ThemeData?`                | 选择器的主题                                             | `CameraPicker.themeData(wechatThemeColor)` |
| textDelegate                  | `CameraPickerTextDelegate?` | 控制部件中的文字实现                                         | `CameraPickerTextDelegate`                 |
| resolutionPreset              | `ResolutionPreset`          | 相机的分辨率预设                                           | `ResolutionPreset.max`                     |
| cameraQuarterTurns            | `int`                       | 摄像机视图顺时针旋转次数，每次 90 度                               | `0`                                        |
| imageFormatGroup              | `ImageFormatGroup`          | 输出图像的格式描述                                          | `ImageFormatGroup.unknown`                 |
| preferredLensDirection        | `CameraLensDirection`       | 首次使用相机时首选的镜头方向                                     | `CameraLensDirection.back`                 |
| lockCaptureOrientation        | `DeviceOrientation?`        | 摄像机在拍摄时锁定的旋转角度                                     | null                                       |
| foregroundBuilder             | `ForegroundBuilder?`        | 覆盖在相机预览上方的前景构建                                     | null                                       |
| previewTransformBuilder       | `PreviewTransformBuilder?`  | 对相机预览做变换的构建                                        | null                                       |
| onEntitySaving                | `EntitySaveCallback?`       | 在查看器中保存图片时的回调                                      | null                                       |
| onError                       | `CameraErrorHandler?`       | 拍摄照片过程中的自定义错误处理                                    | null                                       |
| onXFileCaptured               | `XFileCapturedCallback?`    | 拍摄文件生成后的回调                                         | null                                       |
| onMinimumRecordDurationNotMet | `VoidCallback?`             | 录制时长未达到最小时长时的回调方法                                  | null                                       |

### 使用自定义的 `State`

所有的用户界面都可以通过自定义 `State` 实现，包括：
- `CameraPickerState`
- `CameraPickerViewerState`

在完成 `State` 的重载后，可以在调用时进行构建，具体来说：
- `CameraPicker.pickFromCamera(createPickerState: () => CustomCameraPickerState());`
- `CameraPickerViewer.pushToViewer(..., createViewerState: () => CustomCameraPickerViewerState());`

## 常见问题 💭

### iOS 上的预览在旋转时行为诡异

目前，iOS 上的预览画面在旋转时并未正确地同步，
你可以在这个 issue 里了解更多相关的信息：
https://github.com/flutter/flutter/issues/89216 。
除此之外的问题，你可以提交 issue 进行提问。

[photo_manager pub]: https://pub.flutter-io.cn/packages/photo_manager
[迁移指南]: https://github.com/fluttercandies/flutter_wechat_camera_picker/blob/main/guides/migration_guide.md
