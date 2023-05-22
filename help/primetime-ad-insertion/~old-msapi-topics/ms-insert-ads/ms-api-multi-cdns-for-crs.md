---
description: 雖然預設的創意重新打包服務(CRS)方案是使用一個內容交付網路(CDN)，但您可以在多個CDN上部署CRS資產。
title: 對CRS和交付的多個CDN支援
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# 對CRS和交付的多個CDN支援 {#multiple-cdn-support-for-crs-ad-delivery}

雖然預設的創意重新打包服務(CRS)方案是使用一個內容交付網路(CDN)，但您可以在多個CDN上部署CRS資產。

## 要求

您可以使用多個CDN，原因如下：

* 對大型查看事件進行擴展的要求
* 將CRS資產的CDN源與主內容的CDN源匹配的要求。
* 使用CRS預設CDN(Akamai)中的不同CDN的要求。

當清單伺服器對轉碼請求進行查找時，它使用包含多個查詢參數的引導URL。 如果已設定多CDN環境，則引導URL還需要包含 `ptcdn` 的下界。 清單伺服器使用此參數來標識從中獲取廣告的轉碼版本的CDN伺服器。

有關詳細資訊，請參閱 [多CDN支援](../../~old-creative-repackaging-service/multi-cdn-supportt.md) 在CRS文檔中。
