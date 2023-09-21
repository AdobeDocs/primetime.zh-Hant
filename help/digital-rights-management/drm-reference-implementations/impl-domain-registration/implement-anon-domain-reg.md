---
title: 實作匿名網域註冊
description: 實作匿名網域註冊
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 實作匿名網域註冊{#implement-anonymous-domain-registration}

1. 建立DRM原則，指定需要登入網域。
1. 指定網域伺服器URL為：

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. 將匿名驗證設為必要。

   在您的 [!DNL .properties] 檔案，設定：

   ```
   policy.domain.anonymous=true 
   ```
