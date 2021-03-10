---
title: 啟用使用模式示範
description: 啟用使用模式示範
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# 啟用使用模式示範{#enable-the-usage-model-demo}

1. 在封裝時指定自訂屬性`RI_UsageModelDemo=true`。

   如果您使用Media Packager命令列工具封裝內容，請輸入：

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>如果您未在封裝時啟用選用的示範模式，授權伺服器會根據其處理的第一個有效DRM政策來發行授權。

