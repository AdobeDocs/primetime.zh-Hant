---
title: 設定網域伺服器
description: 設定網域伺服器
copied-description: true
exl-id: b2589412-25e4-44c8-be11-8b2cfccbf7bb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 設定網域伺服器 {#set-up-a-domain-server}

若要在現有授權伺服器安裝上設定網域伺服器，請執行下列工作：

1. 開啟 [!DNL flashaccess-refimpl.properties] 下的檔案 [!DNL tomcat/lib].

1. 在 `Domain CA certificate` 選項，填寫網域CA憑證詳細資料。 此憑證將用於接受網域Token。
1. 在 `Domain CA credential` 選項，填入 `Domain CA credential certificate (PFX)` 詳細資料。 此憑證將用於簽署網域憑證和權杖。

1. 指定值 `DomainServerlURL`. 如果此值為NULL，則網域驗證可能會成功。 但是，加入網域時，會出現加入網域錯誤。
