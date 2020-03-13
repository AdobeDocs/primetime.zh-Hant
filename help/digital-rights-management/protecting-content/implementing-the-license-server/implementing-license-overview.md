---
seo-title: 授權伺服器概觀
title: 授權伺服器概觀
uuid: 8c62376b-b159-4297-9322-75d62947e84e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 概觀 {#license-server-overview}

您必須先部署Adobe Primetime DRM授權伺服器，才能向客戶發行授權。 授權伺服器使用Primetime DRM SDK執行多項工作。

要實施許可證伺服器：

* 如果支援使用者名稱／密碼驗證，請處理驗證要求。
* 處理授權要求
* 處理獲取伺服器版本請求——所有伺服器必須對此類請求實施支援。
* 處理域註冊請求——僅在實施域伺服器時需要。
* 處理域取消註冊請求——僅在實施域伺服器時需要。
* 進程同步——僅在許可證指定同步要求時才需要。

此外，伺服器需要提供商業邏輯來驗證使用者、判斷使用者是否獲得檢視內容的授權，以及選擇性地追蹤授權使用情況。

如需 *Java API的詳細資訊* ，請參閱Adobe Primetime DRM API參考。
