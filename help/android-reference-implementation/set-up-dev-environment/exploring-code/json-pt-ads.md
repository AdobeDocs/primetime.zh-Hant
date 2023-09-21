---
title: Primetime廣告的JSON物件
description: 當型別值為Primetime廣告時，下方的程式碼區塊會定義詳細資訊JSON物件。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Primetime廣告的JSON物件 {#json-object-for-primetime-ads}

當型別值為Primetime廣告時，下方的程式碼區塊會定義詳細資訊JSON物件。

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
| 網域 | 用於廣告請求的Primetime廣告網域。 |
| mediaid | 已針對Primetime內容設定的媒體輔助程式。 |
| zoneid | Primetime廣告zoneid。 如需詳細資訊，請參閱Primetime廣告檔案。 |
| 目標定位 | 用於針對內容定位特定廣告的索引鍵/值配對陣列。 |

另請參閱 [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) 以取得這些屬性值的詳細資訊。
