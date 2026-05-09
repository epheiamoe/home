<img src="./assets/favicon.png" align="right" alt="Logo" width="120" />

# Yumeka's Home

简约可爱的个人主页 🐰✨ [点此预览](https://yumeka.blog/)

[![MIT License](https://img.shields.io/badge/License-MIT-pink.svg?style=flat-square)](./LICENSE)
![Vanilla JS](https://img.shields.io/badge/JavaScript-Vanilla-yellow?logo=javascript&style=flat-square)
![No Build](https://img.shields.io/badge/Build-None-success.svg?style=flat-square)

## 快速开始

1. 下载本仓库
2. 修改根目录下的 `site.yaml` 配置文件
3. 通过 GitHub Pages 或任何静态托管平台发布

## 配置方式

本站所有可配置内容集中在 **`site.yaml`** 一个文件中，无需编辑 HTML。YAML 语法简洁直观，支持注释。

`site.yaml` 包含四个顶级段（对应四个页面）：

### 主页 `site`

```yaml
site:
  font: "./renderer/assets/font.woff2"

  profile:
    title: "Yumeka の 主页"
    avatar: "./assets/avatar.jpg"
    aliases:
      - label: "@KlxPiao"
        tooltip: "描述文字"
        copy: "复制内容"

  about:
    heading: "关于我"
    traits:
      - icon: "fa-solid fa-user"
        tooltip: "特质描述"
    bio: "支持 HTML 的自我介绍..."
    tags:
      - text: "标签名"
        copy: "点击复制的内容"

  portals:
    heading: "传送门"
    items:
      - title: "项目名"
        desc: "简短描述"
        url: "https://example.com/"
        icon: "fa-solid fa-link"

  contact:
    heading: "找到我"
    links:
      - icon: "fa-brands fa-github"
        url: "https://github.com/username"
        isCopy: false
      - icon: "fa-brands fa-qq"
        val: "123456789"
        isCopy: true
        msg: "QQ 号码"

  footer: "页脚 HTML 内容"
```

### 旗帜生成器 `flag`

```yaml
flag:
  state:
    width: 1920
    height: 1080
    format: "png"
    orientation: "horizontal"
    currentFlag: "pride"

  flags:
    pride:
      name: "旗帜名称"
      colors:
        - name: "颜色名"
          hex: "#E40303"
          rgb: "228, 3, 3"
          cmyk: "0, 99, 99, 11"
          pms: "185 C"
      pattern:
        - "#E40303"
        - "#FF8C00"
```

> 注意：`bisexual` 旗帜使用自定义 Canvas 绘制逻辑（非等宽条纹），其 `draw` 函数保留在 `flag/index.html` 的 JS 代码中。YAML 中只需定义其 `colors` 数据，无需定义 `pattern`。

### 表情包生成器 `meme`

```yaml
meme:
  params:
    text: "不出来"
    brightness: 100
    saturation: 80
    blur: 4
    gamma: 1.1
    glow: 4
    iconSize: 10
    iconBlur: 0.7
    bottomBarHeight: 100
    contentScale: 1.1
    relativeFontSize: 60
    spacing: 8
```

### Chat Renderer `renderer`

```yaml
renderer:
  settingsSchema:
    - key: "--font-size"
      label: "全局字号大小"
      type: "number"
      def: 16
      min: 12
      max: 32
      step: 1
      unit: "px"

    - key: "--font-family"
      label: "字体族或路径"
      type: "string"
      def: "./assets/font.woff2"
      placeholder: "./assets/font.woff2"
```

## 演示样式 vs 内容数据

`site.yaml` 中**仅包含内容数据**。所有展示样式（CSS 类名、颜色、渐变背景、悬浮效果等）由各 HTML 的 JS 逻辑层统一控制。如需调整样式，请编辑对应 HTML 文件中的样式数组：

| 区域 | 位置（index.html） | 说明 |
|---|---|---|
| 特质配色 | `traitColors` 数组 | 按顺序对应每个 trait |
| 标签样式 | `tagStyles` 数组 | 按顺序对应每个 tag |
| 传送门背景 | `portalBgs` 数组 | 按顺序对应每个 portal |
| 联系链接悬浮色 | `linkHover` 数组 | 按顺序对应每个 link |

## 页面加载流程

1. HTML 加载静态结构和样式
2. `vendor/js-yaml.min.js` 提供 YAML 解析能力
3. 各页面通过 `fetch('./site.yaml')` 异步加载配置文件
4. `yaml.load()` 解析后注入变量，触发渲染

## 项目结构

```
home/
├── site.yaml                   ← 集中配置文件（所有内容）
├── vendor/
│   └── js-yaml.min.js          ← YAML 解析库（本地化）
├── index.html                  ← 主页
├── flag/index.html             ← 旗帜生成器
├── meme/index.html             ← 表情包生成器
├── renderer/index.html         ← Chat Renderer
├── assets/                     ← 静态资源
├── README.md
└── LICENSE
```

## 图标

图标库由 Font Awesome 驱动。在 `site.yaml` 中使用 `fa-xxx` 类名（如 `fa-solid fa-heart`、`fa-brands fa-github`）指定图标。可用图标列表参见 [Font Awesome 图标库](https://fontawesome.com/search)。
