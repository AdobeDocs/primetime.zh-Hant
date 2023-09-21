---
title: 建立BEES參考實作
description: 建立BEES參考實作
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 建立BEES參考實作 {#build-the-bees-reference-implementation}

確保您使用Java 1.6.0_24或更新版本。
1. 填寫所需的空白路徑，例如 `tomcatdir` 和 `fasterxmldir` 在 [!DNL build-bees.xml]

   包括FailterXML/Jackson。 您也可以從下載 [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. 更新中的實際jar檔案名稱 [!DNL build.common.xml] 如果您想使用其他版本的Jackson資料庫。
1. 執行 `all` 目標： [!DNL build-bees.xml]：

   ```
   ant -f build-bees.xml
   ```

此 [!DNL bees.war] 將會建立於 [!DNL bees-build/wars] 資料夾。
