---
title: 先決條件
description: 先決條件
copied-description: true
exl-id: 1b66f7fd-ea2f-4217-b327-910e90ab889d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 先決條件 {#prerequisites}

在打包內容之前，需要黃金時段DRM打包器證書。 必須通過黃金時段DRM證書註冊流程來請求。 只需要打包器證書（無許可證伺服器或傳輸）。 請在「證書請求」電子郵件中指出該請求是要與DRM服務一起使用的證書。

[證書註冊指南](../../digital-rights-management/certificate-enrollment-guide/about-certs.md)

包裝證書分為兩個級別 — 生產和試用。 使用TRIAL證書打包的內容僅供開發使用，在證書過期後不會播放。 所有頒發給TRIAL內容的許可證的硬編碼策略到期日期將與證書到期日期的最大硬編碼策略到期日期相同（如果未在DRM策略中設定）。
