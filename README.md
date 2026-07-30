# 🍔 大中华麦当劳旧址档案地图(xiaozhang-qd.github.io/mcd-restaurants-history-greater-china/)

> 记录麦当劳在大中华区（中国大陆、香港、澳门、台湾）的历史门店变迁，保留城市商业记忆。

## 📖 项目简介

##### **网站：**[https://xiaozhang-qd.github.io/mcd-restaurants-history-greater-china/](https://xiaozhang-qd.github.io/mcd-restaurants-history-greater-china/)

本项目是一个基于 Leaflet 的交互式地图，可视化展示大中华区麦当劳门店的历史变迁。通过标注原址营业、搬迁、拆除等状态，让用户直观了解城市商业地标的演变。

麦当劳自 1990 年正式踏入大中华市场以来，见证了数十年城市快速变迁。从内地首家深圳光华餐厅起步，金拱门的足迹遍布中国大陆、香港、澳门与台湾各地。无论是市中心繁华商圈的标志性旗舰店，老城区街角陪伴街坊多年的社区门店，还是一代人心心念念的生日聚会据点；这些餐厅早已超越单纯的餐饮场所，成为改革开放时代印记、城市商业迭代的鲜活见证，更是无数人难以复刻的童年记忆与青春碎片。

时代浪潮不停向前，旧城改造、商圈更迭、租约到期、业态调整持续发生。大量承载本土记忆的老牌麦当劳门店悄然搬迁、永久结业。许多老店的历史资料零散分布在社交平台、网友相册，随着时间推移不断流失，系统化的公开档案长期处于空白状态。
本项目旨在依靠社区协作模式，系统性采集、整理、归档大中华区麦当劳老店、旧址完整历史资料，搭建一份可持续维护的公共城市记忆档案，留住即将消散的城市商业历史。

项目将构建一份交互式动态旧址地图，完整记录每一处门店全生命周期信息：历代地理位置变迁、准确开业与结业年份、门店外观历史影像、建筑特征、搬迁沿革，以及市民留存的私人回忆与故事。

无论你是曾经的门店员工、常年光顾的老顾客、本地居民，或是城市发展史、商业史爱好者；你提供的门店地址、老照片、开业结业时间、亲身见闻，都将填补档案空缺，共同留存这份属于大中华地区的集体记忆。


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
    │   └── issue-submit.yml      # GitHub Actions 投稿解析工作流
    └── ISSUE_TEMPLATE/
        ├── config.yml   # 投稿模板配置
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

1. 点击 [👉 前往投稿](https://github.com/XiaoZhang-qd/mcd-restaurants-history-greater-china/issues/new?template=old-store-submit.md)
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
