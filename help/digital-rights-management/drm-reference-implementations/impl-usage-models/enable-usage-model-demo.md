---
title: 啟用使用模式示範
description: 啟用使用模式示範
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
>如果您在封裝時未啟動選用示範模式，則授權伺服器會根據所處理的第一個有效DRM原則發出授權。
