---
description: 雖然預設的創意重新封裝服務(CRS)藍本是使用一個內容傳送網路(CDN)，但您可以在多個CDN上部署CRS資產。
seo-description: 雖然預設的創意重新封裝服務(CRS)藍本是使用一個內容傳送網路(CDN)，但您可以在多個CDN上部署CRS資產。
seo-title: CRS廣告傳送的多個CDN支援
title: CRS廣告傳送的多個CDN支援
uuid: c5557a38-aa49-4161-bb58-3e8dff9a4d64
translation-type: tm+mt
source-git-commit: f327b45de7e482dcb25407659846b2098f1fd49d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# CRS廣告傳送{#multiple-cdn-support-for-crs-ad-delivery}的多個CDN支援

雖然預設的創意重新封裝服務(CRS)藍本是使用一個內容傳送網路(CDN)，但您可以在多個CDN上部署CRS資產。

## 需求

您可基於下列原因使用多個CDN:

* 需要針對大型檢視事件進行放大
* 將CRS資產的CDN來源與主內容的CDN來源相符的需求。
* 使用與CRS預設CDN(Akamai)不同CDN的需求。

當資訊清單伺服器對轉碼請求進行查詢時，會使用包含許多查詢參數的引導URL。 如果您已設定多CDN環境，啟動載入URL也需要包含`ptcdn`參數。 資訊清單伺服器會使用此參數來識別要從中取得廣告轉碼版本的CDN伺服器。

如需詳細資訊，請參閱CRS檔案中的[多CDN支援](../../creative-repackaging-service/multi-cdn-supportt.md)。
