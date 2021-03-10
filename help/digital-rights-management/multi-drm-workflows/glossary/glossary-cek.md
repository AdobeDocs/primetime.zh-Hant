---
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# 辭彙表{#glossary}

需要特殊定義的常用詞語。

## 內容加密密鑰{#content-encryption-key}

內容加密密鑰(CEK)由實用程式生成，隨後由內容包裝商在準備必須保護的內容時使用。
該實用程式以十六進位形式生成密鑰，長度為16個位元組。
本指南在注釋和錯誤消息、檔案和命令示例中顯示了CEK的參數名稱和值名稱的以下變型：

* 內容索引
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

CEK的檔案名稱如下所示：

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

CEK本身可以儲存在密鑰管理系統中，也可以加密。 本指南將儲存索引稱為CEK儲存ID CEKSID。 密鑰加密密鑰(KEK)一詞指二級加密密鑰，而`ek`一詞指該加密的值。
有些呼叫會同時使用CEK和CEK儲存ID CEKSID，而從儲存擷取的CEK必須符合呼叫中提供的CEK。
對於具有FairPlay的HLS Offline，還有`persistentContentKey`可設為過期。

## 內容加密密鑰儲存ID {#content-encryption-key-storage-id}

內容加密密鑰儲存ID(CEKSID)是用於從密鑰管理系統檢索內容加密密鑰的ID。

CEKSID也稱為
* 金鑰ID
* 內容ID
* `&kid`

## 客戶驗證器{#customer-authenticator}

Expressplay API請求中的驗證金鑰。 請求可包含Token請求。