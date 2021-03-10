---
title: HSM首選項
description: HSM首選項
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# HSM首選項{#hsm-preferences}

只有在Packager頁籤中選中&#x200B;**[!UICONTROL Enable HSM]**&#x200B;複選框時，才需要指定此頁籤中的首選項。 下表說明這些偏好設定：

| 偏好設定 | 說明 |
|---|---|
| Sun PKCS#11配置檔案名 | Sun PKCS#11提供程式配置檔案的完整路徑。 有關此配置檔案內容的詳細資訊，請參見Sun網站上的Java PKCS#11參考指南。 |
| 分區密碼 | 在PKCS#11配置檔案中指定的HSM分區的口令。 |
| 許可證伺服器證書別名 | 儲存在HSM上的Adobe許可證伺服器證書的別名。 此證書用於在打包期間加密CEK。 在「封裝器」標籤中指定此選項，而非&#x200B;*授權伺服器憑證*。 |
| 許可證伺服器傳輸證書別名 | 儲存在HSM上的Adobe發出的伺服器傳輸證書的別名。 此憑證用於保護用戶端與授權伺服器之間的通訊安全。 在Packager頁籤中指定此選項，而不是&#x200B;*License Server Transport Certificate*。 |
| Packager憑據別名 | 儲存在HSM上的Adobe發佈的打包器憑證（證書和私鑰）的別名。 這可用來在封裝期間簽署中繼資料。 在「打包器」頁籤中指定此選項，而不是&#x200B;*Packager Credential*。 |
| 許可證伺服器憑據別名 | 儲存在HSM上的Adobe授權伺服器憑證（憑證和私密金鑰）的別名。 此憑據用於簽署策略更新清單。 在「策略更新清單」頁籤中指定此選項，而不是&#x200B;*許可證伺服器憑據*。 （此別名可能與&#x200B;*許可證伺服器證書別名*&#x200B;相同。） |

