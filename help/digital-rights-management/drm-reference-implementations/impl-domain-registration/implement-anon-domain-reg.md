---
seo-title: 實作匿名網域註冊
title: 實作匿名網域註冊
uuid: 330d32fd-8c23-40f9-949b-635e5a9acc86
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# 實作匿名網域註冊{#implement-anonymous-domain-registration}

1. 建立指定需要域註冊的DRM策略。
1. 將網域伺服器URL指定為：

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. 強制進行匿名驗證。

   在[!DNL .properties]檔案中，設定：

   ```
   policy.domain.anonymous=true 
   ```
