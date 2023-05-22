---
title: 辭彙表
description: 需要特殊定義的常用術語。
exl-id: 4e7874f7-c5c0-4f2c-ada2-a0da3ed4d4bf
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 辭彙表 {#glossary}

需要特殊定義的常用術語。

## 內容加密密鑰 {#content-encryption-key}

由實用程式生成的內容加密密鑰(CEK)隨後被內容打包器用於準備必須保護的內容。
該實用程式以十六進位形式生成長度為16位元組的密鑰。
本指南在注釋和錯誤消息、檔案和命令示例中顯示CEK的參數名稱和值名稱的以下變型：

* 內容密鑰
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

CEK的檔案名顯示為：

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

CEK本身可以儲存在密鑰管理系統中並且被加密。 本指南將儲存索引稱為CEK儲存ID CEKSID。 密鑰加密密鑰(KEK)一詞是指二級加密密鑰，該術語 `ek` 指該加密的值。
某些調用同時使用CEK和CEK儲存ID CEKSID，並且從儲存中檢索到的CEK必須與調用中提供的CEK匹配。
對於HLS Offline with FairPlay，還有 `persistentContentKey` 可設定為過期。

## 內容加密密鑰儲存ID {#content-encryption-key-storage-id}

內容加密密鑰儲存ID(CEKSID)是用於從密鑰管理系統檢索內容加密密鑰的ID。

CEKSID也稱為
* 密鑰ID
* 內容ID
* `&kid`

## 客戶驗證器 {#customer-authenticator}

用於對Expressplay的API請求進行身份驗證的密鑰。 請求可以包括令牌請求。
