---
description: 本指南提供有關如何使用瀏覽器TVSDK開發視頻播放器應用程式的資訊。
title: 產品概述和受眾
exl-id: e2bbec5e-d1ce-430c-986c-ba3152190b1c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 產品概述和受眾{#product-overview-and-audience}

本指南提供有關如何使用瀏覽器TVSDK開發視頻播放器應用程式的資訊。

## 產品概述 {#section_1C66E736CEFD4246B7C7C99AADD48118}

Adobe Primetime軟體開發工具包(Browser TVSDK)是一個工具包，允許您向基於瀏覽器的視頻播放器應用程式添加高級視頻播放功能、內容保護和廣告。 瀏覽器TVSDK提供JavaScript API來構建基於瀏覽器的視頻應用程式，並包括以下模式的回放支援：

* 僅HTML5
* HTML5，帶自動快閃記憶體回退
* Flash始終

此版本包括瀏覽器TVSDK API和示例引用實現。

### UI框架

為幫助加快基於JavaScript的瀏覽器視頻播放器應用程式的UI開發，瀏覽器TVSDK包括由API組成的UI框架，用於：

* 包括預設UI控制項，如播放/暫停、音量等
* 無需直接操作DOM結構即可輕鬆添加（或刪除）高級回放UI控制項
* 輕鬆配置關聯UI控制項的行為
* 建立自定義UI控制項
* 根據要求對播放器UI進行外觀

有關UI框架的API的詳細資訊，請參見 [瀏覽器TVSDK 2.4的UI框架](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html)。

## 觀眾 {#section_DFC9DECC2E30426DBBDDEA4E288E666C}

本指南假定您瞭解如何使用JavaScript開發應用程式和視頻播放器。 您可以實現視頻播放器並合併瀏覽器TVSDK功能。
