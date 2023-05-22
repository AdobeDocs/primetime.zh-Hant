---
title: 設定域伺服器
description: 設定域伺服器
copied-description: true
exl-id: b2589412-25e4-44c8-be11-8b2cfccbf7bb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 設定域伺服器 {#set-up-a-domain-server}

要在現有許可證伺服器安裝上配置域伺服器，請執行以下任務：

1. 開啟 [!DNL flashaccess-refimpl.properties] 檔案 [!DNL tomcat/lib]。

1. 在 `Domain CA certificate` 選項，填寫域CA證書詳細資訊。 此證書將用於接受域令牌。
1. 在 `Domain CA credential` 的 `Domain CA credential certificate (PFX)` 。 此證書將用於為域證書和令牌簽名。

1. 指定 `DomainServerlURL`。 如果此值為NULL，則域驗證可能會成功。 但是，在加入域時，將出現加入域錯誤。
