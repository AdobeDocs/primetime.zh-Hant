---
title: 更新License Server WAR檔案
description: 更新License Server WAR檔案
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# 更新許可證伺服器WAR檔案{#update-the-license-server-war-file}

為了支援透過內部個人化伺服器進行個人化的客戶，您必須更新授權伺服器的信任憑證根目錄，以包含新取得的個人化CA憑證。 [!DNL update_license_server]資料夾中包含Python指令碼([!DNL addIndivCert.py])。

執行下列動作以更新授權伺服器：

1. 製作要更新的WAR檔案副本(示例：[!DNL flashaccess.war], [!DNL faxsks.war])。
1. 請確定WAR檔案已解除鎖定，並且已設定其權限，以便修改它們。
1. 運行[!DNL addIndivCert.py] Python指令碼以更新License Server WAR檔案。

   指令碼的輸入如下：

   * `cert`:包含個性化CA證書的PKCS12檔案
   * `war`:要更新的WAR檔案

   輸出檔案是更新的WAR檔案。

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

WAR檔案將就地修改。 如有必要，您可以編輯Python指令碼以滿足您的特定需求。 執行更新後，可以正常部署WAR檔案。
