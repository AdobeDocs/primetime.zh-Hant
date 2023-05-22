---
title: 實現匿名域註冊
description: 實現匿名域註冊
copied-description: true
exl-id: 304cfe6f-0917-42ef-a49a-e6c4bc9c10d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 實現匿名域註冊{#implement-anonymous-domain-registration}

1. 建立指定需要域註冊的DRM策略。
1. 將域伺服器URL指定為：

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. 強制進行匿名身份驗證。

   在 [!DNL .properties] 檔案，設定：

   ```
   policy.domain.anonymous=true 
   ```
