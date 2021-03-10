---
title: 安全地儲存策略
description: 安全地儲存策略
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# 安全地儲存策略{#securely-storing-policies}

Adobe存取SDK在開發用於內容封裝和原則建立的應用程式時，提供極大的彈性。 在建立此類應用程式時，您可能希望允許某些用戶建立和修改策略，並限制其他用戶，使其只能將現有策略應用於內容。 在這種情況下，您必須實施必要的存取控制，以建立具有不同權限的使用者帳戶，以建立原則並將原則套用至內容。

在打包中使用策略之前，不會對其進行簽署或以其他方式保護其不受修改。 如果您擔心封裝工具的使用者會修改原則，請考慮簽署原則，以確保無法修改。

如需有關使用SDK建立應用程式的詳細資訊，請參閱&#x200B;*Adobe存取API參考*。
