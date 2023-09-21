---
description: 本主題說明效能相關考量事項。 全域組態檔中名為flashaccess-global.xml的任何設定都會影響效能。
title: 全域設定檔
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 效能調整 {#performance-tuning}

本主題說明效能相關考量事項。 全域組態檔中名為flashaccess-global.xml的任何設定都會影響效能。

## 全域設定檔 {#global-configuration-file}

組態檔包含下列設定元素：

* `<Caching>` 此 `<Caching>` 元素控制記憶體中組態檔的快取。 此 `<Caching>` 元素支援下列語法：

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 控制伺服器檢查組態檔更新的頻率。 低數值 `refreshDelaySeconds` 會對效能造成負面影響，而較高的值可以改善效能。

  另請參閱 *正在更新組態檔* 如需詳細資訊，請參閱 `refreshDelaySeconds`.

* `numTenants` 指定租使用者的數目。 低於租使用者數的值會影響效能，因為對其他租使用者的請求會導致快取遺漏。 任何設定資料的快取遺漏都會對效能造成負面影響。 因此，建議您將此值設定為大於為伺服器設定的租使用者數量，除非有您需要考慮的記憶體限制。

* `<Logging>` 此 `<Logging>` element指定記錄層級和記錄檔捲動的頻率。 此 `<Logging>` 元素支援下列語法：

  ```
  <Logging level="..." rollingFrequency="..."/>
  ```

* `<level>`  `level` 指定記錄檔的訊息。 值 `DEBUG` 會產生許多紀錄訊息，這可能會對效能產生負面影響。 建議您套用 `WARN` 以獲得最佳效能。 但是，此值可能會導致失去重要的執行階段資訊，例如授權稽核。 如果要以最低的效能影響儲存記錄資訊，您必須套用值 `INFO`.

* `<rollingFrequency>`  `rollingFrequency` 指定記錄檔的頻率 *已滾動*. *`Rolling`* 是將任何新記錄檔指定為使用中記錄檔的程式。 因此，無法再修改先前作用中的記錄檔，且會視為 *`rolled`*. 您可以將滾動間隔設為 `MINUTELY`， `HOURLY`， `TWICE-DAILY`， `DAILY`， `WEEKLY`， `MONTHLY`，或 `NEVER`.

另請參閱 *使用Adobe Primetime DRM SDK來保護內容* 以取得效能最佳化秘訣。
