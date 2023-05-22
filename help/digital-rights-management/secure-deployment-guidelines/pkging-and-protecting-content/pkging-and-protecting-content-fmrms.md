---
description: Flash媒體Rights Management伺服器1.x和Adobe PrimetimeDRM使用不同的元資料來打包內容和請求許可證。 要使用FMRMS 1.x版內容，必須轉換元資料。
title: 確保與Flash媒體Rights Management伺服器1.x的相容性
exl-id: 737c853f-4e27-47e6-9248-857c7800795a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 確保與Flash媒體Rights Management伺服器1.x的相容性 {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash媒體Rights Management伺服器1.x和Adobe PrimetimeDRM使用不同的元資料來打包內容和請求許可證。 要使用FMRMS 1.x版內容，必須轉換元資料。

黃金時段DRM SDK支援以下元資料轉換選項：

* 離線（推薦）

   在離線過程中生成黃金時段DRM元資料並儲存元資料，直到被客戶端請求。 如果元資料離線生成，則許可證伺服器不需要訪問1.x CEK或打包器憑據。 離線轉換可提供更好的效能，因為許可證伺服器不需要即時生成元資料。
* 按需

   當客戶端請求元資料時生成黃金時段DRM元資料。 當黃金時段DRM客戶端下載版本1.x內容時，客戶端將DRM元資料發送到黃金時段DRM SDK。 SDK將DRM元資料轉換為當前格式，加密並嵌入元資料中的內容加密密鑰(CEK)，並將內容發回到黃金時段DRM客戶端。

   >[!NOTE]
   >
   >黃金時段DRM 1.x元資料不包括CEK。

   要轉換元資料，黃金時段DRM需要訪問黃金時段DRM 1.x內容加密密鑰。 從Flash媒體Rights Management伺服器1.x遷移時，您可以繼續將內容加密密鑰儲存在LiveCycleES資料庫中，或實施自定義解決方案以安全地將內容加密密鑰儲存在另一個位置。 如果您決定將內容加密密鑰儲存在LiveCycleES資料庫中，請遵循中概述的建議 *保護對資料庫中敏感內容的訪問* 在 **ES2LiveCycle®的加固和安全性**。

有關確保與使用Flash媒體Rights Management伺服器1.x打包的內容相容的詳細資訊，請參閱上的Adobe PrimetimeDRM API [Adobe PrimetimeAPI參考](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)。
