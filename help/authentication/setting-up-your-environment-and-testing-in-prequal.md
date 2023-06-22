---
title: 在預備中設定您的環境和測試
description: 在預備中設定您的環境和測試
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 在預備中設定您的環境和測試{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

本技術說明旨在協助我們的合作夥伴設定其環境，並開始測試部署在Adobe資格預審環境上的新組建。

由於有兩種建置風格： ***生產*** 和 ***分段***，在本檔案中，我們將專注於生產設定，並提及測試的所有步驟相同，只有URL不同。

步驟1和2是在其中一台測試機器上設定測試環境，步驟3是驗證基本流程，而步驟4和5呈現一些測試准則。

>[!IMPORTANT]
>
> 每當您想要變更測試環境（從測試環境切換至生產設定檔或反之）時，請務必執行步驟1和2
 

## 步驟1. 正在將傳遞網域解析為IP {#resolving-pass-domain-to-an-ip}

* 若要尋找可用於欺騙的負載平衡器IP，請執行以下命令：

* **在Windows上**

   ```cmd
   C:\>nslookup sp-prequal.auth.adobe.com
   ...
   Addresses:  52.13.71.11
               54.184.208.150
   ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **在Linux/Mac上**

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
>網域因不相關且可能因使用者而異，所以無法回答。

>[!IMPORTANT]
>
> 這些IP位址在未來可能會變更，而且對於不同地理區域的使用者而言，這些IP位址可能不同。


## 步驟2.  將資格預審環境偽裝成生產環境 {#spoofing-the-prequalification-environment}

* 編輯 *c：\\windows\\System32\\drivers\\etc\\hosts* 檔案（在Windows中）或 */etc/hosts* 檔案（在Macintosh/Linux/Android上）並新增下列專案：

* 偽造生產設定檔
   * 52.13.71.11 http://entitlement.auth.adobe.com， http://sp.auth.adobe.com， http://api.auth.adobe.com

**在Android上欺騙：** 若要在Android上進行欺騙，您必須使用Android模擬器。

* 一旦設定好詐騙罪名，您就可以將一般URL用於生產和測試設定檔： (也就是說， `http://sp.auth-staging.adobe.com` 和 `http://entitlement.auth-staging.adobe.com` 而且您實際上會點選 *資格預審環境/生產* 新版本編號的。


## 步驟3.  確認您指向正確的環境 {#Verify-you-are-pointing-to-the-right-environment}

**這是一個簡單的步驟：**

* 載入 [權利前置環境](https://entitlement-prequal.auth.adobe.com/environment.html) 和 [權利](https://entitlement.auth.adobe.com/environment.html). 他們應該會傳回相同的回應。


## 步驟4.  使用程式設計師的網站執行簡單的驗證/授權流程 {#peform-a-simple-auth-flow}

* 此步驟需要程式設計師的網站位址和一些有效的MVPD認證（已驗證和授權的使用者）。

## 步驟5.  使用程式設計人員的網站執行案例測試 {#perform-scenario-testing-using-programmer-website}

* 完成環境設定並確保基本驗證授權流程正常運作後，您可以繼續測試更複雜的情境。


## 步驟6.  使用API測試網站執行測試 {#perform-testing-using-api-testing-site}

* 如果您想更深入探究測試Adobe Primetime驗證，建議您使用 [API測試網站](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

您可以在API測試網站找到更多詳細資料 [如何使用Adobe的API測試網站測試驗證和授權流程](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).
