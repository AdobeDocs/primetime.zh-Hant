---
description: 在某些情況下，您可能想要限制一般使用者在購買或出租內容時，無法在多部裝置上播放內容。 如果客戶使用Expressplay，可使用Expressplay API將使用者的Expressplay權杖繫結到使用者的電腦來完成此操作。
title: 裝置繫結
exl-id: 96ead794-e3eb-4059-91d3-a2c351a17ea3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 裝置繫結{#device-binding}

在某些情況下，您可能想要限制一般使用者在購買或出租內容時，無法在多部裝置上播放內容。 如果客戶使用Expressplay，可使用Expressplay API將使用者的Expressplay權杖繫結到使用者的電腦來完成此操作。

您可以透過下列方式使用API。

1. 產生Cookie。
1. 以查詢字串(Cookie=)形式附加產生的Cookie，以傳送虛擬Token產生請求`<cookie>`)或當作標頭。
1. 讓使用者的電腦使用上述Token （例如，透過播放虛擬內容），將授權請求傳送至Expressplay授權伺服器。

   此虛擬授權要求若成功，會將使用者的device_id （由使用者裝置上的DRM實作計算或產生）與Expressplay後端的Cookie建立關聯。 然後會以下列方式使用此Cookie：

   * 在內容購買/出租時，程式碼會傳送相關Cookie ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * 使用購買內容的金鑰(CEK)、keyID (CEKSID)、原則及其他資訊傳送權杖產生請求，將上述Cookie和device_id分別附加為 `cookie` 關聯引數和 `deviceid` 權杖限制引數。

   * 提供此Token給使用者。

      此程式會為繫結至使用者device_id的內容產生權杖。 當使用者的電腦使用此權杖傳送授權請求時，Expressplay後端會交叉檢查權杖的device_id和授權請求的device_id。

      Expressplay軟體權利檔案伺服器會實作此工作流程。
