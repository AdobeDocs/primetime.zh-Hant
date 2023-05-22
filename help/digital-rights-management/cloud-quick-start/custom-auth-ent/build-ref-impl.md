---
title: 構建BEES參考實現
description: 構建BEES參考實現
copied-description: true
exl-id: 330c14de-fe4e-4cc8-b0a5-8f7c74417adf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 構建BEES參考實現 {#build-the-bees-reference-implementation}

確保使用的是Java 1.6.0_24或更高版本。
1. 填充所需的空路徑，如 `tomcatdir` 和 `fasterxmldir` 在 [!DNL build-bees.xml]

   包括FasterXML/Jackson。 您也可以從 [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core)。
1. 更新中的實際jar檔案名 [!DNL build.common.xml] 如果你想使用Jackson圖書館的其他版本。
1. 運行 `all` 目標 [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

的 [!DNL bees.war] 將在 [!DNL bees-build/wars] 的子菜單。
