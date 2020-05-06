---
title: PTAI 20.5.1發行說明
description: PTAI 20.5.1發行說明說明Primetime動態廣告插入在2020年的新增或變更、已解決及已知問題。
translation-type: tm+mt
source-git-commit: 266b884707e9160d539a06fd089732ef8ade21ba
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Primetime動態廣告插入20.5.1發行說明

動態廣告插入20.5.1發行說明說明Primetime動態廣告插入2020年的新增或變更、已解決的問題和已知問題。

## PTAI 20.5.1的新增功能

**時間：** 2020年5月5日星期二東部時間凌晨4時至5時

* 修正在傳送If-Modified-Since標題時，確保提供正確的CORS標題的問題。

* CRS儀表板上的錯誤修正。

* 維護更新。

## 舊版中的變更

### 20.3.4版

**時間：** 2020年4月1日星期三東部時間凌晨3點至4點

* 修正在VOD/WebVTT中插入廣告後，字幕不同步的問題。

* 安全性更新。

### 20.3.3版

**時間：** 2020年3月26日星期四東部時間凌晨3點至4點

* SSAI 4XX和5XX回應現在可正確提供CORS相關標題，讓跨網域javascript/網頁檢視用戶端可成功讀取錯誤回應。

* 修正X-Forwarded-For標題的問題，當IPv6位址傳遞至廣告伺服器時，URL編碼不正確。

* 修正CMAF/去muxed音訊串流的問題，在某些情況下，EXT-X-MEDIA-SEQUENCE編號會錯誤增加。

### 20.1.3版

**時間：** 2020年1月28日，星期二，東部時間凌晨2:00至3:00

* **VMAP搭配FER支援nbc CueFormat**

   將FER串流的提示轉換為FW時間軸覆寫參數(當使 `ptcueformat=nbc` 用時)，且該串流是VOD串流，包含資訊清單內提示和內建廣告。

* 在轉送至協力廠商廣告提供者/CDN之前，先淨化HTTP標題中的使用者代理欄位。

* 在傳送至Auditude和其他廣告供應商CDN之前，先從使用者代理HTTP標題中篩除控制／不可列印的字元（ASCII程式碼&lt; 32）。 用於失敗此類無效標題的Auditude廣告呼叫。

* 從NetStorage Groups清除舊的V1對象，使對象計數保持在Akamai的安全限制內。

## 已解決問題

如果解決方法與報告的問題相關聯，則顯示Zendesk參考。 例如，ZD#xxxxx。

**PTAI 20.3.3**

* X-Forwarded-For標題的問題，當IPv6位址傳遞至廣告伺服器時，URL編碼不正確。

* CMAF/去muxed音訊串流的問題，在某些情況下，EXT-X-MEDIA-SEQUENCE數字在某些情況下會不正確地增加

## 已知問題和限制

**PTAI 20.3.3**

沒有新的限制。
