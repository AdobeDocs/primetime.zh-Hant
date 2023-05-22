---
title: 在準年前設定環境和測試
description: 在準年前設定環境和測試
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 在準年前設定環境和測試{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

本技術說明的目的是幫助我們的合作夥伴建立其環境，並開始測試部署在Adobe資格預審環境上的新構建。

因為有兩種構造風格： ***生產*** 和 ***暫存***，在本文檔中，我們將重點介紹生產設定，其中提到所有步驟對於登台是相同的，只有URL不同。

步驟1和2在其中一台測試機上設定test環境，步驟3是基本流程的驗證，步驟4和5提供一些測試指南。

>[!IMPORTANT]
>
> 每次要更改測試環境時（從轉儲到生產配置檔案或以其他方式切換），執行步驟1和2非常重要
 

## 步驟1. 將域解析為IP {#resolving-pass-domain-to-an-ip}

* 要查找可用於欺騙的負載平衡器IP，請運行以下命令：

* **在Windows上**

   ```cmd
   C:\>nslookup sp-prequal.auth.adobe.com
   ...
   Addresses:  52.13.71.11
               54.184.208.150
   ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **在Linux/Mac**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE]
>
>由於域不相關且可能因用戶而異，因此從應答中排除。

>[!IMPORTANT]
>
> 這些IP地址將來可能會發生變化，並且可能不同地理區域的用戶不會相同。


## 步驟2.  誘使資格預審環境成為生產環境 {#spoofing-the-prequalification-environment}

* 編輯 *c:\\windows\\System32\\drivers\\etc\\hosts* 檔案（在Windows中）或 */etc/hosts* 檔案（在Macintosh/Linux/Android上），並添加以下內容：

* 假離線生產配置檔案
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Android上的欺騙：** 要假裝在Android上，你必須使用Android模擬器。

* 一旦假冒就位，您只需將常規URL用於生產和登台配置檔案：(即， `http://sp.auth-staging.adobe.com` 和 `http://entitlement.auth-staging.adobe.com` 你會撞到 *資格預審環境/生產* *新版本。


## 步驟3.  驗證您指向的環境是否正確 {#Verify-you-are-pointing-to-the-right-environment}

**這是一個簡單的步驟：**

* 負荷 [權利概論環境](https://entitlement-prequal.auth.adobe.com/environment.html) 和 [權利](https://entitlement.auth.adobe.com/environment.html)。 他們應該回答同樣的問題。


## 步驟4。  使用程式設計師網站執行簡單的驗證/授權流 {#peform-a-simple-auth-flow}

* 此步驟需要程式設計師的網址和一些有效的MVPD憑據（已對其進行身份驗證和授權的用戶）。

## 步驟5.  使用程式設計師網站執行方案測試 {#perform-scenario-testing-using-programmer-website}

* 完成環境設定並確保基本的身份驗證授權流正常運行後，您可以繼續測試更複雜的方案。


## 步驟6.  使用APItest站點執行測試 {#perform-testing-using-api-testing-site}

* 如果您想更深入地測試Adobe Primetime身份驗證，我們建議您使用 [APItest站點](http://entitlement-prequal.auth.adobe.com/apitest/api.html)。

有關APItest站點的詳細資訊，請訪問 [如何使用Adobe的APItest站點test驗證和授權流](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md)。
