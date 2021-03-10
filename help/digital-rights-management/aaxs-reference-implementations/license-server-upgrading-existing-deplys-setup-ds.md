---
title: 設定域伺服器
description: 設定域伺服器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 設定域伺服器{#set-up-a-domain-server}

要在現有許可證伺服器安裝上配置域伺服器，請執行以下任務：

1. 開啟[!DNL tomcat/lib]下的[!DNL flashaccess-refimpl.properties]檔案。

1. 在`Domain CA certificate`選項下，填寫域CA證書詳細資訊。 此憑證將用於接受網域Token。
1. 在`Domain CA credential`選項下，填寫`Domain CA credential certificate (PFX)`詳細資訊。 此憑證將用於簽署網域憑證和Token。

1. 指定`DomainServerlURL`的值。 如果此值為NULL，則域驗證可能成功。 但是，在加入網域時，會發生連接網域錯誤。

