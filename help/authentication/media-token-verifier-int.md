---
title: 整合媒體令牌驗證器
description: 整合媒體令牌驗證器
exl-id: 1688889a-2e30-4d66-96ff-1ddf4b287f68
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# 整合媒體令牌驗證器

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 關於媒體令牌驗證器 {#about-media-token-verifier}

授權成功後，Adobe Primetime身份驗證將建立長期授權(AuthZ)令牌。  AuthZ令牌會傳遞到客戶端或儲存在伺服器端，具體取決於客戶端的平台。  (請參閱 [瞭解令牌](/help/authentication/programmer-overview.md#understanding-tokens) 關於令牌如何儲存在不同客戶端系統上，以及其他詳細資訊。)


AuthZ令牌授權站點用戶查看給定資源。  它的典型生存時間(TTL)為6到24小時，在此之後令牌將過期。 **對於實際查看訪問，黃金時段身份驗證使用AuthZ令牌生成您獲取的短時間媒體令牌，並將其傳遞到媒體伺服器**。 這些短壽命媒體令牌的TTL非常短（通常為幾分鐘）。


在AccessEnabler整合中，通過 `setToken()` 回叫。 對於無客戶端API整合，您可以使用 `<SP_FQDN>/api/v1/tokens/media` API調用。 令牌是使用基於PKI（公鑰基礎架構）的令牌保護以明文發送的字串，由Adobe簽名。 在基於PKI的這種保護下，令牌使用非對稱密鑰簽名，由認證機構頒發給Adobe。


由於客戶端上沒有驗證令牌，因此惡意用戶可以使用工具來注入假 `setToken()` 呼叫。 所以你 **不能** 只是依靠一個事實 `setToken()` 觸發，當考慮用戶是否已授權時。 您必須驗證短期令牌本身是否合法。 執行驗證的工具是介質令牌驗證器庫。


>[!TIP]
>
>必須將返回的令牌字串的整個長度傳遞給媒體令牌驗證器進行驗證。

## 使用媒體令牌驗證器驗證短期令牌 {#validate-short-livedttokens}

我們建議程式設計師將令牌發送到使用媒體令牌驗證器庫的Web服務，以便在實際啟動視頻流之前驗證令牌。 短壽命媒體令牌的極短TTL被定義為足夠長，以允許在生成令牌的伺服器和驗證令牌的伺服器之間發生時鐘同步問題，但不再。



的 [媒體令牌驗證器庫](https://adobeprimetime.zendesk.com/auth/v2/login/signin?return_to=https%3A%2F%2Ftve.zendesk.com%2Fhc%2Fen-us%2Farticles%2F204963159-Media-Token-Verifier-library&amp;theme=hc&amp;locale=en-us&amp;brand_id=343429&amp;auth_origin=343429%2Cfalse%2Ctrue){target=_blank} 可供Mighine驗證合作夥伴使用。



媒體令牌驗證器庫包含在Java存檔檔案中 `mediatoken-verifier-VERSION.jar`。 庫定義：

* 令牌驗證API(`ITokenVerifier` 介面)，帶JavaDoc文檔
* 用於驗證令牌是否確實來自Adobe的Adobe公鑰
* 參考實現(`com.adobe.entitlement.test.EntitlementVerifierTest.java`)，顯示如何使用Verifier API以及如何使用庫中包含的Adobe公鑰驗證其源


存檔包含所有依賴項和證書密鑰庫。 包含的證書密鑰庫的預設口令是「123456」。

* 驗證庫需要JDK 1.5版或更高版本。
* 使用您首選的JCE提供程式來使用簽名算法「SHA256WithRSA」。


**驗證器庫必須是用於分析令牌內容的唯一方法。 程式設計師不應分析令牌並自行提取資料，因為令牌格式不受保證，並且受將來更改的影響。** 只有Verifier API才能正確運行。 直接分析字串可能會暫時起作用，但在格式可能更改時，將來會出現問題。 驗證器API從令牌中檢索資訊，如：

* 令牌是否有效( `isValid()` 方法)?
* 資源ID與令牌( `getResourceID()` 方法);可以將此參數與 `setToken()` 函式回調。 如果不匹配，則可能表示欺詐行為。
* 發出令牌的時間(`getTimeIssued()` )。
* TTL(`getTimeToLive()` )。
* 從MVPD(M)接收的匿名認證GUID`getUserSessionGUID()` )。
* 對用戶進行身份驗證的分發伺服器的ID（如果是） — 為分發伺服器提供身份驗證的proxy-MVPD。

## 使用驗證器API {#using-verifier-api}

的 `ITokenVerifier` 類定義用於驗證給定資源的令牌真實性的方法。 使用 `ITokenVerifier` 分析響應於 `setToken()` 請求。


的 `isValid()` 方法是驗證令牌的主要方法。 它需要一個參數，即資源ID。 如果傳遞空資源ID，則該方法僅驗證令牌真實性和有效期。


的 `isValid()` 方法返回以下狀態值之一：



| 有效標籤 | 所有驗證都成功 |
|--------------------|-----------------------------------------|
| INVALID_TOKEN_FORMAT | 令牌格式無效 |
| 無效簽名 | 無法驗證令牌真實性 |
| 令牌(_E) | 令牌TTL無效 |
| INVALID_RESOURCE_ID | 令牌對給定資源無效 |
| 錯誤_未知 | 尚未驗證令牌 |

其他方法提供對給定令牌的資源ID、發出的時間和生存時間的特定訪問。

* 使用 `getResourceID()` 檢索與令牌關聯的資源ID，並將其與從setToken()請求返回的ID進行比較。
* 使用 `getTimeIssued()` 以檢索令牌發出的時間。
* 使用 `getTimeToLive()` 以檢索TTL。
* 使用 `getUserSessionGUID()` 檢索由MVPD設定的匿名GUID。
* 使用 `getMvpdId()` 以檢索已驗證用戶的MVPD的ID。
* 使用 `getProxyMvpdId()` 以檢索已驗證用戶的代理MVPD的ID。

## 示例代碼 {#sample-code}

媒體令牌驗證器存檔包含引用實現(`com.adobe.entitlement.test.EntitlementVerifierTest.java`)和使用test類調用API的示例。 此示例(`com.adobe.entitlement.text.EntitlementVerifierTest.java`)說明了令牌驗證庫與媒體伺服器的整合。


```Java
package com.adobe.entitlement.test; 
import com.adobe.entitlement.verifier.CryptoDataHolder;
import com.adobe.entitlement.verifier.ITokenVerifier;
import com.adobe.entitlement.verifier.ITokenVerifierFactory;
import com.adobe.entitlement.verifier.SimpleTokenPKISignatureVerifierFactory;
import com.adobe.tve.crypto.SignatureVerificationCredential; 
import java.io.InputStream; 

public class EntitlementVerifierTest { 
    String mRequestorID = null;
    String mTokenToVerify = null;
    String mPathToCertificate = null;
    String mKeystoreType = null;
    String mKeystorePasswd = null;
    String mResourceID = null;

    public static void main(String[] args) { 
        if (args == null || args.length < 2 ) {
            System.out.println("Incorrect args: Usage: EntitlementVerifierTest requestorID tokenToVerify [resourceID]");
            return;
        } 
        String requestorID = args[0];
        String tokenToVerify = args[1];
        String pathToCertificate = "media_token_keystore.jks"; // the default keystore provided in the entitlement jar 
        String keystoreType = "jks";
        String keystorePasswd = "123456"; // password for the default keystore 
        if (requestorID == null || tokenToVerify == null) {
            System.out.println("One or more arguments is null");
            return;
        } 
        System.out.println("RequestorID: " + requestorID);
        System.out.println("token: " + tokenToVerify);
        System.out.println("cert: " + pathToCertificate);
        System.out.println("keystoretype: " + keystoreType);
        System.out.println("keystore passwd: " + keystorePasswd);
        String resourceID = null;
        if (args.length > 2) {
            resourceID = args[2];
        }
        System.out.println("Resource ID: " + resourceID);
        EntitlementVerifierTest verifier = new EntitlementVerifierTest(requestorID,
            tokenToVerify, pathToCertificate, keystoreType, keystorePasswd, resourceID);
        verifier.verifyToken();
    } 

    protected EntitlementVerifierTest(String inRequestorID,
                                      String inTokenToVerify,
                                      String inPathToCertificate,
                                      String inKeystoreType,
                                      String inKeystorePasswd, String inResourceID) {
        mRequestorID = inRequestorID;
        mTokenToVerify = inTokenToVerify;
        mPathToCertificate = inPathToCertificate;
        mKeystoreType = inKeystoreType;
        mKeystorePasswd = inKeystorePasswd;
        mResourceID = inResourceID;
    } 

    protected void verifyToken() {
        // It is expected that the SignatureVerificationCredential and 
        // CryptoDataHolder could be created at Init time in a web application 
        // and be reused for all token verifications. 
        CryptoDataHolder cryptoData = createCryptoDataHolder(mPathToCertificate, mKeystoreType, mKeystorePasswd);
        ITokenVerifierFactory tokenVerifierFactory = new SimpleTokenPKISignatureVerifierFactory();
        ITokenVerifier tokenVerifier = tokenVerifierFactory.getInstance(mRequestorID, mTokenToVerify, cryptoData);
        ITokenVerifier.eReturnValue status = tokenVerifier.isValid(mResourceID);
        System.out.println("Is token Valid? : " + status.toString());
        System.out.println("Token User ID: " + tokenVerifier.getUserSessionGUID());
        System.out.println("Token was generated at: " + tokenVerifier.getTimeIssued());

        System.out.println("Token Mvpd ID: " + tokenVerifier.getMvpdId());
        System.out.println("Token Proxy Mvpd ID: " + tokenVerifier.getProxyMvpdId());
    } 
    protected CryptoDataHolder createCryptoDataHolder(String pathToCertificate,
                                                      String keystoreType, String keystorePasswd) {
        SignatureVerificationCredential verificationCredential =
            readShortTokenVerificationCredential(pathToCertificate, keystoreType, keystorePasswd);
        CryptoDataHolder cryptoData = new CryptoDataHolder();
        cryptoData.setCertificateInfo(verificationCredential);
        return cryptoData;
    } 
    protected SignatureVerificationCredential readShortTokenVerificationCredential(String keystoreFile,
                                                                                   String keystoreType,
                                                                                   String keystorePasswd) {
        SignatureVerificationCredential cred = null; 
        if (keystoreFile != null){
            try {
                // load the keystore file 
                ClassLoader loader = EntitlementVerifierTest.class.getClassLoader();
                InputStream certInputStream =  loader.getResourceAsStream(keystoreFile);
                if (certInputStream != null) {
                    cred = new SignatureVerificationCredential(certInputStream, keystorePasswd, keystoreType);          
                }
            }
            catch (Exception e) {
                System.out.println("Error creating short token server credentials: " + e.getMessage());
            }
        }
        if (cred == null) {
            System.out.println("Error creating short token server credentials");
        } 
        return cred;
    } 
}
```
