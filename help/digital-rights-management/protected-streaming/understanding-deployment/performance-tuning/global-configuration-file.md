---
description: 本主題說明效能相關考量事項。 全域組態檔中名為flashaccess-global.xml的任何設定都會影響效能。
title: 全域設定檔
exl-id: 52d41476-d352-4c02-8af6-25c0fe6bcaa7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 效能調整 {#performance-tuning}

本主題說明效能相關考量事項。 全域組態檔中名為flashaccess-global.xml的任何設定都會影響效能。

## 全域設定檔 {#global-configuration-file}

組態檔包含下列設定元素：

* `<Caching>` 此 `<Caching>` element控制記憶體中組態檔的快取。 此 `<Caching>` 元素支援下列語法：

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 控制伺服器檢查組態檔更新的頻率。 以下專案的低值 `refreshDelaySeconds` 會對效能造成負面影響，而較高的值可以改善效能。

   另請參閱 *更新組態檔* 有關下列專案的詳細資訊： `refreshDelaySeconds`.

* `numTenants` 指定租使用者的數量。 低於租使用者數的值會影響效能，因為對其他租使用者的請求會導致快取遺漏。 任何設定資料的快取遺漏都會對效能造成負面影響。 因此，除非您需要考慮記憶體限制，否則建議您將此值設定為高於為伺服器設定的租使用者數量。

* `<Logging>` 此 `<Logging>` element會指定記錄層級和記錄檔的捲動頻率。 此 `<Logging>` 元素支援下列語法：

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` 指定記錄檔的訊息。 值 `DEBUG` 會產生許多紀錄訊息，這可能會對效能造成負面影響。 建議您套用 `WARN` 以獲得最佳效能。 不過，此值可能會導致遺失重要的執行階段資訊，例如授權稽核。 如果您想要以最低的效能影響儲存記錄資訊，您必須套用值 `INFO`.

* `<rollingFrequency>`  `rollingFrequency` 指定記錄檔的頻率 *已滾動*. *`Rolling`* 是將任何新記錄檔指定為使用中記錄檔的程式。 因此，先前作用中的記錄檔無法再修改，且會被視為 *`rolled`*. 您可以將滾動間隔設定為 `MINUTELY`， `HOURLY`， `TWICE-DAILY`， `DAILY`， `WEEKLY`， `MONTHLY`，或 `NEVER`.

另請參閱 *使用Adobe Primetime DRM SDK保護內容* 以取得效能最佳化秘訣。
