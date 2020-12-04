---
description: 'null'
seo-description: 'null'
seo-title: 設定域伺服器
title: 設定域伺服器
uuid: bf85305e-9a00-4bc0-ba36-c870979456e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 設定域伺服器{#set-up-a-domain-server}

要在現有許可證伺服器安裝上配置域伺服器，請執行以下操作：

1. 在[!DNL tomcat/lib]目錄中，開啟[!DNL flashaccess-refimpl.properties]檔案。
1. 在`Domain CA certificate`選項下，填寫域CA證書。

   然後，此憑證會用於接受網域Token。
1. 在`Domain CA credential`選項下，填寫`Domain CA credential certificate (PFX)`詳細資訊。

   然後，此憑證會用於簽署網域憑證和Token。
1. 指定`DomainServerlURL`的值。

   如果此值設定為`NULL` ，則域驗證可能成功。 但是，在加入網域時，可能會發生加入網域錯誤。
