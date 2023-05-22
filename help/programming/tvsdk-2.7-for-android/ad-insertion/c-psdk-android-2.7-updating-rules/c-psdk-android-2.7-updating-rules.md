---
description: 您可以使用TVSDK配置檔案(AdobeTVSDKonfig.json)更新VAST/VMAP響應上廣告創意選擇的優先順序。 您也可以使用此配置檔案來定義廣告創意的源URL轉換規則。
keywords: 創意選擇規則；AdobeTVSDKConfig;ad creative priities；轉換規則
title: 更新廣告創意選擇規則
exl-id: c11a7249-0036-4859-9e98-b0cac9ade5b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 概述 {#update-ad-creative-selection-rules-overview}

您可以使用TVSDK配置檔案(AdobeTVSDKonfig.json)更新VAST/VMAP響應上廣告創意選擇的優先順序。 您也可以使用此配置檔案來定義廣告創意的源URL轉換規則。

當視頻播放器向廣告伺服器請求時，VAST/VMAP響應通常包括多個廣告創意( `MediaFile` 元素)，每個元素都提供到不同容器編解碼器版本的URL。 在某些情況下，VAST/VMAP響應中的廣告創意各自為廣告提供不同的比特率。 如果要為這些廣告創意指定自己的優先順序和轉換規則，可以在 [!DNL AdobeTVSDKConfig.json] 配置檔案。

>[!IMPORTANT]
>
>* 不要更改TVSDK配置檔案的名稱。 名稱必須保留 [!DNL AdobeTVSDKConfig.json]。
>* 此檔案必須放在 [!DNL assets/] 資料夾。
>* 在播放廣告時更改音頻軌道不會更改音頻軌道。 播放器不應允許用戶在播放廣告時更改音頻軌道。
>


可以在中指定兩種類型的規則 [!DNL AdobeTVSDKConfig.json]: *優先順序* 規則和 *規範化* 規則。

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

使用JSON檔案指定Ad規則。 TVSDK的兩個版本中JSON檔案的格式保持相同。 但是，在TVSDK v2.5中，Ad規則JSON檔案必須托管在可通過HTTP URL訪問的位置上。 應用程式可以使用AuditudeSettings實例：

```
//TVSDK v2.5 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
