---
name: ui-ux-pro
description: AI-powered UI/UX design intelligence for building professional interfaces across platforms and frameworks. Includes intelligent design system generator v2.0 for complete tailored design systems with colors, typography, and best practices
---

# UI UX Pro

UI UX Pro 是一个 AI 技能，为跨多个平台和框架构建专业 UI/UX 提供设计智能。

## v2.0 新特性：智能设计系统生成器

AI 驱动的推理引擎，分析你的项目需求并在几秒钟内生成完整、量身定制的设计系统。

### 设计系统输出包含

- **Pattern** - 落地页结构和布局模式
- **Style** - UI 样式关键词和最佳实践
- **Colors** - 主色、辅色、CTA、背景、文本色及调色板建议
- **Typography** - 字体组合和 Google Fonts 导入
- **Key Effects** - 阴影、过渡、悬停状态
- **Anti-patterns to Avoid** - 避免的设计反模式
- **Pre-delivery Checklist** - 可访问性、响应式、焦点状态等检查项

## 支持的技术栈

| 技术栈 | 说明 |
|---------|------|
| HTML + Tailwind | 默认 |
| React / Next.js / shadcn/ui | 支持 |
| Vue / Nuxt.js / Nuxt UI / Svelte | 支持 |
| SwiftUI / React Native / Flutter | 支持 |

只需在提示词中提及你偏好的技术栈，或让它默认为 HTML + Tailwind。

## 57 种 UI 样式

Glassmorphism、Claymorphism、Minimalism、Brutalism、Neumorphism、Bento Grid、Dark Mode、AI-Native UI 等

## 95 种调色板

适用于 SaaS、E-commerce、Healthcare、Fintech、Beauty 等的行业专用调色板。

## 56 种字体组合

精选的排版组合，包含 Google Fonts 导入。

## 100 行业专用推理规则

| 类别 | 示例 |
|------|------|
| Tech & SaaS | SaaS、Micro SaaS、B2B Enterprise、Developer Tools、AI/Chatbot Platform |
| Finance | Fintech、Banking、Crypto、Insurance、Trading Dashboard |
| Healthcare | Medical Clinic、Pharmacy、Dental、Veterinary、Mental Health |
| E-commerce | General、Luxury、Marketplace、Subscription Box |
| Services | Beauty/Spa、Restaurant、Hotel、Legal、Consulting |
| Creative | Portfolio、Agency、Photography、Gaming、Music Streaming |
| Emerging Tech | Web3/NFT、Spatial Computing、Quantum Computing、Autonomous Systems |

每条规则包括：
- 推荐模式 - 落地页结构
- 样式优先级 - 最佳匹配 UI 样式
- 色彩情绪 - 行业适当的调色板
- 排版情绪 - 字体个性匹配
- 关键效果 - 动画和交互
- 反模式 - 避免什么

## 使用方法

### 自然请求

```
Build a landing page for my SaaS product
Create a dashboard for healthcare analytics
Design a portfolio website with dark mode
Make a mobile app UI for e-commerce
Build a fintech banking app with dark theme
```

### 指定技术栈

```
Build a landing page using React and shadcn/ui
Create a dashboard with Vue and Nuxt UI
Design a mobile app using React Native
```

### 指定设计要求

```
Build a landing page with glassmorphism style
Create a dashboard with dark mode and soft shadows
Design with minimalism and clean typography
```

## 设计系统工作原理

```
1. USER REQUEST → 用户提出请求
       ↓
2. MULTI-DOMAIN SEARCH → 并行搜索（产品类型、样式、颜色、模式、排版）
       ↓
3. REASONING ENGINE → 匹配规则、应用优先级、过滤反模式
       ↓
4. COMPLETE DESIGN SYSTEM → Pattern + Style + Colors + Typography + Effects + Checklist
```

## 交付前检查清单

生成的设计系统包含以下检查项：

- [ ] 不使用 emoji 作为图标（使用 SVG：Heroicons/Lucide）
- [ ] 所有可点击元素有 cursor-pointer
- [ ] 悬停状态有平滑过渡（150-300ms）
- [ ] 亮模式文本对比度至少 4.5:1
- [ ] 键盘导航可见焦点状态
- [ ] 遵循 prefers-reduced-motion
- [ ] 响应式断点：375px、768px、1024px、1440px

## 安装

### Claude Code 市场安装

```bash
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill
```

### CLI 安装

```bash
npm install -g uipro-cli
cd /path/to/your/project
uipro init --ai claude
```

### 前置条件

- Python 3.x 运行搜索脚本
