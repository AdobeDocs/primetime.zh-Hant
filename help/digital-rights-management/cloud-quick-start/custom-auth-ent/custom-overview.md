---
title: 自訂驗證/權益概觀（選擇性）
description: 自訂驗證/權益概觀（選擇性）
copied-description: true
exl-id: d92c4246-c772-44da-80b6-4086dfc30ff4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 自訂驗證/權益概觀（選擇性）{#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM可設定為您自己的後端驗證/權益服務來確定：

* 是否允許此使用者取得授權？
* 授權中應有哪些權利/限制？

Primetime Cloud DRM包含後端驗證/權利服務的參考實作。 為了示範，此伺服器正在發出BEES要求的「允許」回應。 另請參閱 [!DNL BEESServlet.java] 修改伺服器行為。

>[!NOTE]
>
>之前，這是一個單獨產品，稱為 *後端權益伺服器* (BEES)，因此在本檔案及來源檔案中會參照BEES。
