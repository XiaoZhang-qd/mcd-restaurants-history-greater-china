---
name: 老店投稿
about: 提交一家大中华区麦当劳旧址信息
title: "🏪 投稿：[城市] [门店名称]"
labels: ["新门店投稿"]
assignees: ""
---

## 📋 请按以下格式填写

> 字段说明、状态选项、示例请参阅 [README.md](https://github.com/xiaozhang-qd/mcd-restaurants-history-greater-china#数据格式)

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
photo_urls: 
```

> 💡 多张照片请每行填一个 URL，或用英文逗号分隔

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
location_1_photo_urls: 

# 第 2 项：第一次搬迁（如有）
location_2_label: 
location_2_address: 
location_2_open_year: 
location_2_close_year: 
location_2_coordinates: 
location_2_photo_urls: 

# 第 3 项：第二次搬迁（如有，以此类推）
location_3_label: 
location_3_address: 
location_3_open_year: 
location_3_close_year: 
location_3_coordinates: 
location_3_photo_urls: 
```

> 💡 多张照片请每行填一个 URL，或用英文逗号分隔
