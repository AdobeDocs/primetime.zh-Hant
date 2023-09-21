---
description: 在某些情況下，您可能想要限制一般使用者在購買或租借內容時，無法在多部裝置上播放內容。 如果客戶使用Expressplay，可使用Expressplay API將使用者的Expressplay權杖繫結至使用者的電腦來完成此操作。
title: 裝置繫結
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 裝置繫結{#device-binding}

在某些情況下，您可能想要限制一般使用者在購買或租借內容時，無法在多部裝置上播放內容。 如果客戶使用Expressplay，可使用Expressplay API將使用者的Expressplay權杖繫結至使用者的電腦來完成此操作。

您可以透過以下方式使用API。

1. 產生Cookie。
1. 以查詢字串(Cookie=)形式附加產生的Cookie，傳送虛擬Token產生請求`<cookie>`)或當作標頭。
1. 讓使用者的電腦使用上述權杖（例如透過播放虛擬內容），將授權要求傳送至Expressplay授權伺服器。

   此虛擬授權要求若成功，會將使用者的device_id （由使用者裝置上的DRM實作所計算或產生）與Expressplay後端中的Cookie建立關聯。 然後會以下列方式使用此Cookie：

   * 在內容購買/租賃時，程式碼會傳送相關聯的Cookie ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * 使用購買內容的金鑰(CEK)、keyID (CEKSID)、原則及其他資訊傳送權杖產生請求，並將上述Cookie和device_id分別附加為 `cookie` 關聯引數和 `deviceid` 權杖限制引數。

   * 提供此Token給使用者。

     此程式會產生內容的Token，內容會繫結至使用者的device_id。 當使用者的電腦傳送具有此權杖的授權請求時，Expressplay後端會以授權請求的device_id交叉檢查權杖的device_id。

     Expressplay軟體權利檔案伺服器會實作此工作流程。
