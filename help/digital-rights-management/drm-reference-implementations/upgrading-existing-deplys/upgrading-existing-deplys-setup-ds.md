---
title: 設定網域伺服器
description: 設定網域伺服器
copied-description: true
exl-id: eeb0d39d-58a4-4414-9123-2cf1b27b73de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# 設定網域伺服器{#set-up-a-domain-server}

若要在現有授權伺服器安裝上設定網域伺服器：

1. 在 [!DNL tomcat/lib] 目錄，開啟 [!DNL flashaccess-refimpl.properties] 檔案。
1. 在 `Domain CA certificate` 選項，完成網域CA憑證。

   然後，會使用此憑證來接受網域Token。
1. 在 `Domain CA credential` 選項，填妥 `Domain CA credential certificate (PFX)` 詳細資料。

   然後，此憑證會用於簽署網域憑證和權杖。
1. 指定值 `DomainServerlURL`.

   如果此值設定為 `NULL`，網域驗證可能會成功。 但是，在加入網域時，可能會發生加入網域錯誤。
