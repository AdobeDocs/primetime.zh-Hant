---
title: 實作使用模型概覽
description: 實作使用模型概覽
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# 實作使用模型概覽 {#implementing-the-usage-models-overview}

「參考實作」包含商業邏輯，可示範如何為封裝內容啟用下列四種不同的使用模式：

* 下載至擁有(DTO)
* 租賃/隨選視訊(VOD)
* 訂閱（隨心所欲）
* 廣告資助

若要啟用使用模式示範，請指定自訂屬性 `RI_UsageModelDemo=true` 封裝時。 如果您使用Media Packager命令列工具封裝內容，請指定：

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>如果您未在封裝時啟用選用示範模式，授權伺服器會使用封裝時指定的原則來發行授權。 如果指定了多個原則，則授權伺服器會使用第一個有效原則。

在示範中，伺服器上的商業邏輯會控制所產生授權的實際屬性。 在封裝時，內容中必須僅包含最低的原則資訊。 具體來說，原則只需指出存取內容是否需要驗證。 若要啟用所有四種使用模式，請包括一個允許匿名存取的原則（針對廣告資助模式）和一個需要使用者名稱/密碼驗證的原則（針對其他3種使用模式）。 當請求授權時，使用者端應用程式可以根據原則中的驗證資訊，決定是否提示使用者進行驗證。

若要控制使用模式，以向特定使用者頒發授權，可將專案新增至「參考實作」資料庫。 此 `Customer` 此表格包含用於驗證使用者的使用者名稱和密碼。 它也會指出使用者是否有訂閱。 擁有訂閱的使用者將依據 *訂閱* 使用模式。 若要授與使用者對下列專案的存取權： *下載至擁有* 或 *隨選影片* 使用模式，可新增專案至 `CustomerAuthorization` 表格，指定允許使用者存取的每個內容片段和使用模式。 請參閱 [!DNL PopulateSampleDB.sql] 指令碼，以瞭解填入每個表格的詳細資訊。

當使用者請求授權時，Reference Implementation Server會檢查使用者端傳送的中繼資料，以判斷內容是否已使用封裝 `RI_UsageModelDemo` 屬性。 若是如此，會使用下列商業規則：

* 如果其中一個原則需要驗證：

   * 如果請求包含有效的驗證Token，請在Customer資料庫表格中尋找使用者。 如果找到使用者：

      * 如果 `Customer.IsSubscriber` 屬性為 `true`，為產生授權 *訂閱* 使用模式，並將其傳送給使用者。

      * 尋找中的記錄 `CustomerAuthorization` 此使用者和內容ID的資料庫表格。 如果找到記錄：

         * 如果 `CustomerAuthorization.UsageType` 是 `DTO`，為產生授權 *下載至擁有* 使用模式，並將其傳送給使用者。

         * 如果 `CustomerAuthorization.UsageType` 是 `VOD`，為產生授權 *隨選影片* 使用模式，並將其傳送給使用者。

   * 如果沒有任何原則允許匿名存取：

      * 如果請求中沒有有效的驗證Token，請傳回「需要驗證」錯誤。
      * 否則會傳回「未授權」錯誤。

* 如果其中一個原則允許匿名存取，請為廣告資助的使用模式產生授權，並將其傳送給使用者。

在「參考實作」伺服器可以核發使用模式示範的授權之前，伺服器必須設定為指定四種使用模式中每種模式的授權產生方式。 這是透過為每個使用模式指定原則來完成的。 此參考實作包含四個原則範例( [!DNL dto-policy.pol]， [!DNL vod-policy.pol]， [!DNL sub-policy.pol]， [!DNL ad-policy.pol])或您可以用您自己的原則替代。 在 [!DNL flashaccess-refimpl.properties]，設定以下屬性以指定用於每個使用模式的原則，並將原則檔案放置在 `config.resourcesDirectory` 屬性：

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
