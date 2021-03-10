---
title: 建立BEES參考實作
description: 建立BEES參考實作
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# 建立BEES參考實作{#build-the-bees-reference-implementation}

請確定您使用的是Java 1.6.0_24或更新版本。
1. 填寫[!DNL build-bees.xml]中所需的空路徑，例如`tomcatdir`和`fasterxmldir`

   隨附FasterXML/Jackson。 您也可以從[https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core)下載。
1. 如果要使用不同版本的Jackson庫，請更新[!DNL build.common.xml]中的實際jar檔案名。
1. 運行[!DNL build-bees.xml]的`all`目標：

   ```
   ant -f build-bees.xml
   ```

[!DNL bees.war]將建立在[!DNL bees-build/wars]資料夾中。