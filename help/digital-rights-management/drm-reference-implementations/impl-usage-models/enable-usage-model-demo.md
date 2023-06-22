---
title: 啟用使用模式示範
description: 啟用使用模式示範
copied-description: true
exl-id: 5d546f1a-ebf6-4c93-9a73-fa812cd71086
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---

# 啟用使用模式示範{#enable-the-usage-model-demo}

1. 指定自訂屬性 `RI_UsageModelDemo=true` 封裝時。

   如果您使用「媒體封裝程式」命令列工具封裝內容，請輸入：

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>如果您在封裝時未啟用可選的示範模式，授權伺服器會根據它處理的第一個有效DRM原則發出授權。
