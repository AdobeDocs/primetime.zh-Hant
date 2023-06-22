---
title: HSM喜好設定
description: HSM喜好設定
copied-description: true
exl-id: 323f839b-fbd8-492c-a210-7651e92c7513
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# HSM喜好設定 {#hsm-preferences}

只有在 **[!UICONTROL Enable HSM]** 核取方塊會選取在「封裝程式」標籤中。 下表說明這些偏好設定：

| 偏好設定 | 說明 |
|---|---|
| Sun PKCS#11設定檔名稱 | Sun PKCS#11提供者組態檔的完整路徑。 請參閱Sun網站上的Java PKCS#11 Reference Guide，以取得此設定檔內容的詳細資訊。 |
| 分割區密碼 | PKCS#11組態檔中指定的HSM磁碟分割密碼。 |
| 授權伺服器憑證別名 | 儲存在HSM上的Adobe核發的授權伺服器憑證別名。 此憑證用於在封裝期間加密CEK。 指定此專案，而非 *授權伺服器憑證* 在「封裝程式」標籤中。 |
| 授權伺服器傳輸憑證別名 | 儲存在HSM上的Adobe核發的伺服器傳輸憑證別名。 此憑證用於保護使用者端與授權伺服器之間的通訊。 指定此專案，而非 *授權伺服器傳輸憑證* 在「封裝程式」標籤中。 |
| 封裝程式認證別名 | 儲存在HSM上的Adobe核發的封裝者認證（憑證和私密金鑰）的別名。 這用於在封裝期間簽署中繼資料。 指定此專案，而非 *封裝程式認證* 在「封裝程式」標籤中。 |
| 授權伺服器認證別名 | 儲存在HSM上的Adobe核發的授權伺服器認證（憑證和私密金鑰）的別名。 此認證用於簽署原則更新清單。 指定此專案，而非 *授權伺服器認證* 在[Policy Update List]標籤中。 (此別名可能與 *授權伺服器憑證別名*.) |
