---
description: 您可以使用TVSDK設定檔(AdobeTVSDKonfig.json)來更新VAST/VMAP回應廣告創意選擇的優先順序。 您也可以使用此設定檔案來定義廣告創作人員的來源URL轉換規則。
seo-description: 您可以使用TVSDK設定檔(AdobeTVSDKonfig.json)來更新VAST/VMAP回應廣告創意選擇的優先順序。 您也可以使用此設定檔案來定義廣告創作人員的來源URL轉換規則。
seo-title: 更新廣告創意選擇規則
title: 更新廣告創意選擇規則
uuid: 9eb4ccc2-425f-4c01-a095-f2043df4e25c
translation-type: tm+mt
source-git-commit: 6837c753b2f031b024ff510cda670340f346c4e1

---


# 概觀 {#updating-ad-creative-selection-rules}

您可以使用TVSDK設定檔(AdobeTVSDKonfig.json)來更新VAST/VMAP回應廣告創意選擇的優先順序。 您也可以使用此設定檔案來定義廣告創作人員的來源URL轉換規則。

當您的視訊播放器向廣告伺服器提出要求時，VAST/VMAP回應通常會包含多個廣告創意素材( `MediaFile` 元素)，其中每個元素都會提供不同容器轉碼器版本的URL。 在某些情況下，VAST/VMAP回應中的廣告創意素材會為廣告提供不同的位元速率。 如果您想要為這些廣告創意人員指定自己的優先順序和轉換規則，可以在設定檔案中 [!DNL AdobeTVSDKConfig.json] 這麼做。

>[!IMPORTANT]
>
>* 請勿變更TVSDK設定檔的名稱。 名稱必須保留 [!DNL AdobeTVSDKConfig.json]。
>* 此檔案應裝載在您的內容傳送網路(CDN)上。
>



您可以在中指定兩種類型的規則 [!DNL AdobeTVSDKConfig.json]:優 *先順序**,* 標準化規則。
