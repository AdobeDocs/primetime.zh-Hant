---
title: 在準年前設定您的環境和測試
description: 在準年前設定您的環境和測試
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# 在準年前設定您的環境和測試{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

此技術說明的目的是協助我們的合作夥伴設定其環境，並開始測試部署在Adobe資格預審環境上的新組建。

因為有兩種建置風格： ***生產*** 和 ***中繼***，在本檔案中，我們將著重於生產設定，其中提及測試的所有步驟相同，只有URL不同。

步驟1和2在其中一台測試機上建立測試環境，步驟3是基本流程的驗證，步驟4和5演示一些測試指南。

>[!IMPORTANT]
>
> 每次您要變更測試環境時（從測試環境切換至生產設定檔或以其他方式切換），務必執行步驟1和2
 

## 步驟1. 解析將域傳遞到IP {#resolving-pass-domain-to-an-ip}

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
>由於網域不相關，因此無法從答案中排除，且可能會因使用者而異。

>[!IMPORTANT]
>
> 這些IP位址未來可能會有所變更，而且對於不同地理位置的使用者而言，可能會有所不同。


## 步驟2.  假造要生產的資格預審環境 {#spoofing-the-prequalification-environment}

* 編輯 *c:\\windows\\System32\\drivers\\etc\\hosts* 檔案（在Windows中）或 */etc/hosts* 檔案（在Macintosh/Linux/Android上），並新增下列內容：

* 假設生產配置檔案
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**在Android上欺騙：** 若要在Android上假設，您必須使用Android模擬器。

* 假冒一旦就緒，您只需為生產和測試設定檔使用一般URL即可：(即， `http://sp.auth-staging.adobe.com` 和 `http://entitlement.auth-staging.adobe.com` 而你會撞到 *資格預審環境/生產* *新版本。


## 步驟3.  驗證您指向的環境是否正確 {#Verify-you-are-pointing-to-the-right-environment}

**這是一個簡單的步驟：**

* 載入 [權利優先環境](https://entitlement-prequal.auth.adobe.com/environment.html) 和 [權利](https://entitlement.auth.adobe.com/environment.html). 他們應傳回相同的回應。


## 步驟4.  使用程式設計師的網站執行簡單的驗證/授權流程 {#peform-a-simple-auth-flow}

* 此步驟要求程式設計師的網站地址和一些有效的MVPD憑證（已驗證和授權的用戶）。

## 步驟5.  使用程式設計師的網站執行方案測試 {#perform-scenario-testing-using-programmer-website}

* 完成環境設定並確保基本的驗證授權流程正常運行後，您可以繼續測試更複雜的情況。


## 步驟6.  使用API測試網站執行測試 {#perform-testing-using-api-testing-site}

* 如果您想要更深入地測試Adobe Primetime驗證，建議您使用 [API測試網站](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

如需API測試網站的詳細資訊，請前往 [如何使用Adobe的API測試網站來測試驗證和授權流程](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

