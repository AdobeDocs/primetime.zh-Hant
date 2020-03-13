---
seo-title: 啟用使用模式示範
title: 啟用使用模式示範
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 啟用使用模式示範{#enable-the-usage-model-demo}

1. 在封裝時指定 `RI_UsageModelDemo=true` 自訂屬性。

   如果您使用Media Packager命令列工具封裝內容，請輸入：

   ```
   java -jar AdobeMediaPackager.jar [
   
<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true

```
>[!NOTE] {class="- topic/note "}
>
>If you do not activate the optional demo mode at packaging time, the license server issues a license based on the first valid DRM policy it processes.

