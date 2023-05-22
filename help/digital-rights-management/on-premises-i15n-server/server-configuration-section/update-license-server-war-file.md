---
title: 更新許可證伺服器WAR檔案
description: 更新許可證伺服器WAR檔案
copied-description: true
exl-id: a70d04e2-24a4-4848-9e9b-97467f2c1749
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 更新許可證伺服器WAR檔案{#update-the-license-server-war-file}

為了支援通過本地個性化伺服器具有個性化的客戶端，必須更新許可證伺服器的信任證書根以包括新獲得的個性化CA憑據。 Python指令碼( [!DNL addIndivCert.py]) [!DNL update_license_server] 的子菜單。

執行以下操作以更新許可證伺服器：

1. 製作要更新的WAR檔案的副本(示例： [!DNL flashaccess.war]。 [!DNL faxsks.war])。
1. 確保WAR檔案已解鎖並設定了權限，以便可以修改它們。
1. 運行 [!DNL addIndivCert.py] 用於更新許可證伺服器WAR檔案的Python指令碼。

   指令碼的輸入如下：

   * `cert`:包含個性化CA證書的PKCS12檔案
   * `war`:要更新的WAR檔案

   輸出檔案是更新的WAR檔案。

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

WAR檔案將被修改到位。 如有必要，您可以編輯Python指令碼以滿足您的特定需要。 執行更新後，可以正常部署WAR檔案。
