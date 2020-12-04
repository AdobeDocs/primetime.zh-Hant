---
seo-title: 確保與Flash Media Rights Management Server 1.x相容
title: 確保與Flash Media Rights Management Server 1.x相容
uuid: 0160ca02-ebe6-4090-bf32-1d1a46088844
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# 確保與Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}相容

Flash Media Rights Management Server 1.x和Adobe Access會使用不同的中繼資料來封裝內容並申請授權。 Adobe Access若要使用FMRMS 1.x版內容，必須轉換中繼資料。

Adobe Access SDK支援兩種轉換中繼資料的選項：

* 離線（建議）

   在離線程式中產生Adobe Access中繼資料，並儲存以供用戶端要求時使用。 Adobe建議使用此選項。 如果中繼資料是離線產生的，授權伺服器就不需要存取1.x CEK或封裝憑證。 此外，離線轉換提供更佳的效能，因為授權伺服器不需要即時產生中繼資料。

* 隨選

   當用戶端要求時，隨選產生Adobe Access中繼資料。 當Adobe Access用戶端下載1.x版內容時，會將DRM中繼資料（也稱為DRM標題）傳送至Adobe Access SDK。 SDK會將DRM中繼資料轉換為目前格式。 SDK會加密內容加密金鑰(CEK)並嵌入在中繼資料中，並將內容傳回至Adobe Access用戶端。 （Adobe Access 1.x中繼資料不包含CEK。）

   若要轉換中繼資料，Adobe Access需要存取Adobe Access 1.x內容加密金鑰。 從Flash Media Rights Management Server 1.x移轉時，您可以繼續將內容加密金鑰儲存在LiveCycle ES資料庫中，或建置自訂解決方案，將內容加密金鑰安全地儲存在其他地方。 如果您選擇繼續將內容加密金鑰儲存在LiveCycle ES資料庫中，請遵循&#x200B;*Hardening and Security for LiveCycle ES*&#x200B;中「保護對資料庫中敏感內容的存取」中的建議。

如需確保與使用Flash Media Rights Management Server 1.x封裝內容相容的詳細資訊，請參閱&#x200B;*Adobe Access API Reference*。
