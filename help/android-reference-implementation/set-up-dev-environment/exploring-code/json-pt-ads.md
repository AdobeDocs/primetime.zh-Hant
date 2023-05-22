---
title: 用於黃金時段廣告的JSON對象
description: 當類型值為Mogfise廣告時，下面的代碼塊定義詳細資訊JSON對象。
exl-id: b1392781-2dfb-4934-b1ce-1c761cbfb22d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 用於黃金時段廣告的JSON對象 {#json-object-for-primetime-ads}

當類型值為Mogfise廣告時，下面的代碼塊定義詳細資訊JSON對象。

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
| 域 | 用於廣告請求的黃金時段廣告域。 |
| 調解 | 在黃金時段廣告中為此內容設定的媒體。 |
| 宗 | 黃金時段廣告區域節。 有關詳細資訊，請參閱黃金時段廣告文檔。 |
| 目標 | 用於針對內容的特定廣告的密鑰/值對陣列。 |

請參閱 [com.adobe.mediacore.metadata.AuditySettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) 的子菜單。
