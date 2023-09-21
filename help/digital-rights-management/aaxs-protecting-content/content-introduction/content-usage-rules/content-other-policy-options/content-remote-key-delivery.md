---
title: 遠端和本機iOS金鑰傳送
description: 遠端和本機iOS金鑰傳送
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 遠端和本機iOS金鑰傳送{#remote-and-local-ios-key-delivery}

Adobe Primetime支援兩種將金鑰傳送至iOS使用者端的選項：

* 遠端 — M3U8資訊清單指定的HTTPS路徑包含AES金鑰，應該用來解密資料流中的下列加密區段，與HLS規格中的指定完全相同。 指定「遠端」時，使用者端裝置會連線至遠端HTTPS伺服器以擷取AES金鑰。
* 本機 — 指定「本機」時，本機HTTPS伺服器會內嵌至iOS應用程式，以處理所有AES金鑰要求，而非透過網際網路/網路連線AES金鑰。 內嵌HTTPS伺服器會在Primetime應用程式中自動設定和設定。 應用程式開發人員不需要介入。

透過用於封裝內容的原則啟用遠端金鑰傳遞（變更此設定需要重新封裝內容）。啟用遠端金鑰傳遞時，必須部署Adobe存取金鑰伺服器以處理來自iOS使用者端的金鑰請求，但其他平台的使用者端的工作流程不會變更。

>[!NOTE]
>
>金鑰傳遞選擇只會影響iOS使用者端。 所有使用HLS內容的其他裝置將一律使用「本機」金鑰傳遞，即使已指定「遠端」亦然。

如需詳細資訊，請參閱 *使用Adobe存取金鑰伺服器*.
