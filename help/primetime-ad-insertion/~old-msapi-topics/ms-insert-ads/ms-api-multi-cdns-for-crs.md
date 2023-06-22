---
description: 雖然預設的Creative重新封裝服務(CRS)情境是使用一個Content Delivery Network (CDN)，但您可以在多個CDN上部署CRS資產。
title: CRS廣告傳遞的多重CDN支援
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# CRS廣告傳遞的多重CDN支援 {#multiple-cdn-support-for-crs-ad-delivery}

雖然預設的Creative重新封裝服務(CRS)情境是使用一個Content Delivery Network (CDN)，但您可以在多個CDN上部署CRS資產。

## 需求

基於以下原因，您可以使用多個CDN：

* 針對大型檢視事件進行擴充的需求
* 必須符合CRS資產的CDN來源與主要內容的CDN來源。
* 需要使用與CRS預設CDN (Akamai)不同的CDN。

資訊清單伺服器查詢轉碼請求時，會使用包含許多查詢引數的啟動程式URL。 如果您已設定多CDN環境，啟動程式URL也需要包含 `ptcdn` 引數。 資訊清單伺服器會使用此引數來識別要從中取得轉碼版廣告的CDN伺服器。

如需詳細資訊，請參閱 [多CDN支援](../../~old-creative-repackaging-service/multi-cdn-supportt.md) CRS檔案中。
