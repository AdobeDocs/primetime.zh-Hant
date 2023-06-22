---
title: 增強授權鏈結
description: 增強授權鏈結
copied-description: true
exl-id: 269e7866-fe43-45a8-84d8-c51e4fc95f77
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 增強授權鏈結 {#enhanced-license-chaining}

您可以使用增強型授權鏈結來更新授權，方法是使用父根授權批次更新授權。

Primetime DRM 2.0支援許可證鏈結，其中葉和根許可證都繫結到特定機器。 Primetime DRM 3.0和更新版本支援增強型授權鏈結，其中分葉繫結至根授權，而只有根授權繫結至特定電腦或網域。 增強型授權鏈結支援將分葉授權與內容嵌入，使用者端只需從授權伺服器取得根授權，即可使用受保護的內容。

如果要啟用增強型授權鏈結，則必須將根加密金鑰指派給Primetime DRM原則。 根加密金鑰用來以密碼方式將Leaf授權繫結到根授權。

>[!NOTE]
>
>Primetime DRM使用者端3.0版或更新版本支援增強型授權鏈結。 如果舊版使用者端請求支援增強型授權鏈結之內容的授權，授權伺服器仍可使用Primetime DRM 2.0支援的授權鏈結向此使用者端發行授權。

使用案例範例：使用此選項可下載單一根授權來更新任何連結的授權。 例如，實作訂閱模型，只要使用者每月更新訂閱，即可播放內容。 此方法的好處是，使用者只需取得單一授權，即可更新其所有訂閱授權。
