---
title: 更新授權伺服器WAR檔案
description: 更新授權伺服器WAR檔案
copied-description: true
exl-id: a70d04e2-24a4-4848-9e9b-97467f2c1749
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 更新授權伺服器WAR檔案{#update-the-license-server-war-file}

為了支援透過On Premises Individualization Server進行個人化的使用者端，您必須更新License Server的信任憑證根目錄，以包含新取得的個人化CA認證。 Python指令碼( [!DNL addIndivCert.py])包含在 [!DNL update_license_server] 資料夾。

請執行以下動作以更新授權伺服器：

1. 複製要更新的WAR檔案(範例： [!DNL flashaccess.war]， [!DNL faxsks.war])。
1. 請確定WAR檔案已解除鎖定，並已設定其許可權以便修改。
1. 執行 [!DNL addIndivCert.py] 用於更新License Server WAR檔案的Python指令碼。

   指令碼的輸入如下：

   * `cert`：包含個人化CA憑證的PKCS12檔案
   * `war`：要更新的WAR檔案

   輸出檔案是更新的WAR檔案。

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

將會就地修改WAR檔案。 如有需要，您可以編輯Python指令碼以符合您的特定需求。 執行更新後，您可以正常部署WAR檔案。
