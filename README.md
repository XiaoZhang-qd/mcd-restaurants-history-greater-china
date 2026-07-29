# 🍔 大中华麦当劳旧址档案地图(xiaozhang-qd.github.io/mcd-restaurants-history-greater-china/)

> 记录麦当劳在大中华区（中国大陆、香港、澳门、台湾）的历史门店变迁，保留城市商业记忆。

## 📖 项目简介

##### **网站：**[https://xiaozhang-qd.github.io/mcd-restaurants-history-greater-china/](https://xiaozhang-qd.github.io/mcd-restaurants-history-greater-china/)

本项目是一个基于 Leaflet 的交互式地图，可视化展示大中华区麦当劳门店的历史变迁。通过标注原址营业、搬迁、拆除等状态，让用户直观了解城市商业地标的演变。

麦当劳自 1990 年进入中国市场以来，在大中华区（内地(中国大陆)、香港、澳门、台湾）的城市变迁中留下了无数记忆。从繁华商圈的旗舰店到社区街角的小门店，它们不仅是餐饮场所，更是一代人的童年印记、城市发展的见证者。

然而，随着城市更新、商业迭代，许多承载着回忆的老店悄然关闭或搬迁。**本项目旨在通过社区协作的方式，系统地收集、整理和归档大中华区麦当劳旧址的历史信息**，让这些城市记忆得以延续。

我们希望构建一份动态的麦当劳旧址地图，记录每一家门店的位置变迁、开业与结业时间、历史照片以及背后的故事。无论你是老员工、常客、路过的居民，还是对城市历史感兴趣的研究者，你的每一份投稿都将为这份公共记忆添砖加瓦。


### ✨ 功能特性

- 🗺️ **三套底图切换**：OSM 标准 / 高德街道 / Stamen 地形
- 🔍 **本地搜索**：按门店名称、城市、地址模糊搜索（支持历史地址）
- 🎛️ **状态筛选**：按营业/搬迁/拆除状态筛选
- 📍 **状态标记**：四种颜色圆圈标记不同现状
  - 🟢 原址营业（still_open_original）
  - 🟡 同楼搬迁（moved_same_building）
  - 🟠 商号远迁（moved_far_away）
  - 🔴 建筑拆除（building_gone）
- 📜 **历史变迁时间线**：点击门店查看有序的搬迁历史（原址 → 第一次搬迁 → 第二次搬迁...）
- 📝 **文字地址支持**：地址字段支持纯文字描述，不仅限经纬度坐标
- 📱 **响应式设计**：手机端自动适配
- 📮 **投稿系统**：GitHub Issue 自动解析 + 邮件通知

## 🛠️ 技术栈

- **原生 HTML + CSS + JavaScript**，零构建
- **Leaflet 1.9.4**（CDN 引入）
- **GitHub Pages** 静态部署
- **GitHub Actions** 自动化投稿解析

## 📁 项目结构

```
mcd-history-greater-china/
├── index.html                    # 主页面
├── data/
│   └── sample.geojson            # 门店数据（GeoJSON 格式）
├── README.md                     # 项目说明
└── .github/
    ├── workflows/
    │   └── issue-submit.yml      # GitHub Actions 投稿解析
    └── ISSUE_TEMPLATE/
        └── old-store-submit.md   # 投稿模板
```

## 📊 数据格式

### GeoJSON Properties 字段说明

每个门店要素的 `properties` 支持以下字段：

| 字段 | 类型 | 必填 | 说明 | 示例 |
|------|------|------|------|------|
| `name` | string | ✅ | 门店全称 | `广州第一家麦当劳（63层广东国际大厦首层）` |
| `region` | string | ✅ | 地区 | `中国‑广东省` |
| `city` | string | ✅ | 城市 | `广州` |
| `address` | string | ✅ | 当前/最近一次搬迁后的详细地址（支持纯文字） | `广州市越秀区环市东路 63 层广东国际大厦二楼` |
| `open_year` | string | ✅ | 原址开业时间 | `1993‑02‑20` |
| `close_year` | string | ✅ | 原址结业/搬迁时间 | `2010‑03‑31` 或 `营业中` |
| `status_key` | string | ✅ | 状态键（见下方） | `moved_same_building` |
| `status` | string | ✅ | 完整历史描述 | `大楼尚存；商号搬迁至本大厦二楼...` |
| `photo_url` | string | ❌ | 当前门店老照片链接（可为空） | `https://...`/`http://...` |
| `locations` | array | ❌ | 有序历史变迁序列（见下方） | 见[locations数组说明](#locations数组说明) |

### locations 数组（历史变迁序列）

`locations` 数组按序号依次记录门店的搬迁历史，从 **1（原址）** 开始：

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `seq` | number | ✅ | 序号，从 1 开始 |
| `label` | string | ✅ | 位置标签，如：原址、同楼搬迁、现址 |
| `address` | string | ✅ | 该位置的详细地址（支持纯文字） |
| `open_year` | string | ❌ | 该位置的开业时间 |
| `close_year` | string | ❌ | 该位置的结业/搬迁时间 |
| `coordinates` | [lng, lat] | ❌ | 该位置的 WGS-84 GPS 坐标 |
| `photo_url` | string | ❌ | 该位置的老照片链接 |

### status_key 状态枚举

| 状态键 | 含义 | 颜色 |
|--------|------|------|
| `still_open_original` | 原址营业 | 🟢 #2ecc71 |
| `moved_same_building` | 同楼搬迁 | 🟡 #f1c40f |
| `moved_far_away` | 商号远迁 | 🟠 #e67e22 |
| `building_gone` | 建筑拆除 | 🔴 #e74c3c |

### GeoJSON 示例

```json
{
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [113.2644, 23.1291]
  },
  "properties": {
    "name": "广州第一家麦当劳（63层广东国际大厦首层）",
    "region": "中国‑广东省",
    "city": "广州",
    "address": "广州市越秀区环市东路 63 层广东国际大厦二楼",
    "open_year": "1993‑02‑20",
    "close_year": "2010‑03‑31",
    "status_key": "moved_same_building",
    "status": "大楼尚存；商号搬迁至本大厦二楼；首层现为银行酒馆，无纪念牌匾",
    "photo_url": "",
    "locations": [
      {
        "seq": 1,
        "label": "原址",
        "address": "广州市越秀区环市东路 63 层广东国际大厦首层",
        "open_year": "1993‑02‑20",
        "close_year": "2010‑03‑31",
        "coordinates": [113.2644, 23.1291],
        "photo_url": ""
      },
      {
        "seq": 2,
        "label": "同楼搬迁",
        "address": "广州市越秀区环市东路 63 层广东国际大厦二楼",
        "open_year": "2010‑04‑01",
        "close_year": "营业中",
        "photo_url": ""
      }
    ]
  }
}
```

> ⚠️ **坐标系说明**：项目使用 **WGS-84** GPS 经纬度（标准 GPS 坐标）。地址字段支持纯文字描述，坐标仅用于地图定位。高德地图使用 GCJ-02 火星坐标系，切换到高德底图时坐标会自动转换。

## 📮 投稿指南

### 方式一：通过 GitHub Issue 投稿（推荐）

1. 点击 [👉 前往投稿](https://github.com/xiaozhang-qd/mcd-restaurants-history-greater-china/issues/new?template=old-store-submit.md)
2. 按照模板格式填写门店信息
3. 提交 Issue 后，GitHub Actions 会自动：
   - 解析投稿内容
   - 生成待审核的 GeoJSON Feature
   - 发送邮件通知你
4. 你审核通过后，将 Feature 合并到 `data/sample.geojson`

### 方式二：手动编辑

直接编辑 `data/sample.geojson`，添加新的 Feature 条目，然后提交 PR。

## ⚙️ GitHub Actions 配置

投稿解析工作流位于 `.github/workflows/issue-submit.yml`，需要配置以下 Secrets：

| Secret | 说明 |
|--------|------|
| `SMTP_SERVER` | SMTP 服务器地址（如 `smtp.qq.com`） |
| `SMTP_PORT` | SMTP 端口（如 `465`） |
| `SMTP_SECURE` | 是否加密（`true`） |
| `SMTP_USERNAME` | 邮箱账号 |
| `SMTP_PASSWORD` | 邮箱 SMTP 授权码 |
| `MAIL_TO` | 接收通知的邮箱 |
| `MAIL_FROM` | 发件人地址 |

### 配置步骤

1. Fork 本仓库，进入你自己的 `mcd-restaurants-history-greater-china` GitHub 仓库 → **Settings** → **Secrets and variables** → **Actions**
2. 点击右上角 **New repository secret**，依次添加上表中的 7 个 Secrets（名称需完全一致，区分大小写）
3. 每个 Secret 的值填写完毕后，点击 **Add secret** 保存
4. 进入仓库 **Settings** → **General** → **Features** 区域，勾选启用 **Issues** 功能
5. （可选）进入仓库 **Actions** 标签页，手动触发一次 `issue-submit` 工作流，验证配置是否生效

## 🚀 部署到 GitHub Pages

1. 将所有文件推送到 GitHub 仓库
2. 进入仓库 → **Settings** → **Pages**
3. Source 选择 `main` 分支 / `root` 目录
4. 保存后访问 `https://yourname.github.io/mcd-restaurants-history-greater-china/`

## 📄 开源协议

本项目数据仅供参考学习使用。
