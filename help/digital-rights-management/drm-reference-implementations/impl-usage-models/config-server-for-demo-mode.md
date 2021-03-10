---
title: 設定使用模式示範模式
description: 設定使用模式示範模式
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# 配置使用模型演示模式{#configure-usage-model-demo-mode}

在「參考實作」伺服器為使用模式示範發行授權之前，您必須先設定伺服器，以指定四種使用模式各自產生授權的方式。 這表示您需要為每個使用模型指定DRM原則。 「參考實施」在[!DNL Reference Implementation/Server/Reference Implementation Server/resources/]目錄中包含以下DRM策略示例：

* `dto-policy.pol` -（下載至擁有）
* `vod-policy.pol` -（租金／隨選視訊）
* `sub-policy.pol` -（訂閱）
* `ad-policy.pol` -（廣告資助）

>[!NOTE]
>
>您可以用自己的DRM策略替換這些示例策略。

1. 在[!DNL flashaccess-refimpl.properties]中設定以下屬性，以指定您打算應用到每個使用模型的DRM策略：

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

1. 將示例策略檔案複製到[!DNL flashaccess-refimpl.properties]中`config.resourcesDirectory`屬性中指定的目錄。
