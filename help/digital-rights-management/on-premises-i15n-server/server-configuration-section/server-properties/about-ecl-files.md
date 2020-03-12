---
seo-title: 關於ECI檔案
title: 關於ECI檔案
uuid: 124d8ab1-933b-4a1b-992a-919f3d799460
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# 關於ECI檔案{#about-eci-files}

除了CRL之外，您還需要定期更新嵌入式公共介面(ECI)檔案。 每當Adobe新增對新Primetime DRM用戶端平台的支援時(例如：iOS、Android、Windows FlashPlayer等)，就會建立新的ECI記錄。 為了支援該客戶機的個性化，需要在個性化伺服器上顯示相應的ECI記錄。

由於Primetime DRM新用戶端的發行不常頻繁，Adobe將視需要發佈更新的ECI資料。 Adobe會定期收集ECI檔案，並將其裝載至下列位置進行散發：

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

文 [!DNL Latest.txt] 件將包含最新CRL分發檔案的URL。

Adobe會依照下列方式建立ECI zip檔案：

資料夾結構：

```
ECI\*
```

資料夾的內容將以遞歸方式壓縮：

```
zip -R ECI ECI.zip
```

OpenSSL SHA-256摘要將會計算zip檔案：

```
openssl dgst -sha256 -hex ECI.zip
```

zip檔案將重新命名為包含封存日期以及SHA-256摘要：

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

例如：

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

您應定期檢查上述位置，以取得更新的ECI檔案。

下載後，請執行下列安裝程式：

1. 請注意SHA-256摘要，然後使用OpenSSL或相當的工具重新計算它。
1. 將它與檔案名稱中指定的比較。
1. 將檔案更名為 [!DNL ECI.zip]。
1. 解壓縮目 [!DNL ECI] 錄。
1. 將舊的ECI目錄更換為新目錄。
1. 重新啟動個性化伺服器。

