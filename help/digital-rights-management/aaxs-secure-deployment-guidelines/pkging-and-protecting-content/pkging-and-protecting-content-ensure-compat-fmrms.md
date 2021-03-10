---
title: 確保與Flash媒體Rights Management伺服器1.x相容
description: 確保與Flash媒體Rights Management伺服器1.x相容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# 確保與Flash介質Rights Management伺服器1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}相容

Flash媒體Rights Management伺服器1.x和Adobe存取使用不同的中繼資料來封裝內容並請求授權。 若要「Adobe存取」使用FMRMS 1.x版內容，必須轉換中繼資料。

Adobe存取SDK支援兩種轉換中繼資料的選項：

* 離線（建議）

   在離線程式中產生Adobe存取中繼資料，並儲存以供用戶端要求時使用。 Adobe建議使用此選項。 如果中繼資料是離線產生的，授權伺服器就不需要存取1.x CEK或封裝憑證。 此外，離線轉換提供更佳的效能，因為授權伺服器不需要即時產生中繼資料。

* 隨選

   當用戶端要求時，隨選產生Adobe存取中繼資料。 當Adobe存取用戶端下載1.x版內容時，會將DRM中繼資料（也稱為DRM標題）傳送至Adobe存取SDK。 SDK會將DRM中繼資料轉換為目前格式。 SDK會加密內容加密金鑰(CEK)並嵌入在中繼資料中，並將內容傳回給Adobe存取用戶端。 (Adobe存取1.x中繼資料不包含CEK)。

   若要轉換中繼資料，「Adobe存取」需要存取「Adobe存取1.x」內容加密金鑰。 從Flash媒體Rights Management伺服器1.x遷移時，您可以繼續將內容加密密鑰儲存在LiveCycleES資料庫中，也可以實施自定義解決方案以安全地將內容加密密鑰儲存在其他位置。 如果您選擇繼續將內容加密密鑰儲存在LiveCycleES資料庫中，請遵循&#x200B;*LiveCycleES*&#x200B;中「保護對資料庫中敏感內容的訪問」中的建議。

有關確保與使用Flash媒體Rights Management伺服器1.x打包的內容相容的詳細資訊，請參閱&#x200B;*Adobe訪問API參考*。
