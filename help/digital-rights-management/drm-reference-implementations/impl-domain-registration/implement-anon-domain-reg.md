---
title: 實作匿名網域註冊
description: 實作匿名網域註冊
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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
