---
title: 設定使用模式示範模式
description: 設定使用模式示範模式
copied-description: true
exl-id: 593acfbd-fd37-4bab-ac8e-5cb62963fac4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 設定使用模式示範模式{#configure-usage-model-demo-mode}

在「參考實作」伺服器可以核發使用模式示範的授權之前，您必須設定伺服器以指定四個使用模式中每一個模式的授權產生方式。 這表示您需要為每個使用模式指定DRM原則。 「參考實作」包含下列DRM原則範例： [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] 目錄：

* `dto-policy.pol` - （下載至擁有）
* `vod-policy.pol` - （租賃/隨選視訊）
* `sub-policy.pol` - （訂閱）
* `ad-policy.pol` - （廣告資助）

>[!NOTE]
>
>您可以使用自己的DRM政策來取代這些範例政策。

1. 在中設定這些屬性 [!DNL flashaccess-refimpl.properties] 若要指定您計畫套用至每個使用模型的DRM原則，請執行下列動作：

   ```
   # DRM Policy file name for Download To Own usage 
   RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol 
   # DRM Policy file name for Rental usage 
   RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol 
   # DRM Policy file name for Subscription usage 
   RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol 
   # DRM Policy file name for Ad Supported (free) usage 
   RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
   ```

1. 將範例原則檔複製到您在 `config.resourcesDirectory` 中的屬性 [!DNL flashaccess-refimpl.properties].
