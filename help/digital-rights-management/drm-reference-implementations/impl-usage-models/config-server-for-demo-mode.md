---
title: 配置使用模式演示模式
description: 配置使用模式演示模式
copied-description: true
exl-id: 593acfbd-fd37-4bab-ac8e-5cb62963fac4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 配置使用模式演示模式{#configure-usage-model-demo-mode}

在「參考實施」伺服器為使用模式演示頒發許可證之前，必須配置伺服器以指定為四種使用模式中的每種使用模式生成許可證的方式。 這意味著您需要為每個使用模型指定DRM策略。 「參考實施」(Reference Implementation)包括以下示例DRM策略， [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] 目錄：

* `dto-policy.pol`  — （自主下載）
* `vod-policy.pol`  — （租賃/視頻點播）
* `sub-policy.pol`  — （訂閱）
* `ad-policy.pol`  — （廣告資助）

>[!NOTE]
>
>您可以用自己的DRM策略替換這些示例策略。

1. 在中設定這些屬性 [!DNL flashaccess-refimpl.properties] 要指定計畫應用於每個使用模型的DRM策略：

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

1. 將示例策略檔案複製到您在 `config.resourcesDirectory` 物業 [!DNL flashaccess-refimpl.properties]。
