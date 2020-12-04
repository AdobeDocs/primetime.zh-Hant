---
description: Flash Media Rights Management Server 1.x和Adobe Primetime DRM使用不同的中繼資料來封裝內容並申請授權。 Primetime DRM若要使用FMRMS 1.x版內容，必須轉換中繼資料。
seo-description: Flash Media Rights Management Server 1.x和Adobe Primetime DRM使用不同的中繼資料來封裝內容並申請授權。 Primetime DRM若要使用FMRMS 1.x版內容，必須轉換中繼資料。
seo-title: 確保與Flash Media Rights Management Server 1.x相容
title: 確保與Flash Media Rights Management Server 1.x相容
uuid: dd70941e-9015-4fb0-b265-557b6252e051
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# 確保與Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}相容

Flash Media Rights Management Server 1.x和Adobe Primetime DRM使用不同的中繼資料來封裝內容並申請授權。 Primetime DRM若要使用FMRMS 1.x版內容，必須轉換中繼資料。

Primetime DRM SDK支援下列中繼資料轉換選項：

* 離線（建議）

   在離線處理中產生Primetime DRM中繼資料，並儲存中繼資料，直到用戶端要求為止。 如果中繼資料是離線產生的，授權伺服器就不需要存取1.x CEK或封裝憑證。 離線轉換提供更佳的效能，因為授權伺服器不需要即時產生中繼資料。
* 隨選

   當用戶端請求中繼資料時，產生Primetime DRM中繼資料。 當Primetime DRM客戶端下載1.x版內容時，客戶端將DRM元資料發送到Primetime DRM SDK。 SDK將DRM中繼資料轉換為目前格式，加密內容加密金鑰(CEK)並嵌入在中繼資料中，並將內容傳回Primetime DRM用戶端。

   >[!NOTE]
   >
   >Primetime DRM 1.x中繼資料不包含CEK。

   若要轉換中繼資料，Primetime DRM需要存取Primetime DRM 1.x內容加密金鑰。 從Flash Media Rights Management Server 1.x移轉時，您可以繼續將內容加密金鑰儲存在LiveCycle ES資料庫，或建置自訂解決方案，將內容加密金鑰安全地儲存在其他位置。 如果您決定將內容加密金鑰儲存在LiveCycle ES資料庫中，請遵循&#x200B;***「LiveCycle® ES2**強化與安全性」中「保護對資料庫中敏感內容的存取」中所述的建議。*

如需使用Flash Media Rights Management Server 1.x確保與封裝內容相容的詳細資訊，請參閱[Adobe Primetime API參考資料](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)上的Adobe Primetime DRM API。
