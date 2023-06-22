---
description: 您可以使用TVSDK設定檔案(AdobeTVSDKConfig.json)來更新VAST/VMAP回應上廣告創意選擇的優先順序。 您也可以使用此設定檔來定義廣告創意的來源URL轉換規則。
title: 更新廣告創意選擇規則
exl-id: 6664c120-2d4d-4cc0-8d9d-4bd8a66a5e88
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# 概觀 {#updating-ad-creative-selection-rules}

您可以使用TVSDK設定檔案(AdobeTVSDKConfig.json)來更新VAST/VMAP回應上廣告創意選擇的優先順序。 您也可以使用此設定檔來定義廣告創意的來源URL轉換規則。

當您的視訊播放器向廣告伺服器提出請求時，VAST/VMAP回應通常包括多個廣告創意( `MediaFile` 元素)，每個元素都會提供不同容器轉碼器版本的URL。 在某些情況下，VAST/VMAP回應中的廣告創意會分別為廣告提供不同的位元速率。 如果您想為這些廣告創意指定自己的優先順序和轉換規則，可以在 [!DNL AdobeTVSDKConfig.json] 設定檔。

>[!IMPORTANT]
>
>* 請勿變更TVSDK設定檔的名稱。 名稱必須保留 [!DNL AdobeTVSDKConfig.json].
>* 此檔案應託管於您的內容傳遞網路(CDN)上。
>


您可以在下列位置指定兩種規則： [!DNL AdobeTVSDKConfig.json]： *優先順序* 規則和 *標準化* 規則。
