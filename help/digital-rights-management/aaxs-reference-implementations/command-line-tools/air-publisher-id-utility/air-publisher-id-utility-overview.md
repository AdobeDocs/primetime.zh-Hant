---
title: AIR Publisher ID公用程式概述
description: AIR Publisher ID公用程式概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# AIR Publisher ID公用程式概述 {#air-publisher-id-utility-overview}

在建置AIR檔案的過程中，AIR開發人員工具(ADT)會產生發佈者ID。 這是用來建立AIR檔案之憑證的唯一識別碼。 如果您在多個AIR應用程式中重複使用相同的憑證，它們就會有相同的發行者ID。AIR發行者ID公用程式是用來計算AIR應用程式的發行者ID。 1.5.2之後的AIR發行版本不會將產生的發行者ID寫入檔案，因此如果您使用AIR應用程式允許清單，則必須使用此工具來判斷發行者ID。

>[!NOTE]
>
>用於AIR允許清單強制執行的發行者ID與應用程式中的應用程式發行者指定的發行者ID不同 [!DNL application.xml] 檔案。
