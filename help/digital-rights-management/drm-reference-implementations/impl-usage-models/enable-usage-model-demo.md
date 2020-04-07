---
seo-title: 啟用使用模式示範
title: 啟用使用模式示範
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 6e949c2f88deef88f0d0ac95b18c006da1c89d2f

---


# 啟用使用模式示範{#enable-the-usage-model-demo}

1. 在封裝時指定 `RI_UsageModelDemo=true` 自訂屬性。

   如果您使用Media Packager命令列工具封裝內容，請輸入：

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>如果您未在封裝時啟用選用的示範模式，授權伺服器會根據其處理的第一個有效DRM政策來發行授權。

