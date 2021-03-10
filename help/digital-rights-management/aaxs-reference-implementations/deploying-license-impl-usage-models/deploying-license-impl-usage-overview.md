---
title: 實作使用模型概觀
description: 實作使用模型概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# 實施使用模型概述{#implementing-the-usage-models-overview}

「參考實作」包含商業邏輯，可示範如何針對封裝內容啟用下列四種不同的使用模式：

* 下載至擁有(DTO)
* 租金／隨選視訊(VOD)
* 訂閱（您可以享用的所有功能）
* 廣告贊助

若要啟用使用模式示範，請在封裝時指定自訂屬性`RI_UsageModelDemo=true`。 如果您使用Media Packager命令列工具封裝內容，請指定：

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>如果您未在封裝時啟用選用的示範模式，則授權伺服器會使用封裝時指定的原則來核發授權。 如果指定了多個策略，則許可證伺服器使用第一個有效策略。

在示範中，伺服器上的商業邏輯會控制所產生授權的實際屬性。 在封裝時，內容中只能包含最少的原則資訊。 具體來說，原則只需要指出存取內容是否需要驗證。 若要啟用所有4種使用模式，請包含一種允許匿名存取的原則（針對廣告資助的模型），以及一種需要使用者名稱／密碼驗證的原則（針對其他3種使用模式）。 當請求許可時，客戶端應用程式可以根據策略中的驗證資訊確定是否提示用戶進行驗證。

為了控制將授予特定用戶許可的使用模式，可以將條目添加到「參考實施」資料庫。 `Customer`表格包含用於驗證用戶的用戶名和密碼。 它也會指出使用者是否有訂閱。 使用訂閱的使用者將依&#x200B;*Subscription*&#x200B;使用模式取得授權。 為了在&#x200B;*下載到Own*&#x200B;或&#x200B;*Video on Demand*&#x200B;使用模式下授予用戶訪問權，可以在`CustomerAuthorization`表中添加一個條目，該表指定允許用戶訪問的每段內容和使用模式。 有關填入每個表的詳細資訊，請參見[!DNL PopulateSampleDB.sql]指令碼。

當使用者要求授權時，參考實作伺服器會檢查用戶端傳送的中繼資料，以判斷內容是否使用`RI_UsageModelDemo`屬性封裝。 如果是，則使用下列業務規則：

* 如果其中一個策略需要驗證：

   * 如果請求包含有效的驗證Token，請在Customer資料庫表格中尋找使用者。 如果找到用戶：

      * 如果`Customer.IsSubscriber`屬性為`true`，請為&#x200B;*訂閱*&#x200B;使用模式產生授權，並傳送給使用者。

      * 在`CustomerAuthorization`資料庫表中查找此用戶和內容ID的記錄。 如果找到記錄：

         * 如果`CustomerAuthorization.UsageType`是`DTO`，請為&#x200B;*下載至擁有*&#x200B;使用模式產生授權，並傳送給使用者。

         * 如果`CustomerAuthorization.UsageType`是`VOD`，請為&#x200B;*隨選視訊使用模式產生授權，並傳送給使用者。*
   * 如果沒有任何策略允許匿名訪問：

      * 如果請求中沒有有效的驗證Token，請傳回「需要驗證」錯誤。
      * 否則傳回「未授權」錯誤。


* 如果其中一個原則允許匿名存取，請為廣告資助的使用模式產生授權，並傳送給使用者。

在「參考實作」伺服器可針對使用模式示範發佈授權之前，必須先設定伺服器，以指定四種使用模式各自產生授權的方式。 這是透過為每個使用模式指定原則來完成的。 「參考實作」包含4個範例原則([!DNL dto-policy.pol]、[!DNL vod-policy.pol]、[!DNL sub-policy.pol]、[!DNL ad-policy.pol])，或您可以替代自己的原則。 在[!DNL flashaccess-refimpl.properties]中，設定以下屬性以指定要用於每個使用模式的策略，並將策略檔案放在由`config.resourcesDirectory`屬性指定的目錄中：

```
# Policy file name for Download To Own usage  
RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol  
# Policy file name for Rental usage  
RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol  
# Policy file name for Subscription usage  
RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol  
# Policy file name for Ad Supported (free) usage  
RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
```

