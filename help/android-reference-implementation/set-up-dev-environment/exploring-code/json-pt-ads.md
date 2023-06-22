---
title: Primetime廣告的JSON物件
description: 當型別值為Primetime廣告時，下面的程式碼區塊會定義詳細資訊JSON物件。
exl-id: b1392781-2dfb-4934-b1ce-1c761cbfb22d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Primetime廣告的JSON物件 {#json-object-for-primetime-ads}

當型別值為Primetime廣告時，下面的程式碼區塊會定義詳細資訊JSON物件。

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
| mediaid | 已針對此內容在Primetime廣告中設定的mediaid。 |
| zoneid | Primetime廣告zoneid。 如需詳細資訊，請參閱Primetime廣告檔案。 |
| 目標定位 | 用來鎖定內容特定廣告的索引鍵/值組陣列。 |

另請參閱 [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) 以取得這些屬性值的詳細資訊。
