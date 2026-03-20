# Mate Engine - 项目全景文档

## 项目定位

**Mate Engine** 是一款免费、轻量级的桌面萌宠应用，作为商业软件 **Desktop Mate** 的开源替代品。项目旨在提供：
- 完全免费的桌面萌宠体验
- 自定义 VRM 角色支持
- 开放的模组开发能力
- 更少限制，更多自由度

项目特点：对标的是付费的 Desktop Mate，解决了后者收费高昂且禁用模组的问题。

---

## 技术栈

### 核心引擎
- **Unity 版本**: 6000.2.6f2 (Unity 6)
- **开发语言**: C# / ShaderLab / HLSL

### 核心包依赖 (manifest.json)
| 包名 | 版本 | 用途 |
|------|------|------|
| com.unity.2d.sprite | 1.0.0 | 2D 精灵处理 |
| com.unity.collab-proxy | 2.9.3 | 协作版本控制 |
| com.unity.feature.development | 1.0.2 | 开发工具特性 |
| com.unity.localization | 1.5.8 | 多语言本地化 |
| com.unity.memoryprofiler | 1.1.9 | 内存分析工具 |
| com.unity.multiplayer.center | 1.0.0 | 多人游戏中心 |
| com.unity.postprocessing | 3.5.1 | 后处理效果 |
| com.unity.timeline | 1.8.9 | 时间线动画 |
| com.unity.toolchain.win-x86_64-linux-x86_64 | 2.0.10 | Linux 交叉编译工具链 |
| com.unity.ugui | 2.0.0 | UI 系统 |
| com.unity.visualscripting | 1.9.7 | 可视化编程 |

### 内置着色器
- **lilToon**: jp.lilxyzw.liltoon-1.8.5
- **Poiyomi Toon**: com.poiyomi.toon-9.2.79

### 第三方集成
- VRM 格式支持（自定义角色加载）
- 内置 LLM 集成（QWEN 2.5 1.5b），Apache 2.0 许可证
- Steam 创意工坊支持（Steam 版本）
- Discord Rich Presence 集成

---

## 核心模块架构

```
Assets/
├── MATE ENGINE - Animations/          # 动画资源（待机动画、拖拽动画等）
├── MATE ENGINE - Avatar/              # 默认角色资源
├── MATE ENGINE - Custom Dance Player/ # 自定义舞蹈播放器模块
├── MATE ENGINE - DLCs/                # DLC 内容管理
├── MATE ENGINE - Fonts/               # 字体资源
├── MATE ENGINE - Icons/               # 图标资源
├── MATE ENGINE - Mod SDK/             # 模组开发 SDK
├── MATE ENGINE - Packages/            # 包管理
├── MATE ENGINE - Props/               # 道具资源
├── MATE ENGINE - Rewrites/            # 重写模块
├── MATE ENGINE - Scenes/              # 场景文件
│   └── Mate Engine Main               # 主入口场景
├── MATE ENGINE - Scripts/             # C# 脚本 (核心代码)
│   ├── APIs/                          # 外部 API 接口
│   ├── AvatarHandlers/                # 角色处理器
│   ├── BlendshapeManager/             # 形变管理
│   ├── Game APIs/                     # 游戏 API 集成
│   ├── Lang/                          # 多语言文件
│   ├── Settings/                      # 设置系统
│   ├── Tasty Pie Menu/                # 菜单系统
│   ├── ThemeManager/                  # 主题管理
│   ├── Tools/                         # 工具类
│   └── VRMLoader/                     # VRM 加载模块
├── MATE ENGINE - Shaders/             # 着色器
├── MATE ENGINE - Sounds/              # 音效资源
├── MATE ENGINE - System Tray/         # 系统托盘功能 (Windows)
├── MATE ENGINE - Tools/               # 编辑器工具
└── MATE ENGINE - VOICE PACKS/         # 语音包
```

### 代码统计
- **C# 代码文件数量**: 1457 个

---

## 核心功能

| 功能 | 状态 | 说明 |
|------|------|------|
| 自定义 VRM 角色 | ✅ | 支持加载任意 VRM 格式模型 |
| 窗口坐立 | ✅ | 可以让角色坐在窗口边缘 |
| 任务栏坐立 | ✅ | 可以让角色坐在任务栏上 |
| 待机动画 | ✅ | 循环待机动画 |
| 拖拽动画 | ✅ | 拖拽时平滑漂浮动画 |
| 音乐舞蹈 | ✅ | 随音乐跳舞（实验性） |
| 头部追踪 | ✅ | 头部跟随追踪 |
| 脊柱追踪 | ✅ | 脊柱骨骼追踪 |
| 眼部追踪 | ✅ | 眼球运动追踪 |
| 手部动作 | ✅ | 动态手部动作 |
| 闹钟/计时器 | ✅ | 定时提醒功能 |
| 屏幕保护 | ✅ | 屏保模式 |
| 触摸响应区域 | ✅ | 支持点击不同区域产生不同反应 |
| 角色音效 | ✅ | 触发音效效果 |
| 粒子效果 | ✅ | 支持粒子特效 |
| FPS 控制 | ✅ | 可配置帧率限制 |
| 始终置顶切换 | ✅ | 窗口置顶控制 |
| Chibi 迷你模式 | ✅ | 缩小角色比例 |
| 后处理 Bloom | ✅ |  bloom 光效 |
| 后处理 AO | ✅ | 环境光遮蔽 |
| MSAA x8 | ✅ | 8 倍多重采样抗锯齿 |
| 大屏幕模式 | ✅ | 大屏显示模式 |
| 系统托盘图标 | ✅ | Windows 系统托盘支持 |
| 平滑动画过渡 | ✅ | 平滑动画切换 |
| Steam 创意工坊 | ✅ | Steam 版本模组支持 |
| 内置 Mod SDK | ✅ | 支持开发者创建模组 |
| AI 聊天 | ✅ | 集成 Qwen LLM |
| 多语言支持 | ✅ | 中英日多语言 |
| 动画模组 | ✅ | 自定义动画模组 |
| 随系统启动 | ✅ | 开机自启 |
| 形变编辑 | ✅ | 运行时编辑 blendshape |
| 装扮系统 | ✅ | 饰品装扮 |
| MMD 动画播放器 | ✅ | 支持 MMD 音乐动画 |
| 动作表情联动 | ✅ | 表情根据动作变化 |
| 逆运动学 IK | ✅ | 支持逆运动学 |
| 菜单自定义 | ✅ | 可定制菜单 |
| 调试菜单 | ✅ | 开发者调试功能 |
| 多角色 | ✅ | 最多同时 9 个角色 |
| 舞蹈同步 | ✅ | 多角色舞蹈同步 |
| Minecraft 集成 | ✅ | Minecraft 相关集成 |
| 食物系统 | ✅ | 喂食互动系统 |

---

## 依赖版本

- Unity Editor: **6000.2.6f2**
- .NET: 随 Unity 6 版本
- 构建目标:
  - Windows: x86_64
  - Linux: x86_64 (通过交叉编译工具链支持)

---

## 构建流程

### 开发环境搭建
1. 克隆仓库到本地
2. 使用 Unity Hub 打开项目
3. 确保 Unity 版本为 **6000.2.6f2**
4. 打开主场景: `Assets/MATE ENGINE - Scenes/Mate Engine Main`
5. 进入 Play 模式运行

### 构建设置
- **主场景**: `Mate Engine Main`
- **渲染管线**: 内置渲染管线
- **目标架构**: x86_64
- **脚本后端**: IL2CPP

### 输出
- Windows: `MateEngineX.exe`
- Linux: 可执行文件（通过 Unity 交叉编译工具链构建）

---

## 部署方式

### 公开版本
- GitHub Releases 发布 ZIP 压缩包（免费）
- Steam 商店发布（付费 $3.99，GitHub 保持免费）

### 安装
用户只需：
1. 下载 ZIP
2. 解压
3. 运行 `MateEngineX.exe`

### 模组部署
- Steam 版本: Steam 创意工坊直接订阅
- GitHub 版本: 手动放入模组文件夹，或通过 .ME 格式安装

---

## 当前版本状态

- **当前版本**: X3.4 (开发中)
- **最新公开发布**: X3.3.0 Hotfix 1
- **分支**: `feat-dev_talk` (当前开发分支)
- **代码行数**: ~1457 个 C# 文件
- **许可证**: 混合许可证
  - 主程序: MateProv2 许可证 (基于 AGPL 的修改版) + GNU AGPL v3
  - 默认角色: 版权所有 (Yorshka Shop)，禁止重新分发
  - QWEN 2.5 LLM: Apache License 2.0
- **Steam 发布状态**: 已发布 (https://store.steampowered.com/app/3625270/MateEngine/)
- **目标发布日期（Steam）**: 2025年3月26日（已达成）

---

## 性能指标

- **CPU 使用率**: 非常好（轻量化设计）
- **GPU 使用率**: 良好
- **RAM 使用率**: 良好
  - 高质量模型示例: ~200MB (Alice 模型)
  - 轻量模型: 更低

---

## 支持平台

- Windows 10/11 (主要支持)
- Linux (社区移植支持)
- 未来可能支持 macOS

---

## 链接

- 原始仓库: https://github.com/Marksonthegamer/Mate-Engine-Linux-Port
- Steam 商店: https://store.steampowered.com/app/3625270/MateEngine/
- 社区自定义舞蹈播放器: https://github.com/maoxig/MateEngine-CustomDancePlayer
