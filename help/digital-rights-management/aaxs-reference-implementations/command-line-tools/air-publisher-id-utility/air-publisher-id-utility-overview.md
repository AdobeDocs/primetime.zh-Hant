---
seo-title: AIR Publisher ID公用程式總覽
title: AIR Publisher ID公用程式總覽
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# AIR Publisher ID公用程式總覽 {#air-publisher-id-utility-overview}

在建立AIR檔案的過程中，AIR開發人員工具(ADT)會產生發佈者ID。 此識別碼是用於建立AIR檔案之憑證的唯一識別碼。 如果您對多個AIR應用程式重複使用相同的憑證，則它們會有相同的發行者ID。AIR Publisher ID公用程式可用來計算AIR應用程式的發行者ID。 1.5.2之後的AIR版本不會將產生的發佈者ID寫入檔案，因此，如果您使用AIR應用程式允許清單，必須使用此工具來判斷發佈者ID。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>用於AIR允許清單執行的發佈者ID與應用程式發佈者在應用程式檔案中指定的發佈者ID不相 [!DNL application.xml] 同。
