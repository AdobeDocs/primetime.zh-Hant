---
title: AIR發佈者ID實用程式概述
description: AIR發佈者ID實用程式概述
copied-description: true
exl-id: ad982ec8-0180-4185-8752-08592cabef3d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# AIR發佈者ID實用程式概述 {#air-publisher-id-utility-overview}

作為構建AIR檔案過程的一部分，AIR開發工具(ADT)將生成發佈者ID。 這是用於生成AIR檔案的證書的唯一標識符。 如果對多個AIR應用程式重複使用相同的證書，則它們將具有相同的發佈者ID。AIR發佈者ID實用程式用於計算AIR應用程式的發佈者ID。 AIR1.5.2之後的版本不要將生成的發佈者ID寫入檔案，因此，如果您使用的是AIR應用程式允許清單，則有必要使用此工具來確定發佈者ID。

>[!NOTE]
>
>用於AIR允許清單強制的發佈者ID與應用程式的應用程式發佈者指定的發佈者ID不相同 [!DNL application.xml] 的子菜單。
