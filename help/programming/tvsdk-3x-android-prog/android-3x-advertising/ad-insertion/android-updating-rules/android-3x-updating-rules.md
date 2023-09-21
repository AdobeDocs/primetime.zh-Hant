---
description: 您可以使用TVSDK設定檔案(AdobeTVSDKConfig.json)來更新VAST/VMAP回應上的廣告創意選擇優先順序。 您也可以使用此設定檔來定義廣告創意的來源URL轉換規則。
keywords: 創意選取規則；AdobeTVSDKConfig；廣告創意優先順序；轉換規則
title: 更新廣告創意選擇規則
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 概觀 {#update-ad-creative-selection-rules-overview}

您可以使用TVSDK設定檔案(AdobeTVSDKConfig.json)來更新VAST/VMAP回應上的廣告創意選擇優先順序。 您也可以使用此設定檔來定義廣告創意的來源URL轉換規則。

當您的視訊播放器向廣告伺服器提出請求時，VAST/VMAP回應通常包含多個廣告創意( `MediaFile` 元素)，每個元素都會提供不同容器轉碼器版本的URL。 在某些情況下，VAST/VMAP回應中的廣告創意會分別為廣告提供不同的位元速率。 如果您想為這些廣告創意指定自己的優先順序和轉換規則，可以在以下連結中進行： [!DNL AdobeTVSDKConfig.json] 組態檔。

>[!IMPORTANT]
>
>* 請勿變更TVSDK設定檔案的名稱。 名稱必須保留 [!DNL AdobeTVSDKConfig.json].
>* 此檔案必須放置在 [!DNL assets/] 資料夾。
>* 在廣告播放時變更音軌不會變更音軌。 播放器不應允許使用者在播放廣告時變更音軌。
>

您可以在中指定兩種規則 [!DNL AdobeTVSDKConfig.json]： *優先順序* 規則和 *標準化* 規則。

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

廣告規則是使用JSON檔案指定的。 兩個版本的TVSDK中，JSON檔案的格式相同。 不過，在TVSDK v3.0中，廣告規則JSON檔案必須託管於可透過HTTP URL存取的位置。 應用程式可以使用AuditudeSettings的例項：

```
//TVSDK v3.0 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
