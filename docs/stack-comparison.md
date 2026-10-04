# Compose 与 Avalonia 技术选型讨论

研究日期：2026-10-04。状态：选型已确定，保留候选对照与事实依据。

## 已确定的选型

用户选择 Avalonia 客户端与可复用的标准 M3 控件库共同交付，视觉基线采用 Material 3 Expressive。决策见 `docs/adr/0001-avalonia-material3-expressive.md`。

## 用户要求

当前主要比较 Android 原生 Compose 和 Avalonia。采用 Avalonia 时，完整标准的 Material 3 / Material You 主题库属于明确的条件需求，实现遵循现代 Avalonia 机制。Native AOT 与 GC 方案作为交付方向研究；“st什么 GC”按 Satori GC 线索核对。

## 初步建议

以 Android Pixiv 客户端为主要交付物时，优先 Kotlin + Jetpack Compose + Material 3。以通用 Avalonia M3 组件库与跨平台客户端共同交付为目标时，Avalonia 方案具有直接价值，并承担控件规范实现、移动平台适配、运行时交付三类工作。

这项建议基于当前目标和实施范围，是工程判断。

## 事实对照

| 维度 | Compose | Avalonia |
| --- | --- | --- |
| Material 3 | 使用 Android 官方组件、颜色、字体和形状体系 | 依照规范建立自己的设计令牌、控件模板和交互实现 |
| Material You 动态配色 | Android 12+ 提供 dynamicLightColorScheme / dynamicDarkColorScheme | 通过 Android 平台适配取得系统调色板，自定义种子配色依照官方算法实现 |
| 系统集成 | 使用 Android 平台 API 与 Jetpack 组件 | 使用 Android 项目适配平台服务、生命周期、Insets 和返回导航 |
| 共享 UI | Android 项目可在未来讨论 Compose Multiplatform 扩展 | 主题与控件面向 Avalonia 多平台复用 |
| 编译与运行时 | Kotlin/Android ART 交付链 | .NET Android 的 Mono、CoreCLR 和 Native AOT 路径分开验证 |

Compose 官方文档明确提供 Material You 与 Material 3 Expressive，实现动态配色、标准组件和无障碍基础：[Material Design 3 in Compose](https://developer.android.com/develop/ui/compose/designsystems/material3)。

Avalonia 的移动项目通过平台专用目标框架和项目交付 APK / AAB，平台接入通过原生互操作处理：[Android deployment](https://docs.avaloniaui.net/docs/deployment/android)、[Native interop](https://docs.avaloniaui.net/docs/app-development/native-interop)。

## 现代 Avalonia M3 实现建议

- 规范基线：固定 Material 3 的规范日期与组件清单，明确经典 M3 与 Expressive 的范围。
- 设计令牌：覆盖语义颜色、字体、形状、状态层、海拔和动效；以主题资源统一表达。
- 控件实现：ControlTheme 与 ControlTemplate 描述外观，标准控件和 TemplatedControl 承担交互，StyledProperty 表达可配置参数，伪类表达交互状态。
- 动态主题：ThemeDictionaries、ThemeVariant 和 DynamicResource 管理主题变化；Android 平台适配取得系统配色和主题变化事件。
- 数据绑定：采用编译绑定和明确的 x:DataType。当前 Avalonia 12 文档将编译绑定设为默认。
- AOT 兼容：数据序列化、视图和服务创建使用可静态分析的路径；为依赖和控件库提供发布验证。
- 标准验收：建立控件展厅，覆盖触摸、鼠标、键盘、字体放大、读屏、状态、主题和截图对照；完整规范覆盖作为主题库交付标准。

依据：[Control themes](https://docs.avaloniaui.net/docs/styling/control-themes)、[Compiled bindings](https://docs.avaloniaui.net/docs/data-binding/compiled-bindings)、[Theme variants](https://docs.avaloniaui.net/docs/styling/theme-variants)、[Material foundations](https://m3.material.io/foundations/)。

动态颜色的数学实现参考 [Material Color Utilities](https://github.com/material-foundation/material-color-utilities) 的 HCT、调色板和语义角色算法。Android 系统调色板与应用自定义种子色分别建立明确的数据来源。

## Native AOT 与 GC

Microsoft 的 [XA1040 文档](https://learn.microsoft.com/en-us/dotnet/android/messages/xa1040)于 2026-09-24 更新，仍把 Android Native AOT 标记为 experimental。[运行时与编译说明](https://learn.microsoft.com/en-us/dotnet/maui/deployment/runtimes-compilation?view=net-maui-10.0)分别解释 Mono AOT、CoreCLR 和 Native AOT；Native AOT 产物包含精简运行时与 GC。

[Satori 作者关于接入的讨论](https://github.com/dotnet/runtime/discussions/115627)记录了使用自构建 runtime / SDK 包接入 JIT 与 Native AOT 的方式。[Satori 编译产物](https://github.com/hez2010/Satori/releases)包含 Native AOT 支持。Android 的 Bionic ABI、.NET Android workload 与 Java 互操作需要逐项对应到真实产物。

当前 Satori 源码已包含 Android GC bridge 相关接入：`SatoriRecycler.cpp` 在 `FEATURE_JAVAMARSHAL` 条件下实现 `MarkBridgeObjects()` 并调用 `GCScan::GcProcessBridgeObjects`；`SatoriGC.cpp` 的 `NullBridgeObjectsWeakRefs()` 调用 `Ref_NullBridgeObjectsWeakRefs`。证据：[SatoriRecycler.cpp](https://github.com/hez2010/Satori/blob/main/src/coreclr/gc/satori/SatoriRecycler.cpp)、[SatoriGC.cpp](https://github.com/hez2010/Satori/blob/main/src/coreclr/gc/satori/SatoriGC.cpp)。这提供了运行时接入的正向源码证据，Bionic 编译产物与完整 Android 发布链仍通过实际构建和真机验证确定。

交付建议：官方运行时建立性能对照，自定义 Satori 产物建立可重复构建和真机比较；最终发布配置由帧时间、内存、启动和稳定性数据决定。

图片性能重点：按显示尺寸解码、限制缓存、控制预取、列表虚拟化和及时释放原生位图。4000×4000 的 RGBA 原始位图约 61 MiB，资源占用需要同时观察托管堆、原生位图和 GPU 缓存。

## Android GPU 加速补充

用户追问 Avalonia 在 Android 上的 GPU 加速能力。调查到的最新稳定版为 12.1.3，发布日期为 2026-09-22。该稳定版本 `AndroidPlatform.cs` 默认渲染优先级为 EGL、Software；`UseAndroid()` 使用 Skia，并提供可选择的 Vulkan 路径，同时接入 ChoreographerTimer 与 Compositor。

证据：[稳定版 AndroidPlatform.cs](https://github.com/AvaloniaUI/Avalonia/blob/12.1.3/src/Android/Avalonia.Android/AndroidPlatform.cs)、[AndroidPlatformOptions 文档](https://docs.avaloniaui.net/api/avalonia/androidplatformoptions)、[渲染模式 API](https://docs.avaloniaui.net/api/avalonia/androidrenderingmode)。

工程判断：现有 GPU 绘制与合成能力适合本项目的图片、缩放、裁剪与 M3 动效；实际流畅度同时取决于图片解码、布局、绑定、纹理上传、缓存预算和目标硬件。

[官方性能指南](https://docs.avaloniaui.net/docs/app-development/performance)说明默认 Skia GPU 资源缓存约 28 MB；图像资源超出预算时会增加纹理重复上传，移动设备需根据实际占用设定预算。图片按显示尺寸解码、相邻图片预取、缓存回收和列表虚拟化共同构成性能方案。

Native AOT 与 Satori 的验证聚焦 C# 执行和托管内存成本，GPU 缓存及原生图片资源分别纳入测量。Impeller 在官方资料中属于下一代渲染器合作方向，当前稳定默认实现采用 Skia。

首轮性能样机建议覆盖：连续滚动图片列表、切换相邻作品、大图缩放、常驻抽屉拉动、收藏处理中动画，以及应用切换前后台后的画面恢复。目标机按实际刷新率测量帧时间：60 Hz 为约 16.7 ms，120 Hz 为约 8.3 ms；同时记录掉帧、托管堆、原生图片与 GPU 资源占用。

## 已完成的决策

1. 主要交付目标：Avalonia 客户端与可复用 M3 控件库共同交付。
2. Material 规范基线：Material 3 Expressive。

后续讨论围绕运行时交付、平台服务和功能细节展开。
