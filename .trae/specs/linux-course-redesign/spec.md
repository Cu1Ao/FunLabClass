# Linux 课程页面重构规格说明

## Why
当前 Linux 课程页面（linux/index.html）视觉风格较为朴素，缺乏科技感和交互体验。需要打造一个高端产品官网级别的视觉效果，提升用户体验和课程吸引力。

## What Changes
- **整体风格**：黑绿色调，科技感高端产品官网风格
- **Hero 区域**：添加动态粒子背景（Canvas）
- **课程地图**：左右布局，左侧课程文字描述，右侧 SVG 动画连线图展示课程架构
- **交互动画**：
  - 滚动时元素淡入（Intersection Observer）
  - 架构图连线流动动画
  - 参数卡片 hover 光晕效果
- **技术实现**：单文件 HTML，内嵌 CSS/JS，使用 Tailwind CSS CDN，不依赖外部图片

## Impact
- Affected specs: linux/index.html 完全重构
- Affected code: 仅修改 `linux/index.html` 文件

## ADDED Requirements

### Requirement: 动态粒子背景
页面 Hero 区域应使用 Canvas 实现动态粒子效果。

#### Scenario: 页面加载时
- **WHEN** 用户打开 Linux 课程页面
- **THEN** Hero 区域显示动态粒子背景，粒子数量约 80-100 个，粒子颜色为绿色 (#00FF41)，带有连线效果

### Requirement: 课程架构 SVG 连线图
右侧 SVG 区域展示课程模块的连线关系。

#### Scenario: 查看课程架构
- **WHEN** 用户查看课程地图区域
- **THEN** SVG 显示课程模块的节点和连接线，连线有流动动画效果（虚线流动）

### Requirement: 滚动淡入动画
页面元素在滚动进入视口时淡入显示。

#### Scenario: 滚动浏览页面
- **WHEN** 用户滚动页面，元素进入视口
- **THEN** 元素从 opacity: 0, translateY: 30px 动画过渡到 opacity: 1, translateY: 0，过渡时长 600ms

### Requirement: 参数卡片光晕效果
课程模块卡片在 hover 时显示光晕效果。

#### Scenario: 鼠标悬停卡片
- **WHEN** 用户鼠标悬停在课程模块卡片上
- **THEN** 卡片边框发出绿色光晕 (box-shadow: 0 0 30px rgba(0, 255, 65, 0.4))

## MODIFIED Requirements

### Requirement: 返回按钮
保持左上角固定定位返回主页按钮。

#### Scenario: 点击返回按钮
- **WHEN** 用户点击返回按钮
- **THEN** 页面跳转到 ../index.html

## REMOVED Requirements
无

## Design Specifications

### Color Palette
- Primary: `#00FF41` (Terminal Green)
- Secondary: `#0D1117` (Dark Background)
- Accent: `#238636` (Darker Green)
- Text Primary: `#E6EDF3`
- Text Secondary: `#8B949E`

### Typography
- Primary Font: JetBrains Mono (code/monospace elements)
- Secondary Font: Noto Sans SC (中文内容)

### Layout Structure
1. **Hero Section** (100vh)
   - 动态 Canvas 粒子背景
   - 居中课程标题 "Linxu 系统管理"
   - 副标题和标签

2. **Course Map Section**
   - 左列：课程模块卡片列表
   - 右列：SVG 架构图（节点+连线）

3. **Learning Path Section**
   - 学习路径时间线

4. **Footer**
   - 版权信息和返回链接