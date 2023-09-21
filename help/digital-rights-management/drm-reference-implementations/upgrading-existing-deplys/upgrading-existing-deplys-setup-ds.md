---
title: 設定網域伺服器
description: 設定網域伺服器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# 設定網域伺服器{#set-up-a-domain-server}

若要在現有授權伺服器安裝上設定網域伺服器：

1. 在 [!DNL tomcat/lib] 目錄，開啟 [!DNL flashaccess-refimpl.properties] 檔案。
1. 在 `Domain CA certificate` 選項，完成網域CA憑證。

   然後，會使用此憑證來接受網域權杖。
1. 在 `Domain CA credential` 選項，填妥 `Domain CA credential certificate (PFX)` 詳細資料。

   然後，此憑證會用於簽署網域憑證和權杖。
1. 指定值 `DomainServerlURL`.

   如果此值設定為 `NULL`，網域驗證可能會成功。 但是，在加入網域時，可能會發生加入網域錯誤。
