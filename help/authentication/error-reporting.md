---
title: 錯誤報告
description: 錯誤報告
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2961'
ht-degree: 1%

---

# 錯誤報告 {#error-reporting}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


## 概述 {#overview}

Adobe Primetime驗證中的錯誤報告目前是以兩種不同的方式實作：

* **進階錯誤報告** 實施者會註冊錯誤回呼，以防 [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk) 或實現名為「`status`」 [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk) 和 [AccessEnabler Android SDK](#accessenabler-android-sdk)，以接收進階錯誤報告。 錯誤分類為 **資訊**, **警告**，和 **錯誤** 類型。 此報告系統為 **非同步**，在 **無法保證觸發多個錯誤的順序**.  有關高級錯誤報告系統的詳細資訊，請參見 [進階錯誤報告](#advanced-error-reporting) 區段。

* **原始錯誤報告 —** 一種靜態報表系統，當特定請求失敗時，會將錯誤訊息傳遞至特定回呼函式。 錯誤會分為一般、驗證和授權類型。 有關在原始系統中報告的錯誤清單，請參見 [原始錯誤報告](#original-error-reporting) 區段。


## 進階錯誤報告 {#advanced-error-reporting}

* [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk)
* [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk)
* [AccessEnabler Android SDK](#accessenabler-android-sdk)
* [AccessEnabler FireOS SDK](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>舊 [原始錯誤報告](#original-error-reporting) API將繼續如往常般運作，進階錯誤報表不會中斷功能，但原始錯誤報表將不會再收到任何更新。 進階錯誤報告系統會發生所有新錯誤和更新。

### AccessEnabler JavaScript SDK {#accessenabler-javascript-sdk}

新的錯誤報告系統仍為可選，因此，實施者可明確註冊錯誤處理程式回呼以接收進階錯誤報告。 該系統包括動態註冊和註銷多個錯誤回呼的能力。 此外，您可以在載入AccessEnabler JavaScript SDK時立即註冊任何新的錯誤回呼，而無需執行任何其他初始化（在呼叫之前） `setRequestor()`)，表示您可以接收有關初始化和設定錯誤的進階報告。


#### 實作 {#access-enab-js-imp}

yourErrorHandler(errorData:Object)


錯誤處理程式回呼函式將接收具有下列結構的單一物件（地圖）:

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

### 1.綁定 {#bind}

**`.bind(eventType:String, handlerName:String):void`**

為事件附加處理程式。

**`eventType`**  — 僅「`errorEvent`&quot;值會導致AccessEnabler JavaScript SDK觸發進階錯誤報告回呼。

**`handlerName`**  — 指定錯誤處理程式函式名稱的字串。\
 

兩個綁定參數只能使用以下集中的字元： `[0-9a-zA-Z][-._a-zA-Z0-9]`;也就是說，參數必須以數字或字母開頭，然後只能包含連字型大小、句號、底線和英數字元。  此外，參數不能超過1024個字元。  

**範例** 綁定錯誤處理程式：

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

由於技術限制，您無法綁定閉包或匿名函式。 您必須在第二個參數中指定方法的名稱。

 
### 2.解除綁定 {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

移除先前附加的事件處理常式。

**`eventType`**  — 僅「`errorEvent`&#39;值會導致AccessEnabler JavaScript SDK觸發進階錯誤報表回呼。

**`handlerName`**  — 指定錯誤處理程式函式名稱的字串，如果為null或缺少指定的所有附加處理程式 `eventType` 即會移除。

兩個綁定參數只能使用以下集中的字元： `[0-9a-zA-Z][-._a-zA-Z0-9]`;也就是說，參數必須以數字或字母開頭，然後只能包含連字型大小、句號、底線和英數字元。  此外，參數不能超過1024個字元。  

**範例** 刪除單個錯誤處理程式：

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**範例** 刪除所有錯誤處理程式：

`accessEnabler.unbind('errorEvent');`


### AccessEnabler iOS/tvOS SDK {#accessenabler-ios-tvos-sdk}

新的錯誤報告系統是強制性的，因此實施者必須明確符合新的Objective C &quot;EntitlementStatus&quot;協定。 這種新方法使程式設計師能夠接收高級錯誤報告。

#### 實作 {#accessenab-ios-tvossdk-imp}

實施者必須符合下列條件 **EntitlementStatus** 協定：

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

您的 **狀態** 函式將接收單一物件( `NSDictionary`)，且具有下列結構：

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

**1. 聲明**

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

新的錯誤報告系統是強制性的，因為實施者必須明確符合 `IAccessEnablerDelegate` 介面定義的協定。 這種新方法使程式設計師能夠接收高級錯誤報告。

#### 實作 {#access-enablr-androidsdk-imp}

實施者需要處理 `status` 介面中的方法`IAccessEnablerDelegate`. 此 **`status`** 函式會收到單一 **`AdvancedStatus`** 物件具有以下模型：

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


新的錯誤報告系統是強制性的，因為實施者必須明確符合 `IAccessEnablerDelegate` 介面定義的協定。 這種新方法使程式設計師能夠接收高級錯誤報告。

#### 實作 {#access-enab-fireos-sdk-}

實施者需要處理 `status`介面中的方法`IAccessEnablerDelegate`. 此 **`status`** 函式會收到單一 **`AdvancedStatus`** 物件具有以下模型：

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

## 高級錯誤代碼參考 {#advanced-error-codes-reference}

下表列出並說明較新錯誤API公開的錯誤碼，以及要採取的修正動作：

| ID | 層級 | 說明 | 開發人員動作 | 使用者動作 | JavaScript | iOS/tvOS | Android |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL&amp;AAPL_ERROR | 錯誤 | 一般Apple SSO錯誤 | 錯誤包含含原始VSA錯誤的詳細資訊欄位。 | n/a | n/a | 是 | n/a |
| VSA203 | 資訊 | 當驗證因透過平台SSO登入而發生時，使用者決定登出應用程式。 | 指示/提示使用者從tvOS上的「設定 — >帳戶 — >電視提供者」明確登出。 <br><br> 指示/提示使用者從iOS/iPadOS上的「設定 — >電視提供者」明確登出。 | 從tvOS上的「設定」 — >「帳戶」 — >「電視提供者」明確登出。 <br> <br> 從iOS/iPadOS上的「設定 — >電視提供者」明確登出 | n/a | 是 | n/a |
| VSA404 | 資訊 | 應用程式視頻訂閱者帳戶權限未確定。 | 說明單一登入(SSO)使用者體驗的優點，以鼓勵拒絕授予存取訂閱資訊權限的使用者。 | 使用者可以前往應用程式設定（電視提供者存取權），或前往iOS/iPadOS上的「設定 — >電視提供者」或「設定 — >帳戶 — >tvOS上的電視提供者」區段，以變更其決策。 | n/a | 是 | n/a |
| VSA503 | 資訊 | 應用程式視頻訂閱者帳戶元資料請求失敗。 | MVPD端點沒有回應。 應用程式可能會回復到一般驗證流程。 | n/a | n/a | 是 | n/a |
| 500 | 錯誤 | 內部錯誤 | 使用AccessEnablerDebug並檢查調試日誌（console.log輸出）以確定出錯的原因。 | n/a | 是 | 是 | n/a |
| SEC403 | 錯誤 | 域安全錯誤。 請求者使用無效的網域。 特定請求者ID使用的所有網域都需加入白名單Adobe。 |  — 僅從允許的域清單中載入AccessEnabler <br> <br>  — 連絡Adobe，以管理所使用請求者ID的網域白名單 <br> <br> - iOS:確認您使用的憑證正確無誤，且簽名已正確建立 | n/a | n/a | 是 | n/a |
| SEC412 | 警告 | [ 在2.5版中提供 ] 設備ID不匹配。 每當基礎平台變更其裝置ID時，就會發生此情況。 在此情況下，將會清除現有代號，且使用者將不再進行驗證。 請注意，當使用者使用JS SDK且正在漫遊時（在JS上，用戶端IP屬於裝置ID的一部分），就會合法地發生此情況。 否則，這可能表示欺詐企圖，即嘗試從不同裝置複製代號。 |  — 監視警告數。 如果尖峰是無明顯原因(最近沒有瀏覽器更新；新作業系統)，可能是欺詐企圖的指標。  <br> <br> — （可選）通知用戶他需要重新登錄。 | 再次登入。 | 是 | 是 | 是，從3.2 |
| SEC420 | 錯誤 | 與Adobe Primetime驗證伺服器通訊時發生HTTP安全性錯誤。 當假造/代理就緒時，通常會發生此錯誤。 |  — 載入 `[https://]{SP_FQDN\}` 並手動接受SSL憑證，例如 **https://api.auth.adobe.com** 或 **https://api.auth-staging.adobe.com** <br> <br> — 將代理證書標籤為受信任 | 如果這對普通用戶來說，則表明可能是中間人攻擊！ | 是 | 是 | 是，從3.2 |
| CFG100 | 警告 | 客戶端電腦「日期/時間/時區」設定不正確。 這可能會導致驗證/授權錯誤。 |  — 通知用戶設定正確的時間。 <br> <br> 採取措施防止福利流，因為它們很可能會失敗。 | 設定正確的日期/時間。 | 是 | 是 | 是，從3.2 |
| CFG400 | 錯誤 | 提供的請求者ID無效。 | 開發人員必須指定有效的請求者ID。 | n/a | 是 | 是 | 是，從3.2 |
| CFG404 | 錯誤 | 找不到Adobe Primetime驗證伺服器。 這可能會發生在3種情況： <br><br>  — 開發人員已設定無效的欺騙。 <br><br>  — 使用者有網路問題，無法存取Adobe Primetime驗證網域。 <br><br> -Adobe Primetime驗證伺服器配置錯誤。 <br><br>  **注意：** 在Firefox上，會顯示CFG400，而非CFG404（瀏覽器限制） |  — 檢查欺騙。 <br><br>  — 檢查網路/DNS設定。 <br><br>  — 通知Adobe。 | 檢查網路/ DNS設定。 | 是 | 是 | 是，從3.2 |
| CFG410 | 錯誤 | AccessEnabler太舊。 | 通知用戶清除快取。 | 清除瀏覽器快取。 | 是 | n/a | 是，從3.2 |
| CFG5xx | 錯誤 | Adobe Primetime驗證伺服器發生內部錯誤。 xx可以是任何數字。 |  — 通知使用者Adobe Primetime驗證無法使用。 <br><br>  — 略過Adobe Primetime驗證。 <br> <br>  — 通知Adobe。 | 請稍後再試。 | 是 | 是 | 是，從3.2 |
| N000 | 資訊 | 未驗證用戶。 | n/a | 登入。 | 是 | 是 | 是，從3.2 |
| N001 | 資訊 | 已在後台啟動被動身份驗證嘗試。 以「每個要求者驗證」設定的MVPD會發生此情況。 雖然希望使用者能自動驗證，但這會在初始化時造成效能損失。 | （可選）通知使用者或提供UI，提醒使用者「工作正在進行中」。 | 等等。 | 是 | 是 | 是，從3.2 |
| N003 | 資訊 | 使用者從Apple MVPD選擇器中選取「其他電視提供者」選項。 | 此 *displayProviderDialog* 將呼叫回呼，而應用程式可回退至一般驗證流程。 | 選取一般MVPD並繼續登入畫面。 | n/a | 是 | n/a |
| N004 | 資訊 | 用戶選擇當前請求者不支援的電視提供者。 | 此 *displayProviderDialog* 將呼叫回呼，而應用程式可回退至一般驗證流程。 | 選取一般MVPD並繼續登入畫面。 | n/a | 是 | n/a |
| N005 | 資訊 | 已取消MVPD選擇器。 | n/a | n/a | 是 | 是 | 是，從3.2 |
| N010 | 警告 | 在為所選MVPD設定「驗證全部」降級規則時，已驗證用戶。 | （可選）通知使用者，他因MVPD困難而獲得「免費」免費存取。 | n/a | 是 | 是 | 是，從3.2 |
| N011 | 資訊 | 使用者已使用TempPass進行驗證。 |  — 通知使用者。 <br> <br>  — （可選）提供一般MVPD的清單。 | （可選）使用一般MVPD登入。 | 是 | 是 | 是，從3.2 |
| N111 | 警告 | 過期的TempPass。 |  — 通知用戶。 <br> <br>  — 提供一般MVPD的清單。 <br> <br>  — 隱藏TempPass選項。 | 使用一般MVPD登入。 | 是 | 是 | 是，從3.2 |
| N130 | 錯誤 | **在會話中找不到身份驗證令牌。**  這可能是因為下列其中一項原因： <br> <br> 1. 瀏覽器已停用（第三方）Cookie（不適用於AccessEnabler JavaScript SDK 4.x版） <br> <br> 2. 瀏覽器已啟用「防止跨網站追蹤」（Safari 11以上版本） <br> <br> 3. 會話已過期 <br> <br> 4. 程式設計師以錯誤的連續調用驗證API <br> <br> 注意：此錯誤代碼不適用於全頁重新導向驗證流程。 | 1.提示使用者啟用（第三方）Cookie <br> <br> 2. 建議使用者停用跨網站追蹤 <br> <br> 3. 提示用戶重新驗證 <br> <br> 4. 以正確順序呼叫API | 1.啟用（第三方）Cookie <br> <br> 2. 停用跨網站追蹤 <br> <br> 3. 重新驗證 <br> <br> 4. 不適用 | 是 | 是 | 是，從3.2 |
| N500 | 錯誤 | 內部錯誤。 <br> <br> 注意：這是原始錯誤系統的「一般驗證錯誤」和「內部驗證錯誤」。 這個錯誤最終會淘汰。 | 使用AccessEnablerDebug並檢查調試日誌（console.log輸出）以確定出錯的原因。 | n/a | 是 | 是 | n/a |
| R401 | 錯誤 | 嘗試獲取訪問令牌時出錯。 <br> <br> 注意：這是無法復原的錯誤。 通知用戶應用程式不可用。 | - iOS:檢查應用程式中的軟體語句和自定義配置。 <br> <br> - JavaScript:檢查網站應用程式中的軟體語句。 <br> <br> 使用Zendesk開啟票證，並通知用戶系統暫時不可用 | n/a | 是從v4.0 | 是從v3.0 | 是，從3.2 |
| R400 | 錯誤 | 未註冊應用程式。 軟體語句無效或已被撤銷。 <br> <br> 注意：這是無法復原的錯誤。 通知用戶應用程式不可用。 | - iOS:檢查應用程式中的軟體語句和自定義配置。 <br> <br> - JavaScript:檢查網站應用程式中的軟體語句。 <br> <br> 使用Zendesk開啟票證，並通知用戶系統暫時不可用 | n/a | 是從v4.0 | 是從v3.0 | 是，從3.2 |
| REG500 | 錯誤 | 無法從伺服器中獲取註冊代碼。 <br> <br> 注意：這是無法復原的錯誤。 通知用戶應用程式不可用。 | 使用Zendesk開啟票證，並通知用戶系統暫時不可用。 | n/a | 是從v4.0 | 是從v3.0 | 是，從3.2 |
| REGCODE | 成功 | tvOS平台上名為setSelectedProvider API的應用程式。 | 指示/提示使用者使用第2個裝置（畫面），使用提供的註冊代碼登入。 | 使用第2個裝置（螢幕）上的regcode來起始驗證。 | n/a | 僅適用於tvOS | n/a |
| Z010 | 警告 | 在選定MVPD的「驗證全部」或「授權全部」降級規則已定位時，用戶被授權。 | （可選）通知使用者，他因MVPD困難而獲得「免費」免費存取。 | n/a | 是 | 是 | 是，從3.2 |
| Z011 | 資訊 | 使用者已透過TempPass取得授權 | （可選）通知用戶 | n/a | 是 | 是 | 是，從3.2 |
| Z100 | 錯誤 | 授權失敗，因為使用者沒有訂閱請求的資源，或由於其他原因（例如，視訊不符合使用者帳戶的家長控制設定） |  — 不允許播放。 <br> <br>  — 通知使用者。 <br> <br>  — 錯誤消息中的「message」鍵MVPD可能包含MVPD提供的更詳細的消息。 | n/a | 是 | 是 | 是，從3.2 |
| Z110 | 錯誤 | 由於重複的MVPD拒絕，授權被拒絕。 可能的欺詐企圖或DOS。 |  — 不允許播放。 <br> <br>  — 通知使用者。 | n/a | 是 | 是 | 是，從3.2 |
| Z120 | 錯誤 | 由於與MVPD通訊的技術原因而拒絕授權。 可能的網路錯誤。 |  — 不允許播放。 <br> <br>  — 通知用戶MVPD遇到了困難，他們應稍後嘗試。 | 請稍後再試。 | 是 | 是 | 是，從3.2 |
| Z130 | 錯誤 | 由於使用了無效/格式錯誤的資源，授權被拒絕。 | 檢查資源字串並加以更正。 通常，此錯誤是由於格式錯誤的MRSS或使用純字串（而非MRSS）所致。 | n/a | 是 | 是 | 是，從3.2 |
| Z169 | 錯誤 | 由於已對指定資源應用authzNone降級規則，因此拒絕授權。 | 通知使用者 | n/a | 是 | 是 | 是，從3.2 |
| Z500 | 錯誤 | 內部錯誤。 <br> <br>  注意：這是舊版的「一般驗證錯誤」和「內部驗證錯誤」。 這個錯誤最終會淘汰。 | 使用AccessEnablerDebug並檢查調試日誌（console.log輸出）以確定出錯的原因。 | n/a | 是 | 是 | 是，從3.2 |
| P100 | 錯誤 | 預授權失敗。 這很可能是因為請求授權太多資源。 |  — 請勿使用超過允許的資源數上限。 <br> <br>  — 請聯絡Adobe Primetime驗證支援，以尋找/設定允許的資源數量上限。 | n/a | 是從v3.0 | 是 | 是，從3.2 |
| IS2XX | 錯誤 | 當個性化伺服器端點響應資料的格式無效或缺少所需的個性化資訊時，將返回這些錯誤代碼。 | 使用Zendesk開啟票證，並通知用戶系統暫時不可用 | n/a | 是從v3.0 | n/a | n/a |
| IS4XX | 錯誤 | 如果個人化伺服器端點失敗4XX — 是回應的HTTP狀態代碼，則會傳回這些錯誤碼。 | 使用Zendesk開啟票證，並通知用戶系統暫時不可用 | n/a | 是從v3.0 | n/a | n/a |
| IS5XX | 錯誤 | 如果個人化伺服器端點失敗5XX — 是回應的HTTP狀態代碼，則會傳回這些錯誤碼。 | 使用Zendesk開啟票證，並通知用戶系統暫時不可用 | n/a | 是從v3.0 | n/a | n/a |
| IS0 | 錯誤 | 當個人化伺服器端點完全未回應時，會傳回此程式碼，因此連線逾時 | 使用Zendesk開啟票證，並通知用戶系統暫時不可用 | n/a | 是從v3.0 | n/a | n/a |
| LS011 | 警告 | 由於LSO/LocalStorage問題和WebStorage問題（或不可用）,AccessEnabler正在使用易失儲存。 <br> <br> 驗證/授權不會持續存在超過目前頁面！ 每次頁面載入都會導致使用者需要驗證。 頁面重新載入時不會強制執行已設定的TTL。 |  — 通知使用者限制。 <br> <br>  — 告知用戶如何增加可用儲存空間。 <br> <br>  — 也可註銷以清除儲存。 |  — 增加儲存。 <br> <br>  — 註銷以清除儲存。 | 是 | n/a | n/a |

<br>

## 原始錯誤報告 {#original-error-reporting}

本節介紹原始錯誤報告系統以及原始錯誤代碼。 在原始錯誤報告系統中，AccessEnabler將錯誤傳遞給以下兩個回調函式： `setAuthenticationStatus()` 呼叫 `checkAuthentication()`; `tokenRequestFailed()`，在呼叫失敗後 `checkAuthorization()` 或 `getAuthorization()`.

原始錯誤報表和狀態API可繼續如先前般運作。 不過，日後將不會更新原始錯誤報告API。 所有新錯誤報告和舊錯誤更新將僅反映在新錯誤中 [高級錯誤報告系統](#advanced-error-reporting).


如需使用原始錯誤報告系統的範例，請參閱 [JavaScript API參考](/help/authentication/javascript-sdk-api-reference.md):[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) 和 [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) 函式， [iOS/tvOS API參考](/help/authentication/iostvos-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)和 [tokentRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed), [Android API參考](/help/authentication/android-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) 和 [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### 原始回撥錯誤代碼 {#original-callback-error-codes}

| **一般錯誤** |  |
|---|---|
| 內部錯誤 | 嘗試處理請求時發生系統錯誤。 |
| 未選擇提供程式錯誤 | 在提供者選擇對話方塊中取消時發生。 |
| 提供程式不可用錯誤 | 當沒有提供程式時發生。 |
|  |  |
| **驗證錯誤** |  |
| 一般驗證錯誤 | 當原因未知或無法發佈時傳回。 |
| 內部驗證錯誤 | 嘗試驗證時出現系統錯誤。 |
| 用戶未驗證錯誤 | 未驗證用戶。 |
|  |  |
| **授權錯誤** |  |
| 一般授權錯誤 | 當原因未知或無法發佈時傳回。 |
| 內部授權錯誤 | 嘗試授權時發生系統錯誤。 |
| 用戶未授權錯誤 | 客戶無權查看請求的內容。 |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->