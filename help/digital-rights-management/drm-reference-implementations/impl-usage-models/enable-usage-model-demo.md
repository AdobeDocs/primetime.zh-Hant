---
title: 啟用使用模型演示
description: 啟用使用模型演示
copied-description: true
exl-id: 5d546f1a-ebf6-4c93-9a73-fa812cd71086
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---

# 啟用使用模型演示{#enable-the-usage-model-demo}

1. 指定自定義屬性 `RI_UsageModelDemo=true` 打包時。

   如果使用Media Packager命令行工具打包內容，請輸入：

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>如果您在打包時未激活可選演示模式，則許可證伺服器會根據其處理的第一個有效DRM策略發放許可證。
