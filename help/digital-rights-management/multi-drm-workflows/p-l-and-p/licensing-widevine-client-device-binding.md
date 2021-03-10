---
description: 在某些情況下，您可能會想要限制使用者在購買或租用內容時，在多種裝置上播放內容。 如果客戶使用Expressplay，則可使用Expressplay API將使用者的Expressplay Token系結至使用者的機器。
title: 裝置系結
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# 設備綁定{#device-binding}

在某些情況下，您可能會想要限制使用者在購買或租用內容時，在多種裝置上播放內容。 如果客戶使用Expressplay，則可使用Expressplay API將使用者的Expressplay Token系結至使用者的機器。

您可透過下列方式使用API。

1. 產生Cookie。
1. 傳送虛擬代號產生請求，並將產生的Cookie附加為查詢字串(cookie=`<cookie>`)或標題。
1. 讓使用者的機器使用上述Token，例如播放虛擬內容，傳送授權要求給Expressplay授權伺服器。

   此虛擬授權請求若成功，會將使用者的device_id（由使用者裝置上的DRM實作所計算或產生）與Expressplay後端的Cookie建立關聯。 然後，會以下列方式使用此Cookie:

   * 在內容購買／租用時，程式碼會傳送相關的Cookie([https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))，以查詢Expressplay後端的使用者device_id
   * 傳送包含購買內容的金鑰(CEK)、金鑰ID(CEKSID)、原則和其他資訊的代號產生要求，分別附加上述Cookie和device_id作為`cookie`關聯參數和`deviceid`代號限制參數。

   * 提供此Token給使用者。

      此程式會為系結至使用者device_id的內容產生Token。 當使用者的機器傳送含有此Token的授權要求時，Expressplay後端會以授權要求的device_id來交叉檢查Token的device_id。

      範例Expressplay權益伺服器會實作此工作流程。
