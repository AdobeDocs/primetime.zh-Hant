---
title: 自訂驗證/權益概述（選用）
description: 自訂驗證/權益概述（選用）
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 自訂驗證/權益概述（選用）{#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM可設定為您自己的後端驗證/權益服務，以判斷：

* 是否允許此使用者取得授權？
* 授權中應該包含哪些權利/限制？

Primetime Cloud DRM包括後端驗證/權利服務的參考實作。 為了示範，此伺服器正在發出BEES要求的「允許」回應。 另請參閱 [!DNL BEESServlet.java] 修改伺服器行為。

>[!NOTE]
>
>之前，這是一個單獨的產品，稱為 *後端權益伺服器* (BEES)，因此在本檔案及來源檔案中會參照BEES。
