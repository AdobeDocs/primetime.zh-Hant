---
description: 'null'
seo-description: 'null'
seo-title: 設定使用模式示範模式
title: 設定使用模式示範模式
uuid: f818c7fc-e88f-4fa4-926e-08a1337b28d3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 設定使用模式示範模式{#configure-usage-model-demo-mode}

在「參考實作」伺服器為使用模式示範發行授權之前，您必須先設定伺服器，以指定四種使用模式各自產生授權的方式。 這表示您需要為每個使用模型指定DRM原則。 「參考實施」(Reference Implementation)在目錄中包括以下DRM策 [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] 略示例：

* `dto-policy.pol` -（下載至擁有）
* `vod-policy.pol` -（租金／隨選視訊）
* `sub-policy.pol` -（訂閱）
* `ad-policy.pol` -（廣告資助）

>[!NOTE]
>
>您可以用自己的DRM策略替換這些示例策略。

1. 在中設定這些 [!DNL flashaccess-refimpl.properties] 屬性，以指定您計畫應用於每個使用模型的DRM策略：

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

1. 將範例原則檔案複製至您在中屬性中指定 `config.resourcesDirectory` 的目錄 [!DNL flashaccess-refimpl.properties]。
