---
title: 字彙表
description: 需要特殊定義的常用詞語。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 字彙表 {#glossary}

需要特殊定義的常用詞語。

## 內容加密金鑰 {#content-encryption-key}

公用程式產生的內容加密金鑰(CEK)隨後由內容封裝程式用來準備必須受保護的內容。
公用程式會產生16個位元組的十六進位金鑰。
本指南在註記和錯誤訊息、檔案和命令範例中顯示CEK的引數名稱和值名稱的下列變體：

* 內容金鑰
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

CEK的檔案名稱如下所示：

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

CEK本身可儲存在金鑰管理系統中並加密。 本指南將儲存索引稱為CEK儲存ID CEKSID。 金鑰加密金鑰(KEK)一詞指的是第二層級加密金鑰，而金鑰則是 `ek` 是指該加密的值。
有些呼叫同時使用CEK和CEK儲存ID CEKSID，而且從儲存擷取的CEK必須符合呼叫中提供的CEK。
對於含FairPlay的HLS離線，也有 `persistentContentKey` ，可設定為過期。

## 內容加密金鑰儲存ID {#content-encryption-key-storage-id}

內容加密金鑰儲存ID (CEKSID)是從金鑰管理系統擷取內容加密金鑰的ID。

CEKSID也稱為
* 金鑰ID
* 內容ID
* `&kid`

## 客戶驗證者 {#customer-authenticator}

在對Expressplay API的請求中進行驗證的金鑰。 要求中可包含權杖要求。
