---
title: 安全地封裝內容
description: 安全地封裝內容
copied-description: true
exl-id: f554852c-83d9-4b31-8dde-2af577c70989
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 安全地封裝內容 {#securely-packaging-content}

AdobeAccess Media Packager命令列工具的組態檔需要封裝期間使用的PKCS12認證。

在「參考實作命令列」工具中，PKCS12證明資料檔的密碼會以純文字形式儲存在flashaccess.properties檔案中。 因此，在保護裝載此檔案的電腦時，請格外小心，並確保其處於安全的環境中。 (請參閱 [實體安全性與存取](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md))。

封裝程式也會使用License Server和License Server傳輸憑證。 必須保護此資訊的完整性和機密性。 僅授權實體才允許使用封裝程式。 如果您的任何私密金鑰遭到盜用，請立即通知Adobe Systems Incorporated以便撤銷憑證。

>[!NOTE]
>
>此API可讓您針對多個內容片段使用相同的金鑰。 為確保最高安全等級，我們建議僅將此功能用於多位元速率FMS內容。 對於代表不同內容的多個檔案，不建議使用相同的索引鍵。

在某些情況下，Adobe存取封裝API會發出警告。 您必須檢閱這些警告，以判斷您的檔案是否已成功加密。 警告訊息可能會指出原則已過期、無法辨識的標籤或追蹤將不會加密、影片片段將不會加密（且這些片段內的參考可能會變得無效），以及中繼資料將不會加密。

如果使用具有不正確屬性的原則封裝內容，則應更新原則，並且更新的原則必須透過原則更新清單或其他將更新後的原則傳送至伺服器的機制提供給授權伺服器。 某些原則屬性在建立原則後即無法變更。 如果這些屬性不正確，請從發佈網站提取內容、撤銷原則，以便未來無法授予任何授權，並重新加密內容。

封裝完成時，不會明確破壞封裝金鑰，但會進行垃圾收集。 因此，封裝金鑰會在一段時間內保留在記憶體中；您必須防止未經授權存取電腦，並採取措施確保不會公開任何可能洩露此資訊的檔案，例如核心傾印。
