---
description: Flash MediaRights Management伺服器1.x和Adobe Primetime DRM使用不同的中繼資料來封裝內容和請求授權。 若要讓Primetime DRM使用FMRMS 1.x版內容，必須轉換中繼資料。
title: 確保與Flash MediaRights Management伺服器1.x相容
exl-id: 737c853f-4e27-47e6-9248-857c7800795a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 確保與Flash MediaRights Management伺服器1.x相容 {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash MediaRights Management伺服器1.x和Adobe Primetime DRM使用不同的中繼資料來封裝內容和請求授權。 若要讓Primetime DRM使用FMRMS 1.x版內容，必須轉換中繼資料。

Primetime DRM SDK支援下列中繼資料轉換選項：

* 離線（建議）

   在離線程式中產生Primetime DRM中繼資料，並儲存中繼資料，直到使用者端要求為止。 如果中繼資料是離線產生，授權伺服器就不需要存取1.x CEK或封裝程式認證。 離線轉換可提供較佳的效能，因為授權伺服器不需要即時產生中繼資料。
* 隨選

   當使用者端要求中繼資料時，就會產生Primetime DRM中繼資料。 當Primetime DRM使用者端下載1.x版內容時，使用者端會將DRM中繼資料傳送至Primetime DRM SDK。 SDK會將DRM中繼資料轉換為目前格式、將內容加密金鑰(CEK)加密並嵌入中繼資料，然後將內容傳回Primetime DRM使用者端。

   >[!NOTE]
   >
   >Primetime DRM 1.x中繼資料不包含CEK。

   若要轉換中繼資料，Primetime DRM需要存取Primetime DRM 1.x內容加密金鑰。 當您從Flash MediaRights Management伺服器1.x移轉時，您可以繼續將內容加密金鑰儲存在LiveCycleES資料庫中，或實作自訂解決方案，將內容加密金鑰安全地儲存在其他位置。 如果您決定將內容加密金鑰儲存在LiveCycleES資料庫中，請遵循中概述的建議 *保護對資料庫中敏感內容的存取* 在 **強化LiveCycle®ES2的安全性**.

如需使用Flash MediaRights Management伺服器1.x確保與封裝內容相容的詳細資訊，請參閱上的Adobe Primetime DRM API [Adobe Primetime API參考](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
