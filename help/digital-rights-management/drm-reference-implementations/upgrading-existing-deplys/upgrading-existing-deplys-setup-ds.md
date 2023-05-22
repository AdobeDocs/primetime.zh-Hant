---
title: 設定域伺服器
description: 設定域伺服器
copied-description: true
exl-id: eeb0d39d-58a4-4414-9123-2cf1b27b73de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# 設定域伺服器{#set-up-a-domain-server}

要在現有許可證伺服器安裝上配置域伺服器：

1. 在 [!DNL tomcat/lib] 目錄，開啟 [!DNL flashaccess-refimpl.properties] 的子菜單。
1. 在 `Domain CA certificate` 選項，填寫域CA證書。

   然後，此證書用於接受域令牌。
1. 在 `Domain CA credential` 選項，完成 `Domain CA credential certificate (PFX)` 。

   然後，此證書將用於對域證書和令牌進行簽名。
1. 指定 `DomainServerlURL`。

   如果此值設定為 `NULL`，域身份驗證可能成功。 但是，在加入域時，可能會發生加入域錯誤。
