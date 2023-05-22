---
description: SEES參考伺服器向您顯示如何使用ExpressPlay啟用設備綁定權利服務。
title: 參考服務設備綁定權利
exl-id: 91f9d406-f3f9-47d3-aa50-f47c4e81b9fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 參考服務：設備綁定權利 {#reference-service-device-binding-entitlement}

SEES參考伺服器向您顯示如何使用ExpressPlay啟用設備綁定權利服務。

>[!NOTE]
>
>設備綁定的權利服務也可以是時間限制的或提供租用期限。

引導 `device_id` 播放虛擬M3U8內容。 然後，您可以在ExpressPlay令牌中嵌入Cookie，生成SPC(包含 `device_id`)，併發送 `getToken` 到ExpressPlay伺服器。

![](assets/fees-device-binding.png)

序列從播放虛擬M3U8開始。 將Cookie發送到SEES伺服器以獲取ExpressPlay令牌URL。 接收到Cookie綁定的ExpressPlay令牌URL後，下一步是生成SPC並將其發送到ExpressPlay伺服器。 ExpressPlay伺服器提取 `device_id` 從SPC中，ExpressPlay標籤URL中的cookie，並將cookie和 `device_id` 中。

客戶端向SEES發送同一cookie發出真實的許可請求。 SEES使用cookie來檢索 `device_id` 從ExpressPlay伺服器獲取。

SEES請求設備綁定和時間綁定的ExpressPlay令牌，並將該令牌返回給客戶端。

客戶端使用ExpressPlay令牌發出許可證請求。

ExpressPlay伺服器將 `device_id` 在SPC中 `device_id` 的下界。 ExpressPlay伺服器僅在兩者 `device_id` 值匹配。
