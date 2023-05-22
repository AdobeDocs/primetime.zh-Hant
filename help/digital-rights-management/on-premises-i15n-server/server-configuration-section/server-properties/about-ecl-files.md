---
title: 關於ECI檔案
description: 關於ECI檔案
copied-description: true
exl-id: ac452897-3c64-4481-a3b7-4b69ef6edb61
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 關於ECI檔案{#about-eci-files}

除了CRL之外，您還需要定期更新嵌入式公共介面(ECI)檔案。 每當Adobe添加對新Mogfire DRM客戶端平台的支援時(例如：iOS、Android、Windows FlashPlayer等)，建立新的ECI記錄。 為了支援該客戶機的個性化，需要在個性化伺服器上存在相應的ECI記錄。

由於新的黃金時段DRM客戶端的發佈並不頻繁，Adobe將根據需要發佈更新的ECI資料。 Adobe將定期收集ECI檔案，並將其寄存到以下位置進行分發：

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

的 [!DNL Latest.txt] 檔案將包含最新CRL分發檔案的URL。

Adobe將按以下方式建立ECI zip檔案：

資料夾結構：

```
ECI\*
```

資料夾的內容將以遞歸方式壓縮：

```
zip -R ECI ECI.zip
```

將計算zip檔案的OpenSSL SHA-256摘要：

```
openssl dgst -sha256 -hex ECI.zip
```

將更名zip檔案，以包含存檔日期和SHA-256摘要：

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

例如：

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

您應定期檢查上面的位置以獲取更新的ECI檔案。

下載後，請執行以下安裝過程：

1. 請注意SHA-256摘要，然後使用OpenSSL或等效工具重新計算它。
1. 將其與檔案名中指定的進行比較。
1. 將檔案更名為 [!DNL ECI.zip]。
1. 解壓縮 [!DNL ECI] 的子菜單。
1. 將舊ECI目錄替換為新目錄。
1. 重新啟動個性化伺服器。
