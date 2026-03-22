---
name: infographic
description: 抖音爆款信息图生成技能，支持8种视觉风格，将复杂知识转化为高密度干货内容。
---

# Infographic 信息图生成技能

将复杂专业知识转化为高密度、视觉化的抖音爆款干货内容。

## 触发条件

- 用户输入 `/infographic`
- 用户要求"生成信息图"、"制作infographic"、"生成干货图"
- 用户想要创建高密度信息图表

---

## 工作流程

### 步骤 1: 展示风格选项

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎨 Infographic 风格选择
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

请选择一种风格（输入数字或名称）：

1️⃣ 打印热敏纸风 - 收据/票据美学，现代新拟物风格
2️⃣ 档案风 - 案件档案板/侦探风格，混合媒体剪贴画
3️⃣ 复古风 - 70年代瑞士网格系统，粗黑描边
4️⃣ 手帐风 - 复古剪贴簿/手绘日志，撕裂纸张元素
5️⃣ 高密度信息大图 - 实验室精密手册感，坐标系统
6️⃣ 票据风 - 剧院票券风格，"五幕剧"叙事结构
7️⃣ 色块风 - Y2K复古未来主义，酸性霓虹色彩
8️⃣ 文件夹风格 - 新拟物文具风，剪贴板+文件夹+标签

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### 步骤 2: 询问用户信息

用户选择风格后，询问以下信息：

```
📝 请提供以下信息，我将为你生成爆款干货内容：
1️⃣ 主题：你想要制作的干货主题是什么？（可以直接提供文章路径或 URL）
2️⃣ 简短描述：用1-2句话描述核心要点或目标受众（可选）
注：默认生成 1 张图片，如需生成多张请主动说明
```

### 步骤 3: 生成高密度内容

根据用户选择的风格，执行对应的风格 Prompt，生成 6-7 个模块的高密度内容。

### 步骤 4: 用户确认

向用户展示生成的内容结构，等待确认：
```
📋 内容已生成，请确认后开始生图：
[展示各模块内容摘要]

确认生图？(确认/修改)
```

### 步骤 5: 模型选择 ⭐

用户确认内容后，询问生成模型：

```
🤖 请选择生成模型：

1️⃣ gemini-3-pro-image-preview-4k（默认）
   - 分辨率：3584×4800, 4K 高清
   - 适合：追求最高画质

2️⃣ nano-banana-2
   - 分辨率：1792×2400, 快速生成
   - 适合：快速出图测试

注：默认使用 gemini-3-pro-image-preview-4k
```

### 步骤 6: 调用图片生成 API

用户确认后，调用图片生成 API 生成实际图片。

**⚠️ 关键规则：串行生成，每张图片独立完成后再进行下一张**

**API 调用方式：**

```bash
# 调用图片生成 API
curl -s -X POST "https://api.tu-zi.com/v1/images/generations" \
  -H "Authorization: Bearer $TUZI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gemini-3-pro-image-preview-4k",
    "prompt": "[完整图片生成Prompt]",
    "size": "3x4",
    "n": 1,
    "response_format": "url"
  }'
```

**API 配置：**
- Base URL: `https://api.tu-zi.com`
- Endpoint: `/v1/images/generations`
- 认证: `Bearer $TUZI_API_KEY` (环境变量，需提前设置)
- 模型选项:
  - `gemini-3-pro-image-preview-4k`（默认）：3584×4800, 4K 高清
  - `nano-banana-2`：1792×2400, 快速生成
- 尺寸选项:
  - `3x4`（默认）：3584×4800, 4K 高清
  - `1792x2400`：1792×2400, 配合 nano-banana-2 使用

**批量生成流程：**

```
对于多张图片请求：

循环处理每张图片：
  1. 显示进度： "📸 正在生成第 X/Y 张..."
  2. 构建完整 Prompt（风格Prompt + 具体内容）
  3. 调用 API 生成图片
  4. 等待 API 响应
  5. 下载并保存图片到本地
  6. 确认保存成功后，显示 "✅ 第X张已保存: <路径>"
  7. 再开始下一张

全部完成后：
  - 汇总显示所有图片路径
  - 显示生成总数
```

**保存图片：**

```bash
# 下载并保存图片
curl -L -s -o "<输出目录>/[主题]_[序号]_[风格].jpg" "<图片URL>"
```

**默认输出目录：** `/Users/bytedance/Documents/trae_projects/xhs-images/`

### 步骤 7: 展示结果

- 显示所有生成图片的路径列表
- 显示成功/失败统计
- 可使用 Read 工具展示图片内容

---

## 风格 Prompt 详细定义

### 风格 1: 打印热敏纸风

**视觉特点：** 收据/票据美学，现代新拟物风格，3D粘土图标

**色彩逻辑：**
- 高对比框架：鲜艳纯色块（亮青色 #00AEEF 或芥末黄 #FFD100）作为背景边框
- 中性核心：米白色/浅灰色 (#F9F9F9) 模拟纸张
- 文字与强调：深炭黑为主色，背景色复用为内部高亮

**设计风格：**
- 现代拟物化（收据/票券美学）：模拟打印收据、票券或标签机
- 排版：复古数字/像素字体标题 + 粗体现代无衬线中文 + 小号英文副标题
- 3D/粘土风格图标：平滑3D渲染图形增加深度

**信息密度原则：**
- 每张图必须包含 6-7 个子主题模块
- 使用收据格式组织密集信息为清晰的逻辑步骤
- 每个模块必须包含具体数据、品牌名称或参数

**图片生成 Prompt：**
```
Create a high-density infographic poster for Douyin about「[主题]」.

STYLE: Modern receipt/ticket aesthetic with perforated edges and 3D skeuomorphic header.

COLOR PALETTE:
- Background border: Vibrant solid color (bright cyan #00AEEF or mustard yellow #FFD100)
- Paper core: Off-white/light gray (#F9F9F9)
- Text: Dark charcoal/black for legibility
- Accent: Reuse background color for highlights

DESIGN ELEMENTS:
- Receipt/ticket layout with cutout or perforated edges
- 3D/claymorphism icons as section anchors
- Hand-drawn style accent colors circling key data points
- Bold sans-serif for main titles, monospaced/pixelated fonts for headers
- Small English subtitles below main headings for layered density

MODULES (6-7 required):
- Module 1: Brand/Option grid
- Module 2: Numerical standards/parameters
- Module 3: Scenario comparison
- Module 4: Identification tips
- Module 5: Recommendations
- Module 6: Warnings (critical)
- Module 7: Quick summary

Aspect Ratio: 3:4 (Portrait)
```

---

### 风格 2: 档案风

**视觉特点：** 案件档案板/侦探风格，混合媒体剪贴画，打字机字体

**色彩逻辑：**
- 基底（中性画布）：米白、奶油色、牛皮纸棕
- 排版（高对比）：深黑和海军蓝
- 强调色：活力绿和红（认证徽章、状态指示器）、柔黄色（和纸胶带）

**设计风格：**
- "证据板"布局：信息像钉在板上的文档
- 模拟纹理：半调图案、撕裂纸边、回形针、胶带纹理
- 排版层次：打字机字体 + 手写体标题 + 粗体无衬线主标题
- 拼贴风格视觉：照片呈现为宝丽来或剪报

**信息密度原则：**
- 每张图必须包含 6-7 个子主题模块
- 剪贴板框架：将6-10个小图像或数据点分组
- 边注：利用文档边缘放置元数据
- 视觉连接器：手绘箭头和虚线引导阅读路径

**图片生成 Prompt：**
```
Create a high-density infographic poster for Douyin about「[主题]」.

STYLE: "Evidence Board" / Detective case file aesthetic with mixed media scrapbook elements.

COLOR PALETTE:
- Base: Off-white, Cream, Kraft Brown (textured paper background)
- Typography: Deep Black and Navy Blue
- Accents: Vibrant Green, Red (status indicators), Soft Yellow (washi tape)

DESIGN ELEMENTS:
- Clipboard or file folder as container for grouped information
- Halftone patterns (dots), torn paper edges, paper clips, tape textures
- Photos as Polaroids or clipped documents
- Typewriter fonts for data, Script/Handwriting for notes
- Hand-drawn arrows and dashed lines as visual connectors

MODULES (6-7 required):
- Module 1 [Classification]: 3-6 specific brands/tiers/options
- Module 2 [Contrast]: Scenarios, "Vs." comparisons
- Module 3 [Hard Data]: Numeric standards, price ranges
- Module 4 [Methodology]: Identification skills or "how-to"
- Module 5 [Applicability]: Scenario recommendations
- Module 6 [Risk Mitigation]: Warnings, common pitfalls
- Module 7 [Quick Reference]: Summary table

Aspect Ratio: 3:4 (Portrait)
```

---

### 风格 3: 复古风

**视觉特点：** 70年代瑞士网格系统，粗黑描边，复古波普网格风格

**色彩逻辑：**
- 画布/背景：温暖复古米黄/米色 (#F5F0E6)
- 平涂强调色：鲑鱼粉、天蓝、芥末黄、薄荷绿
- 视觉锚点：纯黑 (#000000) 和纯白 (#FFFFFF) 块
- 线条艺术：粗黑描边

**设计风格：**
- 1970年代复古波普艺术 + 地下漫画插画风格
- 严格瑞士国际网格系统布局
- 纯2D平面矢量美学，丝网印刷质感
- 统一粗黑描边用于所有插画、文本框、网格分隔线
- 绝对禁止渐变、阴影、3D效果

**信息密度原则：**
- 每张图必须包含 6-7 个子主题模块
- 将海报分割为多个方形和矩形格子
- 文字与图形分离：某些格子纯文字，某些纯插画
- 反转对比：关键警告或主要类别必须用白字黑底

**图片生成 Prompt：**
```
Create a flat graphic design infographic poster for Douyin about「[主题]」.

STYLE: 1970s retro pop art and underground comic illustration style.
- Strict Swiss international grid system layout
- Pure 2D flat vector aesthetic with subtle screen print texture
- Uniform THICK BLACK outlines for ALL illustrations, text boxes, and grid dividers
- ABSOLUTELY NO gradients, shading, drop shadows, or 3D effects

COLOR PALETTE (RETRO POP):
- Canvas/Background: Warm vintage cream/beige (#F5F0E6)
- Flat Accent Colors: Salmon pink, sky blue, mustard yellow, mint green
- Visual Anchors: Solid pure black (#000000) and solid pure white (#FFFFFF)
- Line art & Outlines: Solid thick black

GRID MODULES (6-7 required):
- [Grid 1: Brand Selection] - Sub-grids with brand icons and names
- [Grid 2: Specification Data] - Flat ruler or bar charts
- [Grid 3: Scenario Comparison] - Side-by-side contrasting cells
- [Grid 4: Types/Models] - Abstract flat cross-sections
- [Grid 5: Tips] - List format with bold black checkmarks
- [Grid 6: Warning Zone] - Solid BLACK background with WHITE text
- [Grid 7: Summary] - Highly structured mini-grid table

TYPOGRAPHY:
- Bold, highly legible sans-serif or retro display fonts
- All text in CHINESE (except decorative English like "WARNING")
- No cursive or messy handwriting

Aspect Ratio: 3:4 (Portrait)
```

---

### 风格 4: 手帐风

**视觉特点：** 复古剪贴簿/手绘日志，撕裂纸张、图钉、回形针元素

**色彩逻辑：**
- 调色板：复古大地色调（牛皮纸棕、奶油白）
- 功能强调：大胆红色和明亮黄色
- 纹理：撕裂纸边、网格纸、红色图钉、回形针

**设计风格：**
- "复古调查"风格：侦探证据板或复古日志美学
- 元素：撕裂纸边、网格纸、红色图钉、回形针、虚线连接器
- 插画：极简黑色线条艺术（手绘风格）

**信息密度原则：**
- 每张图必须包含 6-7 个子主题模块
- 使用视觉隐喻如撕裂便条、回形针、放大镜分离信息层次
- 避免模糊描述，使用具体价格、百分比、规格、品牌名称

**图片生成 Prompt：**
```
Create a high-density infographic poster for Douyin about「[主题]」.

STYLE: Vintage Scrapbook & Hand-drawn Journal / Detective Evidence Board aesthetic.

COLOR PALETTE:
- Base: Vintage Earth Tones (Kraft paper brown, Cream white)
- Accents: Bold Red and Bright Yellow for functional highlights

DESIGN ELEMENTS:
- Torn paper edges, grid paper textures
- Red push pins, paper clips, dashed line connectors
- Minimalist black line art (hand-drawn style) for each module
- Magnifying glasses, taped notes, vintage stamps

MODULES (6-7 required):
- Module 1 [Identity]: Classification/Level (3-6 specific tiers/brands)
- Module 2 [Contrast]: Comparison/Scenarios (Pros vs Cons)
- Module 3 [Technical]: Standards/Parameters (Hard data)
- Module 4 [Skillset]: Recognition/Methods (Step-by-step)
- Module 5 [Application]: Recommended Scenarios
- Module 6 [Risk Control]: Common Pitfalls/Warnings
- Module 7 [Quick Reference]: Summary chart

Aspect Ratio: 3:4 (Portrait)
```

---

### 风格 5: 高密度信息大图（坐标蓝图·波普实验室版本）

**视觉特点：** 实验室精密手册感，坐标系统，技术图纸风格

**色彩逻辑：**
- 背景：专业灰白或淡蓝图网格纹理 (#F2F2F2)
- 系统基底：柔和青绿/鼠尾草绿 (#B8D8BE) 用于主要功能块
- 高警告强调：荧光粉 (#E91E63) 严格用于"陷阱"、"关键警告"或最重要数据
- 标记高亮：鲜艳柠檬黄 (#FFF200) 用于关键词高亮
- 线条艺术：超细炭棕 (#2D2926) 用于技术网格和坐标

**设计风格：**
- "实验室手册"美学：微观细节（技术图纸）+ 宏观数据（大粗标题）
- 信息作为坐标：每个模块必须有坐标式标签（如 R-20, G-02, SEC-08）
- 高密度：每张图打包 6-7 个独立模块，最小化边距
- 视觉对比：巨大粗体排版标题 vs 超精细技术注释（8pt外观）

**图形元素：**
- 技术图表：爆炸视图、带锚点的剖面图、建筑骨架线
- 坐标系统：带精确标记的垂直/水平标尺（如 0.5mm, 1.8mm, 45°）
- 数据块："标记覆盖印刷"外观 - 色块略微偏移于高亮文字
- 符号：十字瞄准目标、数学符号（Σ, Δ, ∞）、方向箭头（X/Y轴）

**信息密度原则：**
- 每张图必须包含 6-7 个独立信息块
- 看起来像一份复杂的研究报告
- 每个角落都应包含元数据如微小条形码、时间戳、技术参数

**图片生成 Prompt：**
```
Create a high-density, professional information design infographic for Douyin about「[主题]」.

=== CRITICAL STYLE REQUIREMENTS (SYSTEMIC & EXPERIMENTAL) ===

COLOR PALETTE - BLUEPRINT & POP LOGIC:
- BACKGROUND: Professional grayish-white or faint blueprint grid texture (#F2F2F2)
- SYSTEMIC BASE: Muted Teal/Sage Green (#B8D8BE) for major functional blocks
- HIGH-ALERT ACCENT: Vibrant Fluorescent Pink (#E91E63) for critical warnings or key data
- MARKER HIGHLIGHTS: Vivid Lemon Yellow (#FFF200) for keyword highlights
- LINE ART: Ultra-fine Charcoal Brown (#2D2926) for technical grids

LAYOUT & INFORMATION DENSITY:
- INFORMATION AS COORDINATES: Every module must have coordinate-style label (R-20, G-02, SEC-08)
- THE "LAB MANUAL" AESTHETIC: Mix of microscopic details and macroscopic data
- HIGH DENSITY: Pack 6-7 distinct modules per image. Minimize margins.
- VISUAL CONTRAST: Massive bold typography vs tiny ultra-crisp technical annotations

ILLUSTRATION & GRAPHIC ELEMENTS:
1. TECHNICAL DIAGRAMS: Exploded views, cross-sections with anchor points
2. COORDINATE SYSTEMS: Vertical/horizontal rulers with precise markers
3. DATA BLOCKS: "Marker-over-Print" look - color blocks slightly offset
4. SYMBOLS: Cross-hair targets, mathematical symbols (Σ, Δ, ∞), directional arrows

SPECIFIC MODULE STRUCTURE (6-7 required):
- [MOD 1: BRAND ARRAY] - 4x4 or 3x3 matrix with one "Best Choice" in Pink
- [MOD 2: SPECS SCALE] - Technical ruler showing "Standard" vs "Premium"
- [MOD 3: DEEP DIVE] - Technical sketch with zoom-in callout circles
- [MOD 4: SCENARIO GRID] - Comparison cards separated by fine 0.5pt hair-lines
- [MOD 5: WARNING ZONE] - High-contrast Pink/Black area for "Pitfalls"
- [MOD 6: QUICK CHECK] - Dense summary table resembling lab data sheet
- [MOD 7: STATUS BAR] - Vertical/horizontal stack of information blocks

TYPOGRAPHY:
- Headers: Bold Brutalist Chinese characters, high impact
- Body: Professional sans-serif or crisp handwritten technical print
- Numbers: Large, highlighted with Yellow or Blue

AVOID:
- NO cute/cartoonish doodles
- NO soft pastels or generic textures
- NO empty white space
- NO flat vector stock icons

Aspect Ratio: 3:4 (Portrait)
```

---

### 风格 6: 票据风

**视觉特点：** 剧院票券/电影票风格，"五幕剧"叙事结构

**色彩逻辑：**
- 背景：深海军蓝或深炭灰，带细微颗粒纹理（黑色电影感）
- 主要元素：重叠复古剧院票券、锯齿边纸收据、金属回形针
- 色调：青色、金丝雀黄、珊瑚粉、薄荷绿与深色背景高对比

**设计风格：**
- 视觉系列化：将复杂数据转化为"五幕剧"或"系列票券"叙事
- 电影美学：颗粒纹理、打字机字体、复古纸张元素
- 模块效率：在单个艺术分层画布中组织 6-7 个数据密集子模块

**"五幕剧"结构：**
- 第一幕：钩子/问题（定义与痛点）
- 第二幕：铺垫（分类与等级列表）
- 第三幕：高潮（核心解决方案与硬数据）
- 第四幕：转折（陷阱与反直觉技巧）
- 第五幕：结局（检查清单与行动号召）

**图片生成 Prompt：**
```
Create a high-density infographic poster for Douyin about「[主题]」.

STYLE: Theater-Ticket & Scrapbook Style with "5-Act Play" narrative structure.

COLOR PALETTE:
- Background: Deep Navy or Dark Charcoal with subtle grainy texture (Film Noir feel)
- Primary Elements: Overlapping vintage theater tickets, jagged-edged paper receipts
- Accents: Teal, Canary Yellow, Coral Pink, Mint Green against dark backdrop

DESIGN ELEMENTS:
- Vintage theater tickets with "Act 01, Act 02" labels on the side
- Jagged-edged paper receipts, metal paper clips holding script pages
- Bold Serif titles and fine-print Monospaced text (Typewriter style)
- Asymmetrical collage with clear visual hierarchy

5-ACT STRUCTURE:
- Act 1: The Hook/Problem (Definitions & Pain Points)
- Act 2: The Setup (Categorization & Tier Lists)
- Act 3: The Climax (Core Solutions & Hard Data)
- Act 4: The Twist (Pitfalls & Counter-intuitive Tips)
- Act 5: The Resolution (Checklist & Call to Action)

Each "Ticket" or "Act" must contain 6-7 granular data points.

Aspect Ratio: 3:4 (Portrait)
```

---

### 风格 7: 色块风

**视觉特点：** Y2K复古未来主义，酸性霓虹色彩，高对比度

**色彩逻辑：**
- 调色板：高对比酸性色彩（赛博黄、电橙、霓虹绿）
- 背景：深炭灰，带重度颗粒纹理
- 视觉元素：3D像素化硬件（老式PC、CD）、彩虹渐变、贴纸风格标签

**设计风格：**
- 复古未来主义 / 酸性图形风格
- 不对称模块网格，粗重无衬线标题
- Y2K科技怀旧美学

**信息密度原则：**
- 每张图必须包含 6-7 个子主题模块
- 排版紧凑以容纳最大信息量
- 丰富优于简洁：确保每个模块有具体数据/规格/品牌名称

**图片生成 Prompt：**
```
Create a high-density infographic poster for Douyin about「[主题]」.

STYLE: Retro-Futurist / Acid Graphic style with Y2K Tech-Nostalgia aesthetic.

COLOR PALETTE:
- Background: Dark Charcoal with heavy grain texture
- High-contrast Acid colors: Cyber Yellow, Electric Orange, Neon Green
- Rainbow gradients, sticker-style labels

DESIGN ELEMENTS:
- 3D pixelated hardware (Old PCs, CDs), sticker-style labels
- Asymmetric Modular Grid with bold, heavy sans-serif headers
- High-contrast neon accents against dark background

MODULES (6-7 required):
- Module 1: Naming (3-6 brands/options/levels)
- Module 2: Comparison (tiers/scenarios/pros & cons)
- Module 3: Standardization (numerical values/technical parameters)
- Module 4: Methodology (identification tips/steps)
- Module 5: Recommendation (usage scenarios/suitability)
- Module 6: Warning (common pitfalls/precautions)
- Module 7: Summary (Quick reference/Checklist)

Aspect Ratio: 3:4 (Portrait)
```

---

### 风格 8: 文件夹风格

**视觉特点：** 新拟物文具风，剪贴板+文件夹+标签，3D渲染感

**色彩逻辑：**
- 背景：奶油/米色 (#F5F5DC)
- 主色调：克莱因蓝用于主要项目
- 强调色：活力橙用于重点
- 文字：柔灰色

**设计风格：**
- 新拟物化文具风格，3D渲染感，整洁有序
- 垂直剪贴板，带分层文件夹和索引标签
- 3D鼠标光标和通知图标作为装饰元素
- 大粗无衬线标题，子模块在文件夹内按列表样式组织

**信息密度原则：**
- 每张图必须包含 6-7 个子主题模块
- 信息丰富度优先于空旷美学
- 每个模块必须有具体数据、品牌名称或技术参数支持

**图片生成 Prompt：**
```
Create a high-density infographic poster for Douyin about「[主题]」.

STYLE: Neo-skeuomorphism stationery style, 3D render feel, clean and organized.

COLOR PALETTE:
- Background: Cream/Beige (#F5F5DC)
- Main items: Klein Blue accents
- Emphasis: Vibrant Orange
- Text: Soft Grey

DESIGN ELEMENTS:
- Vertical clipboard with layered folders and index tabs
- 3D mouse cursor and notification icons as decorative elements
- Large bold sans-serif headers
- Sub-modules organized within list-style document inside folder

MODULES (6-7 required):
- Module 1: Naming (3-6 brands/options/levels)
- Module 2: Comparison (tiers/scenarios/pros & cons)
- Module 3: Standardization (numerical values/technical parameters)
- Module 4: Methodology (identification tips/steps)
- Module 5: Recommendation (usage scenarios/suitability)
- Module 6: Warning (common pitfalls/precautions)
- Module 7: Summary (Optional: Quick reference/Checklist)

Maintain consistency with clipboard, the sidebar tags, and folder styling.

Aspect Ratio: 3:4 (Portrait)
```

---

## 通用内容结构模板

所有风格的图片都应遵循以下高密度内容结构：

```markdown
## 图片 [X]：[核心主题名称]

**主标题：** [主题名称] 选择指南 / [主题名称] 避坑攻略
**副标题：** X大维度全面解析

### 模块内容（6-7个模块）：

**[模块1，4字]** - 品牌/选项类
- 品牌A：[图标] [名称]：[描述]
- 品牌B：[图标] [名称]：[描述]

**[模块2，4字]** - 数值阶梯类
- [数值1]：❌ 不合格
- [数值2]：✓ 良好
- [数值3]：👑 优秀

**[模块3，4字]** - 场景对比类
- 场景A：[图标] [具体建议+数据]
- 场景B：[图标] [具体建议+数据]

**[模块4，4字]** - 识别技巧类
- 看：[具体方法]
- 测：[具体方法]

**[模块5，4字]** - 对比表格类
（使用适合风格的表格形式）

**[模块6，4字]** - 避坑提醒类
⚠️ 避坑清单：
- ❌ [错误做法1]：[后果]
- ❌ [错误做法2]：[后果]

**[模块7，4字]**（可选）- 快速总结类
💡 要点速览 / 一句话总结
```

---

## 质量检查清单

生图前必须确认：

- [ ] 模块数量是否达到 6-7 个？
- [ ] 每个模块是否包含具体数据（品牌名、数值、参数）？
- [ ] 风格 Prompt 是否完整粘贴？
- [ ] 是否指定了精准的配色方案？
- [ ] 警告/避坑模块是否设定为最具视觉冲击力的样式？

---

## 示例对话

```
用户: /infographic

助手: [展示8种风格选项]

用户: 5

助手: 已选择「高密度信息大图」风格！

📝 请提供以下信息：
1️⃣ 主题：你想要制作的干货主题是什么？（可以直接提供文章路径或 URL）
2️⃣ 简短描述：用1-2句话描述核心要点或目标受众（可选）


注：默认生成 1 张图片，如需生成多张请主动说明

用户：主题是咖啡豆选购指南，目标受众是咖啡爱好者

助手: [按照高密度信息大图 prompt 流程执行...]
```
