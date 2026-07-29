---
name: 老店投稿
about: 提交一家大中华区麦当劳旧址信息
title: "🏪 投稿：[城市] [门店名称]"
labels: ["新门店投稿"]
assignees: ""
---

## 投稿说明

在提交之前，请仔细阅读以下要求：

- ✅ **信息真实**：请尽可能提供准确的时间、地址和历史描述
- ✅ **格式规范**：严格遵循下方模板中的字段名，便于系统自动解析
- ✅ **来源可靠**：如有历史照片，请注明拍摄时间或来源
- ✅ **尊重事实**：对于不确定的信息，请标注"待核实"而非臆造

## 投稿方法

### 通过 GitHub Issue 投稿，进入[https://github.com/xiaozhang-qd/mcd-restaurants-history-greater-china/issues/new?template=old-store-submit.md](https://github.com/xiaozhang-qd/mcd-restaurants-history-greater-china/issues/new?template=old-store-submit.md)

## 📋 请按以下格式填写（严格遵循字段名，方便自动解析）

### 基础信息

```
name: 
region: 
city: 
address: 
open_year: 
close_year: 
status_key: 
status: 
photo_url: 
```

### 字段说明

| 字段 | 是否必填 | 说明 |
| `name` | ✅ 必填 | 门店全称，如：广州第一家麦当劳（63层广东国际大厦首层） |
| `region` | ✅ 必填 | 地区，如：中国‑广东省、香港特别行政区 |
| `city` | ✅ 必填 | 城市，如：广州、香港、台北 |
| `address` | ✅ 必填 | 当前/最近一次搬迁后的详细地址（文字描述即可） |
| `open_year` | ✅ 必填 | 原址开业时间，格式：YYYY-MM-DD，如：1993-02-20 |
| `close_year` | ✅ 必填 | 原址结业/搬迁时间，营业中请填：营业中 |
| `status_key` | ✅ 必填 | [状态](#status_key-状态选项)，四选一：`still_open_original` / `moved_same_building` / `moved_far_away` / `building_gone`，如：`still_open_original` |
| `status` | ✅ 必填 | 完整历史描述，一句话说明现状 |
| `photo_url` | ❌ 选填 | 当前门店老照片URL链接，没有可留空 |

### status_key 状态选项

- 🟢 **still_open_original** — 原址营业（仍在原地址经营）
- 🟡 **moved_same_building** — 同楼搬迁（同一大楼内移位）
- 🟠 **moved_far_away** — 商号远迁（迁至附近其他街区）
- 🔴 **building_gone** — 建筑拆除（原址建筑已不存在）

---

### 📍 历史变迁（有序填写，从原址到现状）

请按序号依次填写门店的搬迁历史。每个地址都算一个位置，从 **1（原址）** 开始编号。

如果门店从未搬迁过，只需填 **第 1 项（原址）** 即可。

```
# 第 1 项：原址
location_1_label: 原址
location_1_address: 
location_1_open_year: 
location_1_close_year: 
location_1_coordinates: 
location_1_photo_url: 

# 第 2 项：第一次搬迁（如有）
location_2_label: 
location_2_address: 
location_2_open_year: 
location_2_close_year: 
location_2_coordinates: 
location_2_photo_url: 

# 第 3 项：第二次搬迁（如有，以此类推）
location_3_label: 
location_3_address: 
location_3_open_year: 
location_3_close_year: 
location_3_coordinates: 
location_3_photo_url: 
```

#### 历史变迁字段说明

| 字段 | 是否必填 | 说明 |
|------|----------|------|
| `location_N_label` | ✅ 必填 | 位置标签，如：原址、同楼搬迁、第一次搬迁、现址 |
| `location_N_address` | ✅ 必填 | 该位置的详细地址（文字描述即可） |
| `location_N_open_year` | ❌ 选填 | 该位置的开业时间 |
| `location_N_close_year` | ❌ 选填 | 该位置的结业/搬迁时间，营业中请填：营业中 |
| `location_N_coordinates` | ❌ 选填 | 经纬度坐标 `[经度, 纬度]`，WGS-84 GPS 坐标，如：`[113.2644, 23.1291]` |
| `location_N_photo_url` | ❌ 选填 | 该位置的老照片URL链接 |

---

## 💡 示例（广州第一家麦当劳）

```
name: 广州第一家麦当劳（63层广东国际大厦首层）
region: 中国‑广东省
city: 广州
address: 广州市越秀区环市东路 63 层广东国际大厦二楼
open_year: 1993-02-20
close_year: 2010-03-31
status_key: moved_same_building
status: 大楼尚存；商号搬迁至本大厦二楼；首层现为银行酒馆，无纪念牌匾
photo_url: 

location_1_label: 原址
location_1_address: 广州市越秀区环市东路 63 层广东国际大厦首层
location_1_open_year: 1993-02-20
location_1_close_year: 2010-03-31
location_1_coordinates: [113.2644, 23.1291]
location_1_photo_url: 

location_2_label: 同楼搬迁
location_2_address: 广州市越秀区环市东路 63 层广东国际大厦二楼
location_2_open_year: 2010-04-01
location_2_close_year: 营业中
location_2_coordinates: 
location_2_photo_url: 
```

---

⚠️ **注意**：提交后系统会自动解析并发送邮件通知维护者审核。审核通过后将更新到地图中。