---
seo-title: 概觀
title: 概觀
uuid: f4ae10ca-6e2a-4313-80a0-4c7377dba000
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 概觀{#overview}

為了向用戶端發行授權，您必須部署Adobe Access授權伺服器。 授權伺服器使用Adobe® Access™ SDK執行下列工作：

* 如果支援使用者名稱／密碼驗證，請處理驗證要求。
* 處理授權要求
* 處理獲取伺服器版本請求——所有伺服器必須對此類請求實施支援。
* 處理域註冊請求——僅在實施域伺服器時需要。
* 處理域取消註冊請求——僅在實施域伺服器時需要。
* 進程同步——僅在許可證指定同步要求時才需要。

此外，伺服器需要提供商業邏輯來驗證使用者、判斷使用者是否獲得檢視內容的授權，以及選擇性地追蹤授權使用情況。

如需本章所討論之Java API的詳細資訊，請參閱 *Adobe Access API參考*。
