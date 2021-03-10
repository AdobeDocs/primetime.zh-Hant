---
title: 安全地封裝內容
description: 安全地封裝內容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# 安全地封裝內容{#securely-packaging-content}

Adobe訪問Media Packager命令行工具的配置檔案需要在打包過程中使用的PKCS12憑據。

在Reference Implementation Command Line工具中，PKCS12憑證檔案的密碼會以明文儲存在flashaccess.properties檔案中。 因此，在保護托管此檔案的電腦時，請格外小心，並確保其位於安全環境中。 （請參閱[物理安全和訪問](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)）。

Packager也使用「授權伺服器」和「授權伺服器傳輸」憑證。 必須保護此資訊的完整性和機密性。 僅允許授權實體使用封裝程式。 如果您的任何私密金鑰遭到破壞，請立即通知Adobe Systems Incorporated，以撤銷憑證。

>[!NOTE]
>
>API可讓您對多個內容使用相同的金鑰。 為確保最高等級的安全性，我們建議此功能僅用於多位元速率的FMS內容。 不建議對表示不同內容的多個檔案使用相同的索引鍵。

Adobe存取封裝API會在特定條件下發出警告。 您必須檢閱這些警告，以判斷您的檔案是否已成功加密。 警告訊息可能會指出原則已過期、無法識別的標籤或追蹤不會加密、影片片段不會加密（且這些片段內的參考可能會變成無效），而中繼資料也不會加密。

如果內容使用具有錯誤屬性的原則封裝，則應更新原則，而且更新的原則必須透過原則更新清單或其他將更新的原則傳送至伺服器的機制提供給授權伺服器。 建立策略後，無法更改某些策略屬性。 如果這些屬性不正確，請從散發網站拉回內容、撤銷原則，以便未來不能授與授權，然後重新加密內容。

包裝完成時，包裝密鑰沒有明確銷毀；但是，它是垃圾收集。 因此，包裝鑰匙在記憶體中確實存在一段時間；您必須防止未授權存取機器，並採取步驟確保您不會公開任何可能揭露此資訊的檔案，例如核心轉儲。
