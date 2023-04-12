---
title: 整合媒體代號驗證器
description: 整合媒體代號驗證器
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# 整合媒體代號驗證器

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 關於媒體代號驗證器 {#about-media-token-verifier}

授權成功時，Adobe Primetime驗證會建立長期授權(AuthZ)代號。  AuthZ代號會傳遞至用戶端，或儲存在伺服器端，端視用戶端的平台而定。  (請參閱 [了解Token](/help/authentication/programmer-overview.md#understanding-tokens) 關於如何在不同的用戶端系統上儲存代號，以及其他詳細資訊。)


AuthZ代號可授權網站的使用者檢視指定資源。  通常存留時間(TTL)為6到24小時，代號便會過期。 **對於實際的檢視存取，Primetime驗證會使用AuthZ代號來產生您所取得的短期媒體代號，並傳遞至您的媒體伺服器**. 這些短暫的媒體代號的TTL很短（通常需幾分鐘）。


在AccessEnabler整合中，您可通過 `setToken()` 回呼。 若是無用戶端API整合，您可透過 `<SP_FQDN>/api/v1/tokens/media` API呼叫。 令牌是以明文發送的字串，由Adobe簽名，使用基於PKI（公鑰基礎設施）的令牌保護。 通過基於PKI的保護，令牌使用非對稱密鑰簽名，由認證機構發給Adobe。


由於客戶端上沒有對令牌進行驗證，因此惡意用戶可以使用工具插入假 `setToken()` 呼叫。 因此，您 **不能** 僅僅依賴於 `setToken()` 會在考量使用者是否獲授權時觸發。 您必須驗證短期代號本身是否合法。 執行驗證的工具是媒體代號驗證程式庫。


>[!TIP]
>
>您必須將傳回的Token字串的整個長度傳遞至媒體Token驗證器以進行驗證。

## 使用媒體代號驗證器驗證短期代號 {#validate-short-livedttokens}

建議程式設計人員將代號傳送至使用媒體代號驗證程式庫的網站服務，以便在實際啟動視訊資料流之前驗證代號。 短期媒體權杖的極短TTL被定義為足夠長，以允許產生權杖的伺服器和驗證權杖的伺服器之間出現時鐘同步問題，但是不再。



此 [媒體令牌驗證程式庫](https://adobeprimetime.zendesk.com/auth/v2/login/signin?return_to=https%3A%2F%2Ftve.zendesk.com%2Fhc%2Fen-us%2Farticles%2F204963159-Media-Token-Verifier-library&amp;theme=hc&amp;locale=en-us&amp;brand_id=343429&amp;auth_origin=343429%2Cfalse%2Ctrue){target=_blank} 適用於Primetime驗證合作夥伴。



Java歸檔檔案中包含媒體令牌驗證程式庫 `mediatoken-verifier-VERSION.jar`. 程式庫會定義：

* 代號驗證API(`ITokenVerifier` 介面)，搭配JavaDoc檔案
* 用來驗證代號是否確實來自Adobe的Adobe公開金鑰
* 參考實作(`com.adobe.entitlement.test.EntitlementVerifierTest.java`)，說明如何使用驗證程式API，以及如何使用程式庫中包含的Adobe公開金鑰來驗證其來源


封存包含所有相依性和憑證金鑰存放區。 包含的憑證金鑰存放區的預設密碼為「123456」。

* 驗證庫需要JDK 1.5版或更高版本。
* 請使用您慣用的JCE提供程式來使用簽名算法「SHA256WithRSA」。


**驗證程式庫必須是分析令牌內容的唯一方法。 程式設計師不應分析令牌並提取資料本身，因為令牌格式不受保證，並且可能會在未來發生更改。** 只有驗證程式API才能正常運作。 直接剖析字串可能會暫時運作，但在格式可能變更時，將來會造成問題。 驗證器API會從Token中擷取資訊，例如：

* 代號有效( `isValid()` 方法)?
* 系結至代號的資源ID( `getResourceID()` 方法);這可以與（而且應該符合） `setToken()` 函式回呼。 如果不符合，這可能表示欺詐行為。
* 發出代號的時間(`getTimeIssued()` 方法)。
* TTL(`getTimeToLive()` 方法)。
* 從MVPD(`getUserSessionGUID()` 方法)。
* 驗證使用者的經銷商ID（若是如此） — 為經銷商提供驗證的代理MVPD。

## 使用驗證程式API {#using-verifier-api}

此 `ITokenVerifier` 類定義了用於驗證給定資源的令牌真實性的方法。 使用 `ITokenVerifier` 分析響應於 `setToken()` 請求。


此 `isValid()` 方法是驗證Token的主要方式。 需要一個引數，即資源ID。 如果您傳遞Null資源ID，方法只會驗證Token真實性和有效期。


此 `isValid()` 方法會傳回下列其中一個狀態值：



| VALID_TOKEN | 所有驗證均成功 |
|--------------------|-----------------------------------------|
| INVALID_TOKEN_FORMAT | 令牌格式無效 |
| INVALID_SIGNATURE | 無法驗證令牌真實性 |
| TOKEN_EXPIRED | 令牌TTL無效 |
| INVALID_RESOURCE_ID | 令牌對給定資源無效 |
| ERROR_UNKNOWN | 尚未驗證令牌 |

其他方法可提供特定資源ID、核發時間，以及指定Token的存留時間。

* 使用 `getResourceID()` 擷取與Token相關聯的資源ID，並將其與從setToken()請求傳回的ID進行比較。
* 使用 `getTimeIssued()` 以擷取發出代號的時間。
* 使用 `getTimeToLive()` 來擷取TTL。
* 使用 `getUserSessionGUID()` 擷取MVPD設定的匿名GUID。
* 使用 `getMvpdId()` 擷取已驗證使用者的MVPD ID。
* 使用 `getProxyMvpdId()` 擷取已驗證使用者的Proxy MVPD ID。

## 程式碼範例 {#sample-code}

媒體代號驗證器封存包含參考實作(`com.adobe.entitlement.test.EntitlementVerifierTest.java`)和使用測試類別叫用API的範例。 此範例(`com.adobe.entitlement.text.EntitlementVerifierTest.java`)說明代號驗證程式庫整合至媒體伺服器。


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
