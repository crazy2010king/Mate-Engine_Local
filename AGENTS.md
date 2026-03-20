# AGENTS - Mate Engine 项目 AI 代理持久化指令

本文档对所有 AI 代理会话生效，定义了在 Mate Engine 项目上工作的编码规范、架构约束和禁止操作范围。

---

## 1. 项目基本认知

**Mate Engine** 是 Unity 6 开发的开源免费桌面萌宠应用，是 Desktop Mate 的开源替代品。

- 项目类型: Unity 桌面应用 (Windows/Linux)
- Unity 版本: **6000.2.6f2** (必须严格匹配)
- 主语言: C#
- 项目地址: https://github.com/crazy2010king/Mate-Engine_Local (当前仓库)
- 原始项目: https://github.com/Marksonthegamer/Mate-Engine-Linux-Port

---

## 2. 编码规范

### 命名约定
- **类名**: PascalCase (`class AvatarLoader`)
- **方法名**: PascalCase (`public void LoadAvatar()`)
- **私有字段**: camelCase 前缀下划线 `_avatarData`
- **公共变量/属性**: PascalCase (`public float Scale { get; set; }`)
- **局部变量/参数**: camelCase (`avatarPath`)
- **常量**: ALL_CAPS (`const int MAX_AVATARS = 9`)

### 文件组织
- 新代码必须放到对应模块目录:
  - 核心逻辑 → `Assets/MATE ENGINE - Scripts/`
  - 动画资源 → `Assets/MATE ENGINE - Animations/`
  - 着色器 → `Assets/MATE ENGINE - Shaders/`
- 文件名必须和包含的主类名一致
- 保留 Unity 自动生成的 `.meta` 文件

### 代码风格
- 使用四个空格缩进，不使用 Tab
- 大括号换行风格（Allman 风格）
- 单行语句也必须使用大括号
- 公共 API 添加 XML 文档注释

示例:
```csharp
/// <summary>
/// Loads VRM avatar from file path.
/// </summary>
/// <param name="path">Path to .vrm file</param>
/// <returns>True if load succeeded</returns>
public bool Load(string path)
{
    if (string.IsNullOrEmpty(path))
    {
        return false;
    }
    
    _loadedPath = path;
    return ProcessLoad();
}
```

### 性能规范
- 缓存 `GetComponent` 结果，不要在 `Update` 中调用
- 避免在 `Update` / `LateUpdate` 产生 GC 分配
- 频繁创建销毁的对象使用对象池
- 订阅事件必须记得取消订阅防止内存泄漏

---

## 3. 架构约束

### 必须尊重现有架构
- VRM 加载: 使用内置加载模块 (`MATE ENGINE - Scripts/VRMLoader/`)，不要重构除非有非常充分的理由
- 菜单系统: 使用 Tasty Pie Menu，不要更换整体框架
- 多语言: 使用 Unity Localization 包 (`com.unity.localization`)，保持现有结构
- 后处理: 使用 Unity PostProcessing v3 (`com.unity.postprocessing@3.5.1`)

### 依赖约束
- 优先使用 Unity 内置包，不随意新增第三方依赖
- 新增第三方依赖必须满足:
  - 许可证兼容 (MIT/Apache 2.0/BSD 等宽松许可)
  - 不增加过多项目体积
  - 解决确实需要的问题
- 禁止引入闭源/商业授权的依赖

### 模块依赖方向
- SDK → 核心: 允许 (模组 SDK 依赖核心)
- 核心 → SDK: 不允许 (核心不能依赖 SDK 模块)
- UI → 业务逻辑: 允许
- 业务逻辑 → UI: 尽量避免，保持解耦

---

## 4. 禁止操作范围

### 绝对禁止
- ❌ **不得修改** 根目录 LICENSE.md / COPYRIGHT / 许可证信息
- ❌ **不得删除** 版权声明和作者署名
- ❌ **不得将** 默认版权角色 (Yorshka Shop) 重新分发
- ❌ **不得改变** 项目许可证条款
- ❌ **不得提交** 大文件 (>100MB) 到 Git 仓库
- ❌ **不得提交** Unity 生成的 Library/ Temp/ Obj/ Build 文件夹
- ❌ **不得修改** 禁止修改的核心模块（见 DECISIONS.md）而不经过讨论
- ❌ **不得引入** 商业闭源依赖
- ❌ **不得删除** 现有多语言文件，新增功能需要同时更新所有语言文件

### 谨慎操作
- ⚠️ 修改 VRM 加载代码前必须充分测试多种 VRM 模型兼容性
- ⚠️ 修改动画过渡系统前必须测试所有动画类型
- ⚠️ 修改性能敏感代码前后需要做性能对比

---

## 5. Git 规范

- 提交信息使用英文或中文，清晰描述修改内容
- 每个提交做一件事，不将多个无关修改混在一起
- 在功能分支开发，不要直接推送到 main
- 当前工作分支: `feat-dev_talk`

---

## 6. 测试要求

- 修改后必须确保可以在 Unity 中正常进入 Play 模式
- 修改核心功能后，要说明测试了哪些场景
- 修复 Bug 需要验证修复确实生效
- 新增功能需要有基本的错误处理（空检查、异常捕获）

---

## 7. 文档要求

- 新增功能需要更新相关文档
- 保持 PROJECT.md, DECISIONS.md 与实际项目一致
- 重大架构变更需要记录决策到 DECISIONS.md

---

## 8. 对 AI 代理的额外要求

1. **先了解再修改**: 在修改代码前，先读取现有代码理解结构和上下文
2. **保持兼容**: 尽量保持对现有模组和配置的向后兼容性
3. **最小改动**: 只修改需要修改的地方，不做大规模重构除非要求
4. **尊重现状**: 如果现有代码虽然不完美但可以工作，不要强行"美化"
5. **询问确认**: 对于涉及核心架构的修改，在实施前先询问用户确认

---

## 9. 快速参考

- **主场景**: `Assets/MATE ENGINE - Scenes/Mate Engine Main`
- **核心脚本目录**: `Assets/MATE ENGINE - Scripts/`
- **Unity 版本**: 6000.2.6f2
- **最大同时角色**: 9
- **许可证**: 混合 (MateProv2 + AGPLv3)，详见 LICENSE.md
