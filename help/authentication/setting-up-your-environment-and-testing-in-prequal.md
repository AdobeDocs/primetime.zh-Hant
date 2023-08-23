---
title: 在預備中設定您的環境及測試
description: 在預備中設定您的環境及測試
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 在預先 Qual 設定您的環境和測試{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>此頁面的內容僅供參考。 使用此 API 需要 Adobe Systems 的目前授權。 不允許未授權的使用。

此技術說明的目的是説明我們的合作夥伴設定其環境，並開始測試在 Adobe Systems 預先資格的環境上部署的新版本編號。

由於有兩種版本編號口味： ***生產*** 和 ***測試*** ，因此，在此檔中，我們將專注的生產設定中，請注意，只有 url 不同。

步驟1和2是在其中一個測試電腦上設定測試環境，步驟3是驗證基本流量，步驟 4 &amp; 5 則說明了一些測試準則。

>[!IMPORTANT]
>
> 每次想要變更測試環境時，請務必執行步驟1和2（從測試設定檔或其他方式中切換）


## 步驟1. 將傳遞網域解析為IP {#resolving-pass-domain-to-an-ip}

* 若要尋找可用於欺騙的負載平衡器IP，請執行以下命令：

* **在Windows上**

  ```cmd
  C:\>nslookup sp-prequal.auth.adobe.com
  ...
  Addresses:  52.13.71.11
              54.184.208.150
  ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **在 Linux/Mac 上**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE]
>
>從回答中排除的網域不相關，且可能因用戶與用戶不同。

>[!IMPORTANT]
>
> 這些 IP 位址將來可能會變更，且不同地理區域中的使用者可能不會使用相同。


## 步驟2。  哄騙準備環境進行生產 {#spoofing-the-prequalification-environment}

* *編輯 c:\\windows\\System32\\drivers\\etc\\hosts* 檔案（在 windows 中）或 */etc/hosts* 檔案（在 Macintosh/Linux/Android 上）並新增下列專案：

* 假冒生產設定檔
   * 52.13.71.11 http://entitlement.auth.adobe.com、http://sp.auth.adobe.com、http://api.auth.adobe.com

**在Android上詐騙：** 若要在Android上詐騙，您必須使用Android模擬器。

* 一旦設定好詐騙功能，您就可以將一般URL用於生產和測試設定檔： (也就是說， `http://sp.auth-staging.adobe.com` 和 `http://entitlement.auth-staging.adobe.com` 而且您實際上會點選 *資格預審環境/生產* 的URL。


## 步驟3.  確認您指向正確的環境 {#Verify-you-are-pointing-to-the-right-environment}

**這是一個簡單的步驟：**

* 載入 [ 權利 prequal 環境 ](https://entitlement-prequal.auth.adobe.com/environment.html) 和 [ 權利 ](https://entitlement.auth.adobe.com/environment.html) 。 他們應該傳回相同的回應。


## 步驟4。  使用程式師的網站執行簡單驗證/授權流量 {#peform-a-simple-auth-flow}

* 此步驟需要程式師網站位址和一些有效的 MVPD 憑證（經過驗證和授權的用戶）。

## 步驟5。  使用程式師的網站執行案例測試 {#perform-scenario-testing-using-programmer-website}

* 完成環境設定並確保基本驗證授權流程運作後，您可以繼續測試更複雜的案例。


## 步驟6.  使用API測試網站執行測試 {#perform-testing-using-api-testing-site}

* 如果您想更深入探究測試Adobe Primetime驗證，建議您使用 [API測試網站](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

您可以在API測試網站找到更多詳細資料 [如何使用Adobe的API測試網站測試驗證和授權流程](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).
