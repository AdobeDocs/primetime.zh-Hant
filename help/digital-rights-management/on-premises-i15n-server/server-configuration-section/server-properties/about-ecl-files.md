---
title: 關於ECI檔案
description: 關於ECI檔案
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 關於ECI檔案{#about-eci-files}

除了CRL之外，您還需要定期更新內嵌式公用介面(ECI)檔案。 每當Adobe新增對新Primetime DRM使用者端平台(例如：iOS、Android、Windows FlashPlayer等)的支援時，就會建立新的ECI記錄。 為了支援此使用者端的個人化，個人化伺服器上必須有相對應的ECI記錄。

由於新的Primetime DRM使用者端發行頻率不高，Adobe會視需要發行更新的ECI資料。 Adobe會定期收集ECI檔案，並將它們託管到下列位置以供分發：

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

此 [!DNL Latest.txt] 檔案會包含最近CRL散發檔案的URL。

Adobe將以下述方式建立ECI zip檔案：

資料夾結構：

```
ECI\*
```

資料夾的內容將會遞回壓縮：

```
zip -R ECI ECI.zip
```

系統會計算zip檔案的OpenSSL SHA--256摘要：

```
openssl dgst -sha256 -hex ECI.zip
```

zip檔案將會重新命名以包含封存日期及SHA-256摘要：

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

例如：

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

您應該定期檢查上述位置是否有更新的ECI檔案。

請執行以下程式以便在下載後安裝：

1. 記下SHA-256摘要，並使用OpenSSL或同等工具重新計算。
1. 將其與檔案名稱中指定的檔案進行比較。
1. 將檔案重新命名為 [!DNL ECI.zip].
1. 解壓縮 [!DNL ECI] 目錄。
1. 用新的ECI目錄取代舊的ECI目錄。
1. 重新啟動個人化伺服器。
