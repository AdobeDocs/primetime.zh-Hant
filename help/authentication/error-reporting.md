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
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。


## 概述 {#overview}

在Adobe Primetime中報告錯誤身份驗證目前採用兩種不同方式實現：

* **高級錯誤報告** 實施者註冊錯誤回調，以 [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk) 或實現名為「的介面方法`status`&quot; [AccessEnableriOS/tvOS SDK](#accessenabler-ios-tvos-sdk) 和 [AccessEnabler Android SDK](#accessenabler-android-sdk)，以便接收高級錯誤報告。 錯誤被分類為 **資訊**。 **警告**, **錯誤** 的下界。 此報告系統 **非同步**, **無法保證觸發多個錯誤的順序**。  有關高級錯誤報告系統的詳細資訊，請參見 [高級錯誤報告](#advanced-error-reporting) 的子菜單。

* **原始錯誤報告 —** 一種靜態報告系統，在該系統中，當特定請求失敗時，錯誤消息會傳遞到特定回調函式。 錯誤分為一般、驗證和授權類型。 有關在原始系統中報告的錯誤清單，請參見 [原始錯誤報告](#original-error-reporting) 的子菜單。


## 高級錯誤報告 {#advanced-error-reporting}

* [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk)
* [AccessEnableriOS/tvOS SDK](#accessenabler-ios-tvos-sdk)
* [AccessEnabler Android SDK](#accessenabler-android-sdk)
* [AccessEnabler FireOS SDK](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>老 [原始錯誤報告](#original-error-reporting) API將繼續像以前一樣工作，高級錯誤報告不會中斷功能，但原始錯誤報告將不再接收任何更新。 高級錯誤報告系統將發生所有新錯誤和更新。

### AccessEnabler JavaScript SDK {#accessenabler-javascript-sdk}

新的錯誤報告系統是可選的，因此實施者可以顯式註冊錯誤處理程式回調以接收高級錯誤報告。 該系統包括動態註冊和註銷多個錯誤回調的能力。 此外，在載入AccessEnabler JavaScript SDK後，您可以立即註冊任何新錯誤回調，而無需執行任何其他初始化（在調用之前） `setRequestor()`)，表示您能夠接收有關初始化和配置錯誤的高級報告。


#### 實施 {#access-enab-js-imp}

yourErrorHandler(errorData:Object)


錯誤處理程式回調函式將接收具有以下結構的單個對象（映射）:

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

### 1。綁定 {#bind}

**`.bind(eventType:String, handlerName:String):void`**

為事件附加處理程式。

**`eventType`**  — 僅「」`errorEvent`&quot;值導致AccessEnabler JavaScript SDK觸發高級錯誤報告回調。

**`handlerName`**  — 指定錯誤處理程式函式名稱的字串。\
 

兩個綁定參數必須只使用以下集中的字元： `[0-9a-zA-Z][-._a-zA-Z0-9]`;即，參數必須以數字或字母開頭，然後只能包含連字元、句點、下划線和字母數字字元。  此外，參數不能超過1024個字元。  

**示例** 綁定錯誤處理程式：

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

由於技術限制，您無法綁定關閉或匿名函式。 必須在第二個參數中指定方法的名稱。

 
### 2.解除綁定 {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

刪除以前附加的事件處理程式。

**`eventType`**  — 僅「 」`errorEvent`&#39;值導致AccessEnabler JavaScript SDK觸發高級錯誤報告回調。

**`handlerName`**  — 指定錯誤處理程式函式名稱的字串（如果為null或缺少指定的所有附加處理程式） `eventType` 將被刪除。

兩個綁定參數必須只使用以下集中的字元： `[0-9a-zA-Z][-._a-zA-Z0-9]`;即，參數必須以數字或字母開頭，然後只能包含連字元、句點、下划線和字母數字字元。  此外，參數不能超過1024個字元。  

**示例** 刪除單個錯誤處理程式：

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**示例** 刪除所有錯誤處理程式：

`accessEnabler.unbind('errorEvent');`


### AccessEnableriOS/tvOS SDK {#accessenabler-ios-tvos-sdk}

新的錯誤報告系統是強制性的，因此實施者必須明確遵守新的目標C &quot;EntilementStatus&quot;協定。 此新方法允許程式設計師接收高級錯誤報告。

#### 實施 {#accessenab-ios-tvossdk-imp}

實施者需要遵守以下 **權利狀態** 協定：

**權利狀態.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

您 **狀態** 函式將接收單個對象( `NSDictionary`)，其結構如下：

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

**2. 實施**

```OBJ-C
    @implementation DemoAppAppDelegate     
    // very simple implementation
    - (void)status:(NSDictionary *)statusDict {
        NSLog(@"%@:\n%@", statusDict[@"level"], statusDict);
    }
```


### AccessEnabler Android SDK {#accessenabler-android-sdk}

新錯誤報告系統是強制性的，因為實施者必須明確遵守 `IAccessEnablerDelegate` 介面定義協定。 此新方法允許程式設計師接收高級錯誤報告。

#### 實施 {#access-enablr-androidsdk-imp}

實施者需要處理新 `status` 方法`IAccessEnablerDelegate`。 的 **`status`** 函式將接收單個 **`AdvancedStatus`** 對象具有以下模型：

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

**示例**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

### AccessEnabler FireOS SDK {#accessenabler-fireos-sdk}


新錯誤報告系統是強制性的，因為實施者必須明確遵守 `IAccessEnablerDelegate` 介面定義協定。 此新方法允許程式設計師接收高級錯誤報告。

#### 實施 {#access-enab-fireos-sdk-}

實施者需要處理新 `status`方法`IAccessEnablerDelegate`。 的 **`status`** 函式將接收單個 **`AdvancedStatus`** 對象具有以下模型：

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

**示例**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

## 高級錯誤代碼參考 {#advanced-error-codes-reference}

下表列出並說明了較新的錯誤API所暴露的錯誤代碼，以及要採取的糾正它們的建議操作：

| ID | 級別 | 說明 | 開發人員操作 | 用戶操作 | JavaScid | iOS/電視OS | 安卓 |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL和AAPL_ERROR | 錯誤 | 一般AppleSSO錯誤 | 該錯誤包含帶有原始VSA錯誤的詳細資訊欄位。 | n/a | n/a | 是 | n/a |
| VSA203 | 資訊 | 當通過平台SSO登錄導致身份驗證時，用戶決定註銷應用程式。 | 指示/提示用戶從Settings -> Accounts -> TV Provider on tvOS明確註銷。 <br><br> 指示/提示用戶從iOS/iPadOS上的「Settings -> TV Provider（設定 — >電視提供程式）」中明確註銷。 | 顯式從tvOS上的Settings -> Accounts -> TV Provider註銷。 <br> <br> 顯式從iOS/iPadOS上的「設定」 — >「電視提供商」註銷 | n/a | 是 | n/a |
| VSA404 | 資訊 | 應用程式視頻訂戶帳戶權限未確定。 | 通過解釋單一登錄(SSO)用戶體驗的優點，獎勵拒絕授予訪問訂閱資訊權限的用戶。 | 用戶可以通過轉到應用程式設定（電視提供商訪問權限）或轉到iOS/iPadOS上電視提供商或設定 — >帳戶 — >電視提供商tvOS上的「設定」 — > 「電視提供商」部分來更改其決定。 | n/a | 是 | n/a |
| VSA503 | 資訊 | 應用程式視頻訂閱伺服器帳戶元資料請求失敗。 | MVPD終結點未響應。 應用程式可以回退到常規身份驗證流。 | n/a | n/a | 是 | n/a |
| 500 | 錯誤 | 內部錯誤 | 使用AccessEnablerDebug並檢查調試日誌（console.log輸出），以確定出錯的原因。 | n/a | 是 | 是 | n/a |
| SEC403 | 錯誤 | 域安全錯誤。 請求者使用的域無效。 特定請求者ID使用的所有域都需要按Adobe列出白名。 |  — 僅從允許的域清單中載入AccessEnabler <br> <br>  — 聯繫Adobe，以管理使用的請求者ID的域白名單 <br> <br> -iOS:驗證您使用的證書是否正確，以及是否正確建立了簽名 | n/a | n/a | 是 | n/a |
| SEC412 | 警告 | [ 在2.5版中提供 ] 設備ID不匹配。 當基礎平台更改其設備ID時，就會發生這種情況。 在這種情況下，將清除現有令牌，並且用戶將不再經過身份驗證。 請注意，當用戶使用JS SDK並正在漫遊時（在JS上，客戶端IP是設備ID的一部分），這是合法的。 否則，這可能是欺詐企圖的指示 — 試圖從其他設備複製令牌。 |  — 監視警告數。 如果它們沒有明顯原因而出現峰值(最近沒有瀏覽器更新；新作業系統)，可能是欺詐企圖的一個指標。  <br> <br> — （可選）通知用戶需要重新登錄。 | 再次登錄。 | 是 | 是 | 是，從3.2開始 |
| SEC420 | 錯誤 | 與Adobe Primetime身份驗證伺服器通信時出現HTTP安全錯誤。 通常，當欺騙/代理就位時會發生此錯誤。 |  — 載入 `[https://]{SP_FQDN\}` 並手動接受SSL證書，例如， **https://api.auth.adobe.com** 或 **https://api.auth-staging.adobe.com** <br> <br> — 將代理證書標籤為受信任 | 如果普通用戶發生這種情況，則表明可能會發生中間人攻擊！ | 是 | 是 | 是，從3.2開始 |
| CFG100 | 警告 | 未正確設定客戶端電腦「Date / Time / Timezone」。 這可能導致身份驗證/授權錯誤。 |  — 通知用戶設定正確的時間。 <br> <br> 採取措施防止權利流動，因為它們可能會失敗。 | 設定正確的日期/時間。 | 是 | 是 | 是，從3.2開始 |
| CFG400 | 錯誤 | 提供了無效的請求者ID。 | 開發人員必須指定有效的請求者ID。 | n/a | 是 | 是 | 是，從3.2開始 |
| CFG404 | 錯誤 | 找不到Adobe Primetime身份驗證伺服器。 這可以在3種情況下發生： <br><br>  — 開發人員已部署無效的欺騙。 <br><br>  — 用戶存在網路問題，無法訪問Adobe Primetime身份驗證域。 <br><br> -Adobe Primetime驗證伺服器配置錯誤。 <br><br>  **注：** 在Firefox上，將顯示CFG400，而不顯示CFG404（瀏覽器限制） |  — 檢查欺騙。 <br><br>  — 檢查網路/DNS設定。 <br><br>  — 通知Adobe。 | 檢查網路/DNS設定。 | 是 | 是 | 是，從3.2開始 |
| CFG410 | 錯誤 | AccessEnabler太舊。 | 通知用戶清除快取。 | 清除瀏覽器快取。 | 是 | n/a | 是，從3.2開始 |
| CFG5xx | 錯誤 | Adobe Primetime身份驗證伺服器遇到內部錯誤。 xx可以是任何數字。 |  — 告知用戶Adobe Primetime驗證不可用。 <br><br>  — 繞過Adobe Primetime驗證。 <br> <br>  — 通知Adobe。 | 稍後再試。 | 是 | 是 | 是，從3.2開始 |
| N000 | 資訊 | 未驗證用戶。 | n/a | 登錄。 | 是 | 是 | 是，從3.2開始 |
| N001 | 資訊 | 已在後台啟動被動身份驗證嘗試。 對於配置了「每個請求者的身份驗證」的MVPD，將發生這種情況。 雖然用戶希望能夠被自動驗證，但這會在初始化時產生效能損失。 | （可選）通知用戶或顯示提醒用戶「正在進行工作」的UI。 | 等等。 | 是 | 是 | 是，從3.2開始 |
| N003 | 資訊 | 用戶從AppleMVPD選取器中選擇「其他電視提供商」選項。 | 的 *displayProviderDialog* 將調用回調，應用程式可以回退到常規身份驗證流。 | 選擇常規MVPD並繼續登錄螢幕。 | n/a | 是 | n/a |
| N004 | 資訊 | 用戶選擇當前請求者不支援的電視提供者。 | 的 *displayProviderDialog* 將調用回調，應用程式可以回退到常規身份驗證流。 | 選擇常規MVPD並繼續登錄螢幕。 | n/a | 是 | n/a |
| N005 | 資訊 | 已取消MVPD選取器。 | n/a | n/a | 是 | 是 | 是，從3.2開始 |
| N010 | 警告 | 在為所選MVPD設定「authenticate-all」降級規則時，已對用戶進行身份驗證。 | （可選）通知用戶由於MVPD困難而獲得「免費」訪問。 | n/a | 是 | 是 | 是，從3.2開始 |
| N011 | 資訊 | 用戶已使用TempPass進行身份驗證。 |  — 通知用戶。 <br> <br>  — （可選）提供常規MVPD清單。 | （可選）使用常規MVPD登錄。 | 是 | 是 | 是，從3.2開始 |
| N111 | 警告 | 過期的TempPass。 |  — 通知用戶。 <br> <br>  — 提供常規MVPD的清單。 <br> <br>  — 隱藏TempPass選項。 | 使用常規MVPD登錄。 | 是 | 是 | 是，從3.2開始 |
| N130 | 錯誤 | **在會話上找不到身份驗證令牌。**  這可能是由於以下原因之一： <br> <br> 1. 瀏覽器已禁用（第三方）Cookie（不適用於AccessEnabler JavaScript SDK版本4.x） <br> <br> 2. 瀏覽器已啟用「防止跨站點跟蹤」(Safari 11+) <br> <br> 3. 會話已過期 <br> <br> 4. 程式設計師連續調用驗證API時不正確 <br> <br> 注：此錯誤代碼不可用於全頁重定向身份驗證流。 | 1。提示用戶啟用（第三方）Cookie <br> <br> 2. 禁止用戶跨站點跟蹤 <br> <br> 3. 提示用戶重新驗證 <br> <br> 4. 按正確順序調用API | 1。啟用（第三方）Cookie <br> <br> 2. 禁用跨站點跟蹤 <br> <br> 3. 重新驗證 <br> <br> 4. 不適用 | 是 | 是 | 是，從3.2開始 |
| N500 | 錯誤 | 內部錯誤。 <br> <br> 注：這是原始錯誤系統的「一般驗證錯誤」和「內部驗證錯誤」。 這個錯誤最終將被淘汰。 | 使用AccessEnablerDebug並檢查調試日誌（console.log輸出），以確定出錯的原因。 | n/a | 是 | 是 | n/a |
| R401 | 錯誤 | 嘗試獲取訪問令牌時出錯。 <br> <br> 注：這是一個無法恢復的錯誤。 通知用戶應用程式不可用。 | -iOS:檢查應用程式中的軟體語句和自定義方案。 <br> <br> - JavaScript:檢查網站應用程式中的軟體語句。 <br> <br> 使用Zendesk開啟票證並通知用戶系統暫時不可用 | n/a | 是從4.0版 | 是從3.0版 | 是，從3.2開始 |
| R400 | 錯誤 | 未註冊應用程式。 軟體語句無效或已被吊銷。 <br> <br> 注：這是一個無法恢復的錯誤。 通知用戶應用程式不可用。 | -iOS:檢查應用程式中的軟體語句和自定義方案。 <br> <br> - JavaScript:檢查網站應用程式中的軟體語句。 <br> <br> 使用Zendesk開啟票證並通知用戶系統暫時不可用 | n/a | 是從4.0版 | 是從3.0版 | 是，從3.2開始 |
| REG500 | 錯誤 | 無法從伺服器獲取註冊代碼。 <br> <br> 注：這是一個無法恢復的錯誤。 通知用戶應用程式不可用。 | 使用Zendesk開啟票證，並通知用戶系統暫時不可用。 | n/a | 是從4.0版 | 是從3.0版 | 是，從3.2開始 |
| REGCODE | 成功 | 在tvOS平台上調用setSelectedProvider API的應用程式。 | 指示/提示用戶使用第二設備（螢幕）使用提供的註冊代碼登錄。 | 使用第二個設備（螢幕）上的regcode啟動身份驗證。 | n/a | 是，僅適用於tvOS | n/a |
| Z010 | 警告 | 在為所選MVPD設定「authenticate-all」或「authorize-all」降級規則時，已授權用戶。 | （可選）通知用戶由於MVPD困難而獲得「免費」訪問。 | n/a | 是 | 是 | 是，從3.2開始 |
| Z011 | 資訊 | 用戶已使用TempPass授權 | （可選）通知用戶 | n/a | 是 | 是 | 是，從3.2開始 |
| Z100 | 錯誤 | 授權失敗，因為用戶沒有訂閱請求的資源，或者由於MVPD的其他原因，例如視頻與用戶帳戶的家長控制設定不匹配 |  — 不允許播放。 <br> <br>  — 通知用戶。 <br> <br>  — 錯誤消息MAY中的「message」鍵包含MVPD提供的更詳細的消息。 | n/a | 是 | 是 | 是，從3.2開始 |
| Z110 | 錯誤 | 由於MVPD重複拒絕，授權被拒絕。 可能的欺詐嘗試或DOS。 |  — 不允許播放。 <br> <br>  — 通知用戶。 | n/a | 是 | 是 | 是，從3.2開始 |
| Z120 | 錯誤 | 由於與MVPD通信時的技術原因而拒絕授權。 可能的網路錯誤。 |  — 不允許播放。 <br> <br>  — 告知用戶MVPD遇到了困難，他們應稍後再試。 | 稍後再試。 | 是 | 是 | 是，從3.2開始 |
| Z130 | 錯誤 | 由於使用了無效/格式錯誤的資源，授權被拒絕。 | 檢查資源字串並更正它。 通常，此錯誤是由於格式錯誤的MRSS或使用純字串代替MRSS。 | n/a | 是 | 是 | 是，從3.2開始 |
| Z169 | 錯誤 | 由於已對指定資源應用authzNone降級規則，因此拒絕授權。 | 通知用戶 | n/a | 是 | 是 | 是，從3.2開始 |
| Z500 | 錯誤 | 內部錯誤。 <br> <br>  注：這是傳統的「一般驗證錯誤」和「內部驗證錯誤」。 這個錯誤最終將被淘汰。 | 使用AccessEnablerDebug並檢查調試日誌（console.log輸出），以確定出錯的原因。 | n/a | 是 | 是 | 是，從3.2開始 |
| P100 | 錯誤 | 預授權失敗。 這很可能是因為請求授權太多的資源。 |  — 不要使用超過允許的最大資源數。 <br> <br>  — 聯繫Adobe Primetime身份驗證支援以查找/設定允許的最大資源數。 | n/a | 是從3.0版 | 是 | 是，從3.2開始 |
| IS2XX | 錯誤 | 當個性化伺服器端點響應資料的格式無效或缺少所需的個性化資訊時，返回這些錯誤代碼。 | 使用Zendesk開啟票證並通知用戶系統暫時不可用 | n/a | 是從3.0版 | n/a | n/a |
| IS4XX | 錯誤 | 如果個別化伺服器端點故障4XX — 是響應的HTTP狀態代碼，則返回這些錯誤代碼。 | 使用Zendesk開啟票證並通知用戶系統暫時不可用 | n/a | 是從3.0版 | n/a | n/a |
| IS5XX | 錯誤 | 如果個別化伺服器端點故障5XX — 是響應的HTTP狀態代碼，則返回這些錯誤代碼。 | 使用Zendesk開啟票證並通知用戶系統暫時不可用 | n/a | 是從3.0版 | n/a | n/a |
| IS0 | 錯誤 | 當個性化伺服器端點根本沒有響應時，將返回此代碼，因此連接已超時 | 使用Zendesk開啟票證並通知用戶系統暫時不可用 | n/a | 是從3.0版 | n/a | n/a |
| LS011 | 警告 | 由於LSO/LocalStorage問題和WebStorage問題（或不可用）,AccessEnabler正在使用易失性儲存。 <br> <br> 身份驗證/授權不會在當前頁面之外持續！。 每個頁面載入都將導致用戶需要進行身份驗證。 在重新載入頁面時，不會強制執行配置的TTL。 |  — 告知用戶限制。 <br> <br>  — 告知用戶如何增加可用儲存空間。 <br> <br>  — 或者註銷以清除儲存。 |  — 增加儲存。 <br> <br>  — 註銷以清除儲存。 | 是 | n/a | n/a |

<br>

## 原始錯誤報告 {#original-error-reporting}

本節介紹原始錯誤報告系統以及原始錯誤代碼。 在原始錯誤報告系統中，AccessEnabler將錯誤傳遞給以下兩個回調函式： `setAuthenticationStatus()` 呼叫後 `checkAuthentication()`; `tokenRequestFailed()`，呼叫失敗後 `checkAuthorization()` 或 `getAuthorization()`。

原始錯誤報告和狀態API與以前完全一樣繼續工作。 但是，轉發原始錯誤報告API時不會更新。 對舊錯誤的所有新錯誤報告和更新將僅反映在 [高級錯誤報告系統](#advanced-error-reporting)。


有關使用原始錯誤報告系統的示例，請參見 [JavaScript API參考](/help/authentication/javascript-sdk-api-reference.md):[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) 和 [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) 函式， [iOS/tvOS API參考](/help/authentication/iostvos-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)和 [tokentRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed)。 [Android API參考](/help/authentication/android-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) 和 [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed)。

### 原始回調錯誤代碼 {#original-callback-error-codes}

| **一般錯誤** |  |
|---|---|
| 內部錯誤 | 嘗試處理請求時發生系統錯誤。 |
| 提供程式未選擇錯誤 | 在提供商選擇對話框中取消時發生。 |
| 提供程式不可用錯誤 | 當沒有提供程式時發生。 |
|  |  |
| **驗證錯誤** |  |
| 常規身份驗證錯誤 | 當原因未知或無法發佈時返回。 |
| 內部身份驗證錯誤 | 嘗試驗證時發生系統錯誤。 |
| 用戶未驗證錯誤 | 未驗證用戶。 |
|  |  |
| **授權錯誤** |  |
| 常規授權錯誤 | 當原因未知或無法發佈時返回。 |
| 內部授權錯誤 | 嘗試授權時發生系統錯誤。 |
| 用戶未授權錯誤 | 客戶無權查看請求的內容。 |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->
