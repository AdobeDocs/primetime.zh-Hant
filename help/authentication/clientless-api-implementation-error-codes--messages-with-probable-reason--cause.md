---
title: 無用戶端API實作 — 錯誤碼/可能原因/原因的訊息
description: 無用戶端API實作 — 錯誤碼/可能原因/原因的訊息
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 無用戶端API實作 — 錯誤碼/可能原因/原因的訊息 {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>


## 錯誤：未授權

### 原因：

1. POST中缺少授權標頭
1. 授權標頭問題 — 檢查請求時間是否以毫秒為單位。

## 錯誤：驗證期間SC 400

### 原因：

1. 伺服器找不到為特定請求者和環境建立的註冊代碼。
1. 您可能遇到跨網域指令碼問題
1. /etc/hosts檔案中應新增正確的欺騙

## 錯誤：400個錯誤請求

### 原因：

1. POST/GET的URL格式錯誤
1. SAMLAssertionParserException — 在Adobe的結尾處無法解密加密的SAML斷言

## 錯誤： 403 Forbidden

### 原因：

1. 請求太多 — API管理功能，可防止DoS攻擊。
2. 如果使用預先環境，則添加欺騙，否則請確保已從/etc/hosts檔案中刪除欺騙

## 錯誤：無法登入MVPD頁面

### 原因：

1. 用戶名和密碼不匹配 
2. 登錄可能已禁用
3. 檢查登入是否用於生產或測試


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->