---
title: 確保與Flash MediaRights Management伺服器1.x相容
description: 確保與Flash MediaRights Management伺服器1.x相容
copied-description: true
exl-id: 324ea561-c666-4cf9-871b-11f6b6b406f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 確保與Flash MediaRights Management伺服器1.x相容{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash MediaRights Management伺服器1.x和Adobe存取使用不同的中繼資料來封裝內容和請求授權。 若要讓Adobe存取使用FMRMS 1.x版內容，必須轉換中繼資料。

Adobe存取SDK支援兩種轉換中繼資料的選項：

* 離線（建議）

   在離線程式中產生Adobe存取中繼資料，並將其儲存以供使用者端請求時使用。 Adobe建議使用此選項。 如果中繼資料是離線產生，授權伺服器就不需要存取1.x CEK或封裝程式認證。 此外，離線轉換可提供較佳的效能，因為授權伺服器不需要即時產生中繼資料。

* 隨選

   在使用者端要求時隨選產生Adobe存取中繼資料。 當Adobe存取使用者端下載版本1.x內容時，它會將DRM中繼資料（也稱為DRM標頭）傳送到Adobe存取SDK。 SDK會將DRM中繼資料轉換為目前格式。 SDK會將內容加密金鑰(CEK)加密並嵌入中繼資料，然後將內容傳回Adobe存取使用者端。 (Adobe存取1.x中繼資料不包含CEK。)

   若要轉換中繼資料，Adobe存取需要存取Adobe存取1.x內容加密金鑰。 當您從Flash MediaRights Management伺服器1.x移轉時，您可以繼續將內容加密金鑰儲存在LiveCycleES資料庫中，也可以實作自訂解決方案，將內容加密金鑰安全地儲存在其他地方。 如果您選擇繼續將內容加密金鑰儲存在LiveCycleES資料庫中，請遵循以下的「保護對資料庫中敏感內容的存取」中概述的建議： *強化LiveCycleES的安全性*.

如需確保與使用Flash MediaRights Management伺服器1.x封裝的內容相容的詳細資訊，請參閱 *Adobe存取API參考*.
