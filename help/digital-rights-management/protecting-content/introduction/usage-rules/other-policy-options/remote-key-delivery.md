---
title: 遠端和本機iOS金鑰傳遞
description: 遠端和本機iOS金鑰傳遞
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 遠端和本機iOS金鑰傳遞 {#remote-and-local-ios-key-delivery}

Adobe Primetime支援下列將金鑰傳送至iOS使用者端的選項：

* **遠端**  — 依照HTTP即時資料流(HLS)規格中指定的方式執行；M3U8資訊清單指定HTTPS路徑，其中包含應該用來解密資料流中下列加密區段的AES金鑰。 當您指定 `Remote` 在Primetime DRM原則中，使用者端裝置必須連線到遠端HTTPS伺服器才能取得AES金鑰。

* **本機**  — 當您指定 `Local` 在Primetime DRM中，本機HTTPS伺服器內嵌於iOS應用程式，然後管理所有AES金鑰要求，而不是連線至網際網路/網路AES金鑰。 內嵌HTTPS伺服器會自動在P應用程式中設定和設定。 應用程式開發人員不需要介入。

遠端金鑰傳遞會透過用來封裝內容的Primetime DRM原則來啟用。 若要變更此設定，您必須重新封裝內容。 如果您啟用遠端金鑰傳遞，則必須部署可管理iOS使用者端之金鑰請求的Primetime DRM金鑰伺服器。 不過，其他平台上的使用者端的工作流程沒有變更。

>[!NOTE]
>
>金鑰傳遞選擇只會影響iOS使用者端。 所有其他使用HLS內容的裝置，例如Android和案頭上的Primetime (Flash Player)，一律使用 `Local` 金鑰傳遞，即使 `Remote` 已指定。
