---
title: 資料保留原則
description: 資料保留原則
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# 資料保留原則 {#data-retention-policy}

>[!WARNING]
>
>**注意：** 此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。


## 簡介 {#introduction}

Adobe身為資料處理者，必須採取適當措施來協助客戶完成存取、刪除和其他來自個人的請求。 套用適當、安全且即時的刪除政策，是遵守這項法規中非常重要的一個環節。

## 定義 {#definitions}

資料保留原則可決定Adobe儲存客戶資料的時間長度。 並行監視的預設資料保留原則為 **25個月**.

| 資料保留期 | 資料保留期是預設的資料保留期（25個月）。 |
|---|---|
| **資料保留期間** | 資料保留視窗會定義可供檢視及報告完整資料的引數。 資料保留時間長度如下：<br/> *開始日期* =目前日期 — 資料保留期 <br/>*結束日期* =目前日期 |

## 資料彙集 {#data-collection}

*點按資料流資料* 代表客戶在工作階段心率上共用的資料（例如，subjectID、mvpdName和中繼資料）。 所有自訂中繼資料欄位都可在 [標準中繼資料屬性](/help/concurrency-monitoring/standard-metadata-attributes.md).

## 客戶型別 {#customer-types}

### 目前客戶 {#current-customers}

除非客戶購買資料保留延伸，否則並行監視將符合以下客戶資料保留要求：

* *點按資料流資料* 「並行監視」所收集的內容最晚必須刪除 **25個月** 從集合日期起。

### 已終止的客戶 {#terminated-customers}

已終止的客戶是已結束與Adobe的關係且不再使用「並行監控」的客戶。

* *點按資料流資料* 「並行監視」收集的專案必須刪除於 **6個月** 自客戶的合約終止日期起算。

## 資料刪除 {#data-deletion}

Adobe保留在資料保留期間過後刪除資料的權利，且無法復原。 目前客戶的資料應每月滾動刪除。

