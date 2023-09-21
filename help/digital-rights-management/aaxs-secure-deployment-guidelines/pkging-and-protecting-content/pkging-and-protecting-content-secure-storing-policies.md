---
title: 安全地儲存原則
description: 安全地儲存原則
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 安全地儲存原則{#securely-storing-policies}

Adobe存取SDK在開發用於內容封裝和原則建立的應用程式時，可提供極大的彈性。 建立這類應用程式時，您可能想要允許某些使用者建立和修改原則，並限制其他使用者，讓他們只能將現有原則套用至內容。 如果是這種情況，您必須實作必要的存取控制，以建立具有不同許可權的使用者帳戶，以便建立原則以及將原則套用至內容。

原則在用於封裝之前，不會經過簽署，或受到修改保護。 如果您擔心封裝工具的使用者修改原則，您應該考慮簽署原則以確保無法修改原則。

如需使用SDK建立應用程式的詳細資訊，請參閱 *Adobe存取API參考*.
