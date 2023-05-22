---
title: 無客戶端API實施 — 錯誤代碼/可能原因/原因的消息
description: 無客戶端API實施 — 錯誤代碼/可能原因/原因的消息
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 無客戶端API實施 — 錯誤代碼/可能原因/原因的消息 {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>


## 錯誤：未授權

### 原因：

1. POST中缺少授權標頭
1. 授權標頭問題 — 檢查請求時間是否以毫秒為單位。

## 錯誤：SC 400驗證期間

### 原因：

1. 伺服器找不到為特定請求者和環境建立的註冊代碼。
1. 您可能正在遇到跨域指令碼問題
1. 應將正確的欺騙添加到/etc/hosts檔案

## 錯誤：400錯誤請求

### 原因：

1. POST/GET的URL格式不正確
1. SAMLAssertionParserException — 在Adobe末尾無法解密加密的SAML斷言

## 錯誤： 403已禁止

### 原因：

1. 請求太多 — API管理的一個功能，可防止DoS攻擊。
2. 如果使用預先環境，則添加欺騙，否則請確保已從/etc/hosts檔案中刪除欺騙

## 錯誤：無法登錄到MVPD頁

### 原因：

1. 用戶名和密碼不匹配 
2. 登錄名可能已禁用
3. 檢查登錄是否用於生產或暫存


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
