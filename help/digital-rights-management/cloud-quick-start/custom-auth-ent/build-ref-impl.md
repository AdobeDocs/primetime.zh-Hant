---
seo-title: 建立BEES參考實作
title: 建立BEES參考實作
uuid: c9358188-e626-4f99-a02c-4928b06d6ae2
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# 建立BEES參考實作 {#build-the-bees-reference-implementation}

請確定您使用的是Java 1.6.0_24或更新版本。
1. 填入所需的空路徑，例 `tomcatdir` 如 `fasterxmldir` 和 [!DNL build-bees.xml]

   隨附FasterXML/Jackson。 您也可以從https://jar-download.com/artifacts/com.fasterxml.jackson.core下 [載](https://jar-download.com/artifacts/com.fasterxml.jackson.core)。
1. 如果要使用不同版 [!DNL build.common.xml] 本的Jackson庫，請更新中的實際jar檔案名。
1. 運行以 `all` 下目標 [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

將 [!DNL bees.war] 在資料夾中創 [!DNL bees-build/wars] 建。