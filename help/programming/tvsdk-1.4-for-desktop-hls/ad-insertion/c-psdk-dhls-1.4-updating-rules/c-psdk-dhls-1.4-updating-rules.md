---
description: 您可以使用TVSDK配置檔案(AdobeTVSDKonfig.json)更新VAST/VMAP響應上廣告創意選擇的優先順序。 您也可以使用此配置檔案來定義廣告創意的源URL轉換規則。
title: 更新廣告創意選擇規則
exl-id: 6664c120-2d4d-4cc0-8d9d-4bd8a66a5e88
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# 概述 {#updating-ad-creative-selection-rules}

您可以使用TVSDK配置檔案(AdobeTVSDKonfig.json)更新VAST/VMAP響應上廣告創意選擇的優先順序。 您也可以使用此配置檔案來定義廣告創意的源URL轉換規則。

當視頻播放器向廣告伺服器請求時，VAST/VMAP響應通常包括多個廣告創意( `MediaFile` 元素)，每個元素都提供到不同容器編解碼器版本的URL。 在某些情況下，VAST/VMAP響應中的廣告創意各自為廣告提供不同的比特率。 如果要為這些廣告創意指定自己的優先順序和轉換規則，可以在 [!DNL AdobeTVSDKConfig.json] 配置檔案。

>[!IMPORTANT]
>
>* 不要更改TVSDK配置檔案的名稱。 名稱必須保留 [!DNL AdobeTVSDKConfig.json]。
>* 此檔案應托管在您的內容分發網路(CDN)上。
>


可以在中指定兩種類型的規則 [!DNL AdobeTVSDKConfig.json]: *優先順序* 規則和 *規範化* 規則。
