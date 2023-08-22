---
title: Clientless API 實施-具有可能原因/原因的錯誤代碼/訊息
description: Clientless API 實施-具有可能原因/原因的錯誤代碼/訊息
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Clientless API 實施-具有可能原因/原因的錯誤代碼/訊息 {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>此頁面的內容僅供參考。 使用此 API 需要 Adobe Systems 的目前授權。 不允許未經授權的使用。

</br>


## 錯誤：未授權

### 原因：

1. POST 中遺失授權標題
1. 授權標題問題-檢查請求時間是否以毫秒為單位。

## 錯誤：驗證期間的 SC 400

### 原因：

1. 伺服器找不到為特定要求者和環境建立的註冊代碼。
1. 您可以執行跨網域指令碼問題
1. 應將適當的哄騙新增至/etc/hosts 檔案

## 錯誤：400錯誤請求

### 原因：

1. POST/GET 的 url 格式錯誤
1. SAMLAssertionParserException –無法在 Adobe Systems 的結尾解密加密的 SAML 斷言

## 錯誤：403禁止

### 原因：

1. 快速請求太多-這是 API 管理的一項功能，可防止 DoS 攻擊。
2. 如果使用 prequal 環境然後增加哄騙，請確保已從/etc/hosts 檔案中移除哄騙

## 錯誤：無法登入至 MVPD 頁面

### 原因：

1. 使用者名稱和密碼不符
2. 登入可能已停用
3. 檢查登入是用於生產或測試


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
