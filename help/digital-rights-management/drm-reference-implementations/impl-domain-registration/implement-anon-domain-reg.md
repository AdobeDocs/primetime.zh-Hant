---
title: 實作匿名網域註冊
description: 實作匿名網域註冊
copied-description: true
exl-id: 304cfe6f-0917-42ef-a49a-e6c4bc9c10d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 實作匿名網域註冊{#implement-anonymous-domain-registration}

1. 建立DRM原則，指定需要登入網域。
1. 將網域伺服器URL指定為：

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. 將匿名驗證設為必要。

   在您的 [!DNL .properties] 檔案，設定：

   ```
   policy.domain.anonymous=true 
   ```
