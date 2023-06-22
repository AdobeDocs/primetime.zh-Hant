---
title: 錯誤報告
description: 錯誤報告
exl-id: a52bd2cf-c712-40a2-a25e-7d9560b46ba6
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2961'
ht-degree: 1%

---

# 錯誤報告 {#error-reporting}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。


## 概觀 {#overview}

Adobe Primetime驗證中的錯誤報告目前以兩種不同的方式實作：

* **進階錯誤報告** 若發生以下情況，實作人員會註冊錯誤回呼： [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk) 或實作名為&#39;&#39;的介面方法`status`&quot;若是 [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk) 和 [AccessEnabler Android SDK](#accessenabler-android-sdk)，以接收進階錯誤報告。 錯誤會分類為 **資訊**， **警告**、和 **錯誤** 型別。 此報告系統是 **非同步**，在此 **無法保證觸發多個錯誤的順序**.  如需進階錯誤報告系統的詳細資訊，請參閱 [進階錯誤報告](#advanced-error-reporting) 區段。

* **原始錯誤報告 —** 一種靜態報告系統，當特定請求失敗時，錯誤訊息會傳遞至特定的回呼函式。 錯誤會分組為通用、驗證和授權型別。 如需在原始系統中報告的錯誤清單，請參閱 [原始錯誤報告](#original-error-reporting) 區段。


## 進階錯誤報告 {#advanced-error-reporting}

* [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk)
* [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk)
* [AccessEnabler Android SDK](#accessenabler-android-sdk)
* [AccessEnabler FireOS SDK](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>舊的 [原始錯誤報告](#original-error-reporting) API會繼續像之前一樣運作，進階錯誤報告不會破壞功能，但原始錯誤報告將不再收到任何更新。 所有新的錯誤和更新都會發生在進階錯誤報告系統中。

### AccessEnabler JavaScript SDK {#accessenabler-javascript-sdk}

新的錯誤報告系統保留為選擇性，因此實作人員可以明確註冊錯誤處理常式回呼，以接收進階錯誤報告。 此系統包含動態註冊和取消註冊多個錯誤回呼的功能。 此外，一旦AccessEnabler JavaScript SDK載入，您就可以註冊任何新的錯誤回呼，而不需要執行任何其他初始化（在呼叫之前） `setRequestor()`)，這表示您可以接收有關初始化和設定錯誤的進階報告。


#### 實作 {#access-enab-js-imp}

yourErrorHandler(errorData：Object)


您的錯誤處理常式回呼函式將接收單一物件（對應），其結構如下：

```JavaScript
    {
      errorId: "CFG410",
      level: "error",
      message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

### 1.繫結 {#bind}

**`.bind(eventType:String, handlerName:String):void`**

附加事件的處理常式。

**`eventType`**  — 僅限&quot;`errorEvent`「值會導致AccessEnabler JavaScript SDK觸發進階錯誤報告回呼。

**`handlerName`**  — 指定錯誤處理常式函式名稱的字串。\
 

兩個繫結引數都必須只使用下列集合中的字元： `[0-9a-zA-Z][-._a-zA-Z0-9]`；也就是說，引數必須以數字或字母開頭，然後只能包含連字型大小、句號、底線和英數字元。  此外，引數不能超過1024個字元。  

**範例** 的繫結錯誤處理常式：

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

由於技術限制，您無法繫結關閉或匿名函式。 您必須在第二個引數中指定方法的名稱。

 
### 2.解除繫結 {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

移除先前附加的事件處理常式。

**`eventType`**  — 僅&#39;`errorEvent`&#39;值會導致AccessEnabler JavaScript SDK觸發進階錯誤報告回呼。

**`handlerName`**  — 指定錯誤處理常式函式名稱的字串（如果為null或遺失指定之所有附加的處理常式） `eventType` 將被移除。

兩個繫結引數都必須只使用下列集合中的字元： `[0-9a-zA-Z][-._a-zA-Z0-9]`；也就是說，引數必須以數字或字母開頭，然後只能包含連字型大小、句號、底線和英數字元。  此外，引數不能超過1024個字元。  

**範例** 移除單一錯誤處理常式時：

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**範例** 移除所有錯誤處理常式：

`accessEnabler.unbind('errorEvent');`


### AccessEnabler iOS/tvOS SDK {#accessenabler-ios-tvos-sdk}

新的錯誤報告系統是強制性的，因此實作人員必須明確遵循新的Objective C「EntitlementStatus」通訊協定。 此新方法可讓程式設計師接收進階錯誤報告。

#### 實作 {#accessenab-ios-tvossdk-imp}

實作人員必須符合下列條件 **EntitlementStatus** 通訊協定：

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

您的 **狀態** 函式將接收單一物件(一個 `NSDictionary`)的屬性具有下列結構：

```OBJ-C
    {
          errorId: "CFG410",
          level: "error",
          message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

**1. 宣告**

```OBJ-C
    @interface MyEntitlementStatusDelegate : NSObject <EntitlementStatus>
```

**2. 實作**

```OBJ-C
    @implementation DemoAppAppDelegate     
    // very simple implementation
    - (void)status:(NSDictionary *)statusDict {
        NSLog(@"%@:\n%@", statusDict[@"level"], statusDict);
    }
```


### AccessEnabler Android SDK {#accessenabler-android-sdk}

新的錯誤報告系統是強制性的，因為實作人員必須明確遵守 `IAccessEnablerDelegate` 介面定義的通訊協定。 此新方法可讓程式設計師接收進階錯誤報告。

#### 實作 {#access-enablr-androidsdk-imp}

實作人員需要處理新的 `status` 來自介面的方法`IAccessEnablerDelegate`. 此 **`status`** 函式將收到單一 **`AdvancedStatus`** 具有下列模型的物件：

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**範例**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

### AccessEnabler FireOS SDK {#accessenabler-fireos-sdk}


新的錯誤報告系統是強制性的，因為實作人員必須明確遵守 `IAccessEnablerDelegate` 介面定義的通訊協定。 此新方法可讓程式設計師接收進階錯誤報告。

#### 實作 {#access-enab-fireos-sdk-}

實作人員需要處理新的 `status`來自介面的方法`IAccessEnablerDelegate`. 此 **`status`** 函式將收到單一 **`AdvancedStatus`** 具有下列模型的物件：

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**範例**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

## 進階錯誤代碼參考 {#advanced-error-codes-reference}

下表列出並描述較新的錯誤API所公開的錯誤代碼，以及更正這些錯誤的建議動作：

| ID | 層級 | 說明 | 開發人員動作 | 使用者動作 | JavaScript | iOS/tvOS | Android |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL和AAPL_ERROR | 錯誤 | 一般Apple SSO錯誤 | 錯誤包含具有原始VSA錯誤的詳細資料欄位。 | 不適用 | 不適用 | 是 | 不適用 |
| VSA203 | 資訊 | 使用者決定登出應用程式，而驗證發生於透過平台SSO登入的結果。 | 指示/提示使用者從tvOS上的[設定] -> [帳戶] -> [電視提供者]明確登出。 <br><br> 指示/提示使用者明確登出iOS/iPadOS上的「設定 — >電視提供者」。 | 明確地從tvOS上的[設定] -> [帳戶] -> [電視提供者]登出。 <br> <br> 明確登出iOS/iPadOS上的「設定 — >電視提供者」 | 不適用 | 是 | 不適用 |
| VSA404 | 資訊 | 應用程式視訊訂閱者帳戶許可權未確定。 | 說明單一登入(SSO)使用者體驗的優點，以鼓勵拒絕授予存取訂閱資訊許可權的使用者。 | 使用者可以變更其決定，方法是前往應用程式設定（電視提供者存取），或前往iOS/iPadOS上的「設定 — >電視提供者」或tvOS上的「設定 — >帳戶 — >電視提供者」區段。 | 不適用 | 是 | 不適用 |
| VSA503 | 資訊 | 應用程式視訊訂閱者帳戶中繼資料要求失敗。 | MVPD端點沒有回應。 應用程式可退回至一般驗證流程。 | 不適用 | 不適用 | 是 | 不適用 |
| 500 | 錯誤 | 內部錯誤 | 使用AccessEnablerDebug和檢查偵錯記錄（console.log輸出）來判斷哪裡出了問題。 | 不適用 | 是 | 是 | 不適用 |
| SEC403 | 錯誤 | 網域安全性錯誤。 請求者使用無效的網域。 特定請求者ID使用的所有網域都必須依Adobe列入白名單。 |  — 僅從允許的網域清單載入AccessEnabler <br> <br>  — 聯絡Adobe以管理所使用請求者ID的網域白名單 <br> <br> - iOS：確認您使用正確的憑證，且簽章已正確建立 | 不適用 | 不適用 | 是 | 不適用 |
| SEC412 | 警告 | [ 第2.5發行版本提供 ] 裝置ID不相符。 每當基礎平台變更其裝置ID時，就可能發生這種情況。 在此情況下，現有的Token將會清除，且使用者將不再獲得驗證。 請注意，當使用者使用JS SDK且漫遊（在JS上，使用者端IP是裝置ID的一部分）時，就會合法地發生此狀況。 否則，這可能表示有人嘗試詐騙，即有人嘗試從其他裝置複製Token。 |  — 監視警告數目。 如果流量尖峰沒有明顯的原因（沒有近期的瀏覽器更新；新的作業系統），這可能表示有人企圖詐騙。  <br> <br> — 選擇性地通知使用者他需要再次登入。 | 再次登入。 | 是 | 是 | 是（從3.2） |
| SEC420 | 錯誤 | 與Adobe Primetime驗證伺服器通訊時出現HTTP安全性錯誤。 此錯誤通常會在假冒/代理程式就位時發生。 |  — 載入 `[https://]{SP_FQDN\}` 並手動接受SSL憑證，例如 **https://api.auth.adobe.com** 或 **https://api.auth-staging.adobe.com** <br> <br> — 將Proxy憑證標示為受信任 | 如果這發生在一般使用者身上，則表示可能是中間人攻擊！ | 是 | 是 | 是（從3.2） |
| CFG100 | 警告 | 使用者端電腦日期/時間/時區未正確設定。 這可能會導致驗證/授權錯誤。 |  — 通知使用者設定正確的時間。 <br> <br> 採取行動來避免權益流程，因為這些流程可能會失敗。 | 設定正確的日期/時間。 | 是 | 是 | 是（從3.2） |
| CFG400 | 錯誤 | 提供了無效的請求者ID。 | 開發人員必須指定有效的請求者ID。 | 不適用 | 是 | 是 | 是（從3.2） |
| CFG404 | 錯誤 | 找不到Adobe Primetime驗證伺服器。 這可能在3個例項中發生： <br><br>  — 開發人員已設定無效的偽造。 <br><br>  — 使用者發生網路問題，無法連線Adobe Primetime驗證網域。 <br><br> -Adobe Primetime驗證伺服器設定錯誤。 <br><br>  **注意：** 在Firefox上，將會顯示CFG400，而不是CFG404 （瀏覽器限制） |  — 檢查偽造。 <br><br>  — 檢查網路/DNS設定。 <br><br>  — 通知Adobe。 | 檢查網路/DNS設定。 | 是 | 是 | 是（從3.2） |
| CFG410 | 錯誤 | AccessEnabler太舊。 | 通知使用者清除快取。 | 清除瀏覽器快取。 | 是 | 不適用 | 是（從3.2） |
| CFG5xx | 錯誤 | Adobe Primetime驗證伺服器發生內部錯誤。 xx可以是任何數字。 |  — 通知使用者Adobe Primetime驗證無法使用。 <br><br>  — 略過Adobe Primetime驗證。 <br> <br>  — 通知Adobe。 | 請稍後再試。 | 是 | 是 | 是（從3.2） |
| N000 | 資訊 | 使用者未驗證。 | 不適用 | 登入。 | 是 | 是 | 是（從3.2） |
| N001 | 資訊 | 已在背景啟動被動驗證嘗試。 這將會發生在設定為「每個請求者的驗證」的MVPD上。 雖然使用者有望自動驗證，但這會在初始化時造成效能損失。 | 選擇性地通知使用者或顯示UI提醒使用者「工作進行中」。 | 等一下。 | 是 | 是 | 是（從3.2） |
| N003 | 資訊 | 使用者從Apple MVPD選擇器中選取「其他電視提供者」選項。 | 此 *displayProviderDialog* 將會呼叫callback，而應用程式可以回覆成一般的驗證流程。 | 選取一般MVPD並繼續登入畫面。 | 不適用 | 是 | 不適用 |
| N004 | 資訊 | 使用者會選取目前要求者不支援的電視提供者。 | 此 *displayProviderDialog* 將會呼叫callback，而應用程式可以回覆成一般的驗證流程。 | 選取一般MVPD並繼續登入畫面。 | 不適用 | 是 | 不適用 |
| N005 | 資訊 | MVPD選擇器已取消。 | 不適用 | 不適用 | 是 | 是 | 是（從3.2） |
| N010 | 警告 | 在為所選MVPD設定全部驗證降級規則時，使用者已驗證。 | 選擇性地告知使用者，由於MVPD問題，他獲得「免費」的免費存取權。 | 不適用 | 是 | 是 | 是（從3.2） |
| N011 | 資訊 | 已使用TempPass驗證使用者。 |  — 通知使用者。 <br> <br>  — 可選擇提供一般MVPD的清單。 | 您可以選擇使用一般MVPD登入。 | 是 | 是 | 是（從3.2） |
| N111 | 警告 | 過期的TempPass |  — 通知使用者。 <br> <br>  — 提供一般MVPD的清單。 <br> <br>  — 隱藏TempPass選項 | 使用一般MVPD登入。 | 是 | 是 | 是（從3.2） |
| N130 | 錯誤 | **在工作階段中找不到驗證權杖。**  這可能是由於下列其中一個原因所造成： <br> <br> 1. 瀏覽器已停用（第三方） Cookie （不適用於AccessEnabler JavaScript SDK 4.x版） <br> <br> 2. 瀏覽器已啟用「防止跨網站追蹤」 (Safari 11+) <br> <br> 3. 工作階段已過期 <br> <br> 4. 程式設計師呼叫驗證API的順序不正確 <br> <br> 注意：此錯誤碼不適用於整頁重新導向驗證流程。 | 1.提示使用者啟用（第三方） Cookie <br> <br> 2. 提示使用者停用跨網站追蹤 <br> <br> 3. 提示使用者重新驗證 <br> <br> 4. 以正確順序呼叫API | 1.啟用（第三方） Cookie <br> <br> 2. 停用跨網站追蹤 <br> <br> 3. 重新驗證 <br> <br> 4. 不適用 | 是 | 是 | 是（從3.2） |
| N500 | 錯誤 | 內部錯誤。 <br> <br> 注意：這是原始錯誤系統的「一般驗證錯誤」和「內部驗證錯誤」。 此錯誤最終將被淘汰。 | 使用AccessEnablerDebug和檢查偵錯記錄（console.log輸出）來判斷哪裡出了問題。 | 不適用 | 是 | 是 | 不適用 |
| R401 | 錯誤 | 嘗試取得存取權杖時發生錯誤。 <br> <br> 注意：這是無法復原的錯誤。 通知使用者應用程式無法使用。 | - iOS：檢查應用程式中的軟體陳述式和自訂配置。 <br> <br> - JavaScript：檢查網站應用程式中的軟體陳述式。 <br> <br> 使用Zendesk開啟票證，並通知使用者系統暫時無法使用 | 不適用 | 是（從v4.0） | 是（從v3.0） | 是（從3.2） |
| R400 | 錯誤 | 應用程式未註冊。 軟體陳述式無效或已撤銷。 <br> <br> 注意：這是無法復原的錯誤。 通知使用者應用程式無法使用。 | - iOS：檢查應用程式中的軟體陳述式和自訂配置。 <br> <br> - JavaScript：檢查網站應用程式中的軟體陳述式。 <br> <br> 使用Zendesk開啟票證，並通知使用者系統暫時無法使用 | 不適用 | 是（從v4.0） | 是（從v3.0） | 是（從3.2） |
| REG500 | 錯誤 | 無法從伺服器擷取註冊代碼。 <br> <br> 注意：這是無法復原的錯誤。 通知使用者應用程式無法使用。 | 使用Zendesk開啟票證，並通知使用者系統暫時無法使用。 | 不適用 | 是（從v4.0） | 是（從v3.0） | 是（從3.2） |
| REGCODE | 成功 | tvOS平台上名為setSelectedProvider API的應用程式。 | 指示/提示使用者使用第二部裝置（熒幕）登入，並使用提供的註冊代碼。 | 在第2部裝置（熒幕）上使用regcode來起始驗證。 | 不適用 | 是，僅適用於tvOS | 不適用 |
| Z010 | 警告 | 在為選定的MVPD實施「全部驗證」或「全部授權」降級規則時，使用者已獲得授權。 | 選擇性地告知使用者，由於MVPD問題，他獲得「免費」的免費存取權。 | 不適用 | 是 | 是 | 是（從3.2） |
| Z011 | 資訊 | 已使用TempPass授權使用者 | 選擇性地通知使用者 | 不適用 | 是 | 是 | 是（從3.2） |
| Z100 | 錯誤 | 授權失敗，因為使用者沒有訂閱要求的資源，或是其他源自MVPD的原因，例如視訊不符合使用者帳戶的家長監護設定 |  — 不允許播放。 <br> <br>  — 通知使用者。 <br> <br>  — 錯誤訊息中的&#39;message&#39;索引鍵可能包含MVPD提供的更詳細訊息。 | 不適用 | 是 | 是 | 是（從3.2） |
| Z110 | 錯誤 | 由於重複的MVPD拒絕，授權被拒絕。 可能的詐騙企圖或DOS。 |  — 不允許播放。 <br> <br>  — 通知使用者。 | 不適用 | 是 | 是 | 是（從3.2） |
| Z120 | 錯誤 | 由於與MVPD通訊的技術原因，拒絕授權。 可能的網路錯誤。 |  — 不允許播放。 <br> <br>  — 通知使用者MVPD發生問題，他們應該稍後再試。 | 請稍後再試。 | 是 | 是 | 是（從3.2） |
| Z130 | 錯誤 | 授權被拒絕，因為使用了無效/格式錯誤的資源。 | 檢查資源字串並加以更正。 一般而言，此錯誤是由於MRSS格式錯誤或使用純字串而非MRSS所造成。 | 不適用 | 是 | 是 | 是（從3.2） |
| Z169 | 錯誤 | 授權被拒絕，因為authzNone降級規則已套用到指定的資源。 | 通知使用者 | 不適用 | 是 | 是 | 是（從3.2） |
| Z500 | 錯誤 | 內部錯誤。 <br> <br>  注意：這是舊版「一般驗證錯誤」和「內部驗證錯誤」。 此錯誤最終將被淘汰。 | 使用AccessEnablerDebug和檢查偵錯記錄（console.log輸出）來判斷哪裡出了問題。 | 不適用 | 是 | 是 | 是（從3.2） |
| P100 | 錯誤 | 預先授權失敗。 這很可能是因為請求對太多資源的授權。 |  — 請勿使用超過允許的最大資源數。 <br> <br>  — 聯絡Adobe Primetime驗證支援以尋找/設定允許的最大資源數量。 | 不適用 | 是（從v3.0） | 是 | 是（從3.2） |
| IS2XX | 錯誤 | 當個人化伺服器端點回應資料的格式無效或缺少必要的個人化資訊時，會傳回這些錯誤代碼。 | 使用Zendesk開啟票證，並通知使用者系統暫時無法使用 | 不適用 | 是（從v3.0） | 不適用 | 不適用 |
| IS4XX | 錯誤 | 若個別化伺服器端點失敗4XX — 是回應的HTTP狀態碼，則會傳回這些錯誤代碼。 | 使用Zendesk開啟票證，並通知使用者系統暫時無法使用 | 不適用 | 是（從v3.0） | 不適用 | 不適用 |
| IS5XX | 錯誤 | 若個別化伺服器端點失敗5XX — 是回應的HTTP狀態碼，則會傳回這些錯誤代碼。 | 使用Zendesk開啟票證，並通知使用者系統暫時無法使用 | 不適用 | 是（從v3.0） | 不適用 | 不適用 |
| IS0 | 錯誤 | 當個人化伺服器端點完全沒有回應，因此連線已逾時時，會傳回此程式碼 | 使用Zendesk開啟票證，並通知使用者系統暫時無法使用 | 不適用 | 是（從v3.0） | 不適用 | 不適用 |
| LS011 | 警告 | 由於LSO / LocalStorage問題和WebStorage問題（或無法使用），AccessEnabler使用不穩定的儲存體。 <br> <br> 驗證/授權不會持續存在超過目前頁面！ 每次頁面載入都會導致使用者需要驗證。 頁面重新載入時不會強制執行已設定的TTL。 |  — 通知使用者限制。 <br> <br>  — 告知使用者如何增加可用儲存空間。 <br> <br>  — 或是登出以清除儲存空間。 |  — 增加儲存空間。 <br> <br>  — 登出以清除儲存空間。 | 是 | 不適用 | 不適用 |

<br>

## 原始錯誤報告 {#original-error-reporting}

本節說明原始的錯誤報告系統，以及原始的錯誤代碼。 在原始錯誤報告系統中，AccessEnabler會將錯誤傳遞給這兩個回呼函式： `setAuthenticationStatus()` 在呼叫之後 `checkAuthentication()`； `tokenRequestFailed()`，在對的呼叫失敗後 `checkAuthorization()` 或 `getAuthorization()`.

原始錯誤報告和狀態API會繼續像之前一樣運作。 不過，日後不會更新原始的錯誤報告API。 舊錯誤的所有新錯誤報告和更新都將只反映在新版 [進階錯誤報告系統](#advanced-error-reporting).


如需使用原始錯誤報告系統的範例，請參閱 [JavaScript API參考](/help/authentication/javascript-sdk-api-reference.md)：[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) 和 [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) 函式， [iOS/tvOS API參考](/help/authentication/iostvos-sdk-api-reference.md)： [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)和 [tokentRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed)， [Android API參考](/help/authentication/android-sdk-api-reference.md)： [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) 和 [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### 原始回呼錯誤代碼 {#original-callback-error-codes}

| **一般錯誤** |  |
|---|---|
| 內部錯誤 | 嘗試處理請求時發生系統錯誤。 |
| 未選取提供者錯誤 | 當客戶在提供者選擇對話方塊中取消時發生。 |
| 無法使用提供者錯誤 | 當沒有可用的提供者時發生。 |
|  |  |
| **驗證錯誤** |  |
| 一般驗證錯誤 | 原因不明或無法發佈時傳回。 |
| 內部驗證錯誤 | 嘗試驗證時發生系統錯誤。 |
| 使用者未驗證錯誤 | 使用者未驗證。 |
|  |  |
| **授權錯誤** |  |
| 一般授權錯誤 | 原因不明或無法發佈時傳回。 |
| 內部授權錯誤 | 嘗試授權時發生系統錯誤。 |
| 使用者未授權錯誤 | 客戶無權檢視要求的內容。 |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->
