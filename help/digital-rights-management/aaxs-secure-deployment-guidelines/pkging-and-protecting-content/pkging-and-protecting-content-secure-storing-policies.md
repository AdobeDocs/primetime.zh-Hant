---
title: 安全地儲存策略
description: 安全地儲存策略
copied-description: true
exl-id: fd335a0c-7eb1-4159-958f-7302fce98cef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 安全地儲存策略{#securely-storing-policies}

AdobeAccess SDK在開發用於內容打包和策略建立的應用程式方面提供了極大的靈活性。 在建立此類應用程式時，您可能希望允許某些用戶建立和修改策略，並限制其他用戶，以便他們只能將現有策略應用於內容。 如果是這種情況，您必須實施必要的訪問控制，以建立具有不同權限的用戶帳戶，以便建立策略以及將策略應用到內容。

在打包中使用策略之前，不會對其進行簽名或以其他方式保護其不受修改。 如果您擔心打包工具的用戶修改策略，則應考慮對策略進行簽名，以確保不能修改這些策略。

有關使用SDK建立應用程式的詳細資訊，請參見 *Adobe訪問API參考*。
