---
title: 實施使用模型概述
description: 實施使用模型概述
copied-description: true
exl-id: 48e7db54-484f-4c46-9a4e-a51bae7c84b4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# 實施使用模型概述 {#implementing-the-usage-models-overview}

「參考實施」包括業務邏輯，用於演示如何為打包的內容啟用以下四種不同的使用模式：

* 自行下載(DTO)
* 租賃/視頻點播(VOD)
* 訂閱（您可以享用）
* 廣告資助

要啟用使用模式演示，請指定自定義屬性 `RI_UsageModelDemo=true` 打包時。 如果使用「媒體打包器」命令行工具打包內容，請指定：

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>如果您在打包時未激活可選演示模式，則許可證伺服器將使用打包時指定的策略來頒發許可證。 如果指定了多個策略，則許可證伺服器使用第一個有效策略。

在演示中，伺服器上的業務邏輯控制生成的許可證的實際屬性。 在打包時，內容中只能包含最少的策略資訊。 具體來說，該策略只需要指示是否需要身份驗證才能訪問內容。 要啟用所有四種使用模式，請包括一個允許匿名訪問的策略（對於廣告資助的模式）和一個要求用戶名/密碼驗證的策略（對於其他三種使用模式）。 當請求許可時，客戶端應用程式可以基於策略中的驗證資訊確定是否提示用戶進行驗證。

為了控制在其下將向特定用戶頒發許可證的使用模型，可以將條目添加到參考實現資料庫中。 的 `Customer` 表包含用於驗證用戶的用戶名和密碼。 它還指示用戶是否具有訂閱。 具有訂閱的用戶將根據 *訂閱* 使用模式。 在 *下載到Own* 或 *視頻點播* 使用模型，可將條目添加到 `CustomerAuthorization` 表，它指定允許用戶訪問的每段內容和使用模型。 查看 [!DNL PopulateSampleDB.sql] 用於填充每個表的詳細資訊的指令碼。

當用戶請求許可證時，參考實現伺服器檢查客戶端發送的元資料以確定內容是否使用 `RI_UsageModelDemo` 屬性。 如果是，則使用以下業務規則：

* 如果其中一個策略需要身份驗證：

   * 如果請求包含有效的驗證令牌，請在「客戶」資料庫表中查找用戶。 如果找到用戶：

      * 如果 `Customer.IsSubscriber` 屬性 `true`，為 *訂閱* 使用模式併發送給用戶。

      * 在 `CustomerAuthorization` 此用戶和內容ID的資料庫表。 如果找到記錄：

         * 如果 `CustomerAuthorization.UsageType` 是 `DTO`，為 *下載到擁有* 使用模式併發送給用戶。

         * 如果 `CustomerAuthorization.UsageType` 是 `VOD`，為 *視頻點播* 使用模式併發送給用戶。
   * 如果所有策略都不允許匿名訪問：

      * 如果請求中沒有有效的驗證令牌，則返回「需要驗證」錯誤。
      * 否則返回「未授權」錯誤。


* 如果其中一個策略允許匿名訪問，則為廣告資助的使用模式生成許可證並將其發送給用戶。

在參考實施伺服器為使用模型演示頒發許可證之前，需要配置伺服器以指定如何為四種使用模型中的每種生成許可證。 這可以通過為每個使用模型指定策略來完成。 參考實施包括四個示例策略( [!DNL dto-policy.pol]。 [!DNL vod-policy.pol]。 [!DNL sub-policy.pol]。 [!DNL ad-policy.pol])，或者您可以替換自己的策略。 在 [!DNL flashaccess-refimpl.properties]，設定以下屬性以指定用於每個使用模型的策略，並將策略檔案放置在由 `config.resourcesDirectory` 屬性：

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
