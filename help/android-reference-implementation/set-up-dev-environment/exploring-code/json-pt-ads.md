---
seo-title: Primetime廣告的JSON物件
title: Primetime廣告的JSON物件
uuid: acf968d2-9856-4ed6-a046-1ac17d176571
description: 當類型值為Primetime廣告時，下方的程式碼區塊會定義詳細資訊JSON物件。
seo-description: 當類型值為Primetime廣告時，下方的程式碼區塊會定義詳細資訊JSON物件。
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Primetime廣告的JSON物件 {#json-object-for-primetime-ads}

當類型值為Primetime廣告時，下方的程式碼區塊會定義詳細資訊JSON物件。

```
“metadata”: {
    “ad” :  {
        “type”: “Primetime ads”,
        “details”: {
            "domain": "sandbox2.auditude.com",
            "mediaid": "rom_asset_case_1",
            "zoneid": "109754",
            "targeting": [
                {
                    "key": "osmfKeyMulAdsAvail12346",
                    "value": "MulAdsAvail12346"
                }
            ]
        }
    }
}
```

| 屬性 | 說明 |
|---|---|
| 域 | 用於廣告請求的Primetime廣告網域。 |
| mediaid | 已在Primetime廣告中針對此內容設定的媒體。 |
| zoneid | Primetime廣告zoneid。 如需詳細資訊，請參閱Primetime廣告檔案。 |
| 定位 | 用於定位內容特定廣告的索引鍵／值對陣列。 |

如需 [這些屬性之值的詳細資訊，請參閱com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) 。