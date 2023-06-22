---
title: 安全地儲存原則
description: 安全地儲存原則
copied-description: true
exl-id: fd335a0c-7eb1-4159-958f-7302fce98cef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 安全地儲存原則{#securely-storing-policies}

Adobe存取SDK在開發用於內容封裝和原則建立的應用程式時，提供極大的彈性。 建立這類應用程式時，您可能希望允許某些使用者建立和修改原則，並限制其他使用者，讓他們只能將現有原則套用至內容。 如果是這種情況，您必須實作必要的存取控制，以建立具有不同許可權的使用者帳戶，以便建立原則以及將原則套用至內容。

原則在用於封裝之前，不會被簽署或以其他方式保護以防止修改。 如果您擔心封裝工具的使用者修改原則，您應該考慮簽署原則以確保無法修改原則。

如需使用SDK建立應用程式的詳細資訊，請參閱 *Adobe存取API參考*.
