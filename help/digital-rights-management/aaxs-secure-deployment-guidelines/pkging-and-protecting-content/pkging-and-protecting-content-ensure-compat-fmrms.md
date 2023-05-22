---
title: 確保與Flash媒體Rights Management伺服器1.x的相容性
description: 確保與Flash媒體Rights Management伺服器1.x的相容性
copied-description: true
exl-id: 324ea561-c666-4cf9-871b-11f6b6b406f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 確保與Flash媒體Rights Management伺服器1.x的相容性{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash媒體Rights Management伺服器1.x和Adobe訪問使用不同的元資料來打包內容和請求許可證。 要使Adobe訪問使用FMRMS 1.x版內容，必須轉換元資料。

Adobe訪問SDK支援兩種轉換元資料的選項：

* 離線（推薦）

   在離線進程中生成Adobe訪問元資料，並將其儲存，以便在客戶端請求時使用。 Adobe建議使用此選項。 如果元資料離線生成，則許可證伺服器不需要訪問1.x CEK或打包器憑據。 此外，離線轉換可提供更好的效能，因為許可證伺服器不需要即時生成元資料。

* 按需

   當客戶端請求Adobe訪問元資料時，按需生成該元資料。 當Adobe訪問客戶端下載1.x版內容時，它將DRM元資料（也稱為DRM頭）發送到Adobe訪問SDK。 SDK將DRM元資料轉換為當前格式。 SDK將內容加密密鑰(CEK)加密並嵌入元資料中，並將內容發回Adobe訪問客戶端。 (AdobeAccess 1.x元資料不包含CEK。)

   要轉換元資料，Adobe訪問需要訪問Adobe訪問1.x內容加密密鑰。 從Flash媒體Rights Management伺服器1.x遷移時，您可以繼續將內容加密密鑰儲存在LiveCycleES資料庫中，也可以實施自定義解決方案以安全地將內容加密密鑰儲存在其他位置。 如果您選擇繼續將內容加密密鑰儲存在LiveCycleES資料庫中，請遵循中「保護對資料庫中敏感內容的訪問」中概述的建議 *LiveCycleES的強化與安全*。

有關確保與使用Flash媒體Rights Management伺服器1.x打包的內容相容的詳細資訊，請參見 *Adobe訪問API參考*。
