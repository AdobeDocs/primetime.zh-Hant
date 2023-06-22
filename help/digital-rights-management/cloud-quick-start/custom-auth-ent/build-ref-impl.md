---
title: 建立BEES參考實作
description: 建立BEES參考實作
copied-description: true
exl-id: 330c14de-fe4e-4cc8-b0a5-8f7c74417adf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 建立BEES參考實作 {#build-the-bees-reference-implementation}

確保您使用的是Java 1.6.0_24或更新版本。
1. 填入所需的空白路徑，例如 `tomcatdir` 和 `fasterxmldir` 在 [!DNL build-bees.xml]

   包括FailterXML/Jackson。 您也可以從下載 [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. 更新中的實際jar檔案名稱 [!DNL build.common.xml] 如果您想使用不同版本的Jackson程式庫。
1. 執行 `all` 目標： [!DNL build-bees.xml]：

   ```
   ant -f build-bees.xml
   ```

此 [!DNL bees.war] 將在以下位置建立： [!DNL bees-build/wars] 資料夾。
