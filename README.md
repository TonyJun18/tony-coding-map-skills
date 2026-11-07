# xfg-coding-map-skills

代码地图（Code Map）生成技能：把一次开发迭代、一个需求设计或一个教学章节，生成为一张**自包含的可交互 HTML 全景图**。

## 它长什么样

三栏联动布局（参考 `case/xfg-2-1-code-map.html` 实例）：

- **左栏**：IDEA 风格工程树 —— 类/接口/方法图标、新增/调整/复用状态徽标、搜索过滤、折叠展开
- **中栏**：Mermaid 图（全景模块地图 / 运行时序 / 方法流程），五色变更标记（新增绿 / 复用灰虚线 / 外部蓝 / 兜底橙 / 错误红）
- **右栏**：变更说明卡（定位 → 关键设计 → 坑），按类型过滤
- **联动**：任意一栏点击，另外两栏定位高亮 + SVG 贝塞尔连线
- **主线导览**：顶部"跟着流程走"站点条 + 底部导览卡，沿开发叙事走完整个主题

完全离线可用（mermaid 本地 vendor），单文件交付，浏览器直接打开。

## 五种使用场景

| 场景 | 一句话 |
|---|---|
| S1 教学章节 | 课程每章一张串联图，8 站导览讲完一条链 |
| S2 迭代对比 | 两个版本之间改了什么、为什么改、影响面，评审动线走一遍 |
| S3 需求蓝图 | 开发前画出目标态，导览顺序即开发顺序——跟着流程走就能实现出来 |
| S4 PR 讲解 | 单 PR 变更子图 + 评审关注点，末站给评审结论 |
| S5 架构 Onboarding | 新人看懂项目：模块职责 + 一次请求的生命周期 |

## 目录结构

```
xfg-coding-map-skills/
├── SKILL.md                      # 技能入口：工作流（场景识别→素材→生成→校验→交付）
├── assets/
│   ├── code-map-template.html    # 渲染引擎 + 示例数据（MAP-DATA 区间整体替换）
│   └── vendor/mermaid.min.js     # 离线 mermaid
├── references/
│   ├── data-spec.md              # TREE/DOCS/TOUR/图源码 字段规范与 kw 联动规则
│   └── scenarios.md              # 五种场景的素材来源与场景化设计
├── scripts/
│   ├── extract-diff.sh           # 采集 git 基线变更（迭代/PR 场景素材）
│   └── validate-map.js           # 生成后一致性校验（kw 断链/doc 引用/TOUR 引用）
└── case/                         # 实例：xfg-2-1 教学章节图（deepseek-harness 项目）
```

## 快速体验

```bash
# 校验内置示例（应输出 0 错误）
node scripts/validate-map.js assets/code-map-template.html

# 打开实例
open case/xfg-2-1-code-map.html
```

## 安装为 WorkBuddy 技能

```bash
cp -r xfg-coding-map-skills ~/.workbuddy/skills/
```

之后在对话里说"帮我生成这次迭代的代码地图"或"给这个需求出一张开发蓝图导览"即可触发。
