---
title: 了解伺服器端量度
description: 了解伺服器端量度
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---

# 了解伺服器端量度 {#understanding-server-side-metrics}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


## 簡介 {#intro}

本檔案說明Entitlement Service Monitoring(ESM)服務產生的Adobe Primetime驗證伺服器端量度。 它不會說明從用戶端觀點看的相同事件(程式設計人員若要在其頁面/應用程式上實作測量服務(例如Adobe Analytics)，會看到什麼內容)。  

## 事件摘要 {#events_summary}

從Adobe Primetime驗證伺服器端的檢視點，會產生下列事件：

* **驗證流程中產生的事件**（使用MVPD實際登入）

   * AuthN嘗試通知 — 當使用者傳送至MVPD登入網站時，就會產生此通知。
   * AuthN待定通知 — 如果使用者以其MVPD成功登入，則當使用者重新導向回Primetime驗證時，就會產生此通知。
   * 授予的AuthN通知 — 當用戶返回程式設計師站點時，將生成此通知，並且已成功從Primetime身份驗證中檢索身份驗證令牌。 
* **授權流程** （只需檢查MVPD的授權）\
   *先決條件：* 有效的AuthN代號
   * AuthZ嘗試通知
   * 已授予AuthZ通知
* **成功播放請求**\
   *先決條件：* 有效的AuthN和AuthZ代號
   * 使用Adobe Primetime驗證的檢查通知 
   * 播放請求需要授權的驗證和授權


不重複使用者人數將於 [不重複使用者](#unique-users) 一節。 由於授予的驗證和授權回應通常是快取的，因此通常會套用下列公式：

* 嘗試AuthN的次數\>授予的AuthN數
* 嘗試AuthZ的次數\>授予的AuthZ的次數
* 嘗試AuthZ的次數\>授予的AuthN次數（通常）
* 成功播放請求數\>授予的AuthZ數


### 範例 {#example}

下列範例顯示一個品牌一個月的伺服器端量度：

|量度 | MVPD 1 | MVPD 2 | ... | MVPD n |總計 | | — | — | — | - | — | — | |成功的身份驗證 | 1125 | 2892 | | 2203 | SUM(MVP1+..MVPD n) | |成功的授權 | 2527 | 5603 | | 5904 | SUM(MVP1+..MVPD n) | |成功的播放請求 | 4201 | 10518 | | 10737 | SUM(MVP1+..MVPD n) | |不重複使用者 | 1375 | 2400 | | 2890 |所有已消除重複資料的MVPD的所有用戶總和\* | |嘗試的身份驗證 | 2147 | 3887 | | 3108 | SUM(MVP1+..MVPD n) | |嘗試的授權 | 2889 | 6139 | | 6039 | SUM(MVP1+..MVPD n) |

</br>

在此情況下，去重複化應該沒有作用，因為不同的MVPD使用者不應收到相同的使用者ID。 當為兩個不同品牌（但相同的MVPD）進行總和時，重複資料消除效果應該大得多。

## 事件觸發器 {#event_triggers}

### 新用戶 — 完整流量 {#new-user-full-flow}

下表說明沒有驗證Token的使用者（新使用者或驗證Token已過期的使用者）的事件和步驟：



![](assets/ae-flow-with-events.png)



該流涉及對MVPD的往返驗證(#5到\#7)和授權(\#11)。



流程完成後，會在使用者裝置上快取驗證和授權Token。 驗證Token的存留時間(TTL)值介於6小時到90天之間。 AuthN代號過期會自動強制AuthZ代號過期。 授權代號的TTL值通常為24小時。

| 已觸發伺服器端事件 | <ul><li>身份驗證嘗試，身份驗證掛起，已授予身份驗證</li><li>授權嘗試，授權</li><li>成功的播放要求</li></ul> |
|---|---|


### 已快取傳回使用者 — AuthZ和AuthN代號

對於快取了有效AuthZ和AuthN代號的使用者，會執行下列步驟：


![](assets/ae-flow-tokens-cached-web.png)



呼叫時會自動觸發 `getAuthorization()`，且僅涉及Adobe Primetime驗證的檢查。 MVPD不參與此流程。


| 已觸發伺服器端事件 | *成功播放要求 |
|---|---|


### 傳回使用者 — 已快取AuthN代號，AuthZ代號已過期

若使用者仍具備有效的AuthN代號，則會執行下列步驟：

![](assets/ae-flow-authn-token-cached.png)


此流程需要往返MVPD。


| 已觸發伺服器端事件 | <ul><li>授權嘗試，授權確定</li><li>成功的播放要求</li> |
|---|---|

## 驗證事件 {#authn_events}

### 驗證嘗試 {#authentication-attempt}

如上圖所示，只有在使用者往返MVPD時，才會觸發驗證事件；驗證事件不包含快取Token驗證。

使用者從選擇器按一下特定MVPD後，會觸發驗證嘗試事件。

* MVPD端上最接近此狀態的第一個事件是頁面載入
* Adobe Primetime驗證不會計算使用者重複嘗試登入MVPD頁面（密碼錯誤，請重試）
* 多次嘗試均計為一次嘗試
* 有些MVPD也會在驗證步驟中執行授權，如果授權失敗，系統不會將使用者重新導向回。

### 驗證掛起 {#authentication-pending}

重新導向至Adobe Primetime驗證的程式啟動時，即會發生此事件。

### 授予的驗證 {#authentication-granted}

使用者是MVPD的已知訂閱者，通常為付費電視訂閱，但有時僅限網際網路存取。 成功驗證可能是因為用戶使用其MVPD明確輸入了有效憑據，或者他們先前輸入了有效憑據，並且已選中「記住我」（並且前一個會話尚未過期）。

因此，MVPD會傳送Adobe Primetime驗證給驗證請求的正面回應，而Adobe Primetime驗證會建立 *AuthN代號*.

* 通常會快取長時間（一個月或更久）的驗證。 因此，在Token過期並重新啟動流程之前，驗證事件將不再存在。
* 透過單一登入從其他網站/應用程式進入將不會觸發驗證事件。

 

### Comcast驗證 {#comcast-authentication}

與其他MVPD相比，Comcast的AuthN流量不同。

以下功能說明差異：

* **工作階段Cookie行為**:這會導致使用者關閉瀏覽器後，完全移除任何驗證Token。 此功能僅存在於Web上。 主要目的是確保您的Comcast工作階段不會持續存在於不安全/共用的電腦上。 其影響是，與其餘的MVPD相比，會有更多驗證嘗試/授權的流量。

* **每個請求者ID的AuthN**:Comcast不允許將AuthN狀態從一個請求者ID快取到另一個請求者ID。 因此，每個網站/應用程式都必須前往Comcast取得驗證Token。 除了使用者體驗考量事項，如上所述，其影響在於會產生更多驗證嘗試/已授權事件。

* **被動驗證**:為了改善使用者體驗，但仍維持每個requestorID的AuthN功能，會在隱藏的iFrame中發生被動式驗證流程。 使用者看不到任何內容，但事件仍會如先前般觸發。

如果使用者在Comcast登入頁面上按一下「記住我」，則此頁面的後續造訪（在2週內）將只是快速重新導向回。 否則，使用者實際上必須在頁面上驗證。

### 失敗驗證 {#unsuccessful-authentication}

失敗的驗證不是Adobe Primetime驗證中的事件本身，而是可以以嘗試與成功之間的差異來計算。

在2013年5月版本中，Adobe Primetime驗證將新增因系統或網路錯誤而失敗的驗證的錯誤碼，包括DRM錯誤（權杖捆綁失敗）和LSO錯誤（沒有空間寫入權杖等）。

### 驗證轉換率 {#authenitication-conversion-rate}

程式設計師可追蹤的一個有趣量度是驗證轉換率，計算方式為（授予的AuthN請求/AuthN）%。

關於量度的一些附註：

* 由於這是以事件為基礎的量度，因此不會真正反映不重複使用者轉換率（如果使用者嘗試八次並在第九次成功），這在上述轉換率中會反映得非常糟糕。
* Adobe Primetime驗證（位於伺服器端）中尚無法運算唯一的驗證轉換。
* 如果網站/應用程式中存在自動AuthN重試次數，這也會扭曲上述量度。

## 授權事件 {#authorization_events}

### 授權嘗試 {#authorization_attempt}

除了取得驗證Token，使用者在播放內容之前還必須取得授權Token。 這通常會在驗證之後，或授權Token過期時發生。 由於此檢查是在伺服器端(從Adobe Primetime驗證伺服器到MVPD伺服器)進行，因此使用者不需要執行任何動作。

### 授權 {#authorization-granted}

「授權」表示被驗證用戶的訂閱包括所請求的寫程式。

請注意，並非所有MVPD都支援個別的授權步驟；對於某些驗證，則與授權相等。 MVPD會傳送Adobe Primetime驗證對後通道AuthZ請求的成功回應，而Adobe Primetime驗證會建立AuthZ代號。

* AuthZ代號會快取一段時間，通常為24小時。在此期間不會引發AuthZ事件。
* 有些MVPD使用資產層級授權，有些則使用通道層級授權； — 視使用者而定，會引發更多或更少AuthZ事件。 即使是通道層級授權，也已建立快取功能，因此若在24小時內請求相同資產，將不會引發任何事件。

### 拒絕授權 {#authorization-denied}

如果拒絕授權，則被驗證的用戶沒有對所請求的寫程式的確認訂閱。 最可能的原因是管道不是使用者訂閱套件的一部分，但這也可能反映使用者只能從MVPD存取網際網路。

對於某些MVPD，即使使用者只有來自MVPD的網際網路訂閱（無付費電視訂閱），使用者仍會成功驗證。 在這種情況下，即使用戶請求授權的通道位於基包中，授權也將被拒絕。

有些MVPD會針對AuthZ拒絕提供自訂錯誤訊息，其中可能包含升級其套件的選件。


### 授權轉換率 {#authorization-conversion-rate}

驗證轉換率的計算方式為（授予的AuthZ請求/授予的AuthZ）%。

### 成功播放請求 {#successful-play-request}

經過驗證和授權的用戶被允許查看受保護的內容。

在成功的播放要求時，Adobe Primetime驗證會產生短時的媒體代號，主張使用者有權檢視要求的視訊。 程式設計師使用此媒體令牌來進一步驗證潛在的查看器。 媒體代號會作為成功的播放請求受到追蹤。

* Adobe Primetime驗證 *not* 追蹤視訊播放是否實際在產生媒體代號之後開始。 例如，如果內容有地理限制，即使資料流實際上從未開始，交易仍會計為成功播放請求。
* 由於AuthN和AuthZ代號會在一段時間內快取MVPD回應，因此成功的播放請求事件是量度中最頻繁的事件。

## 不重複使用者 {#unique-users}

### 定義 {#definition}

成功驗證時，Adobe Primetime驗證會根據傳回的MVPD使用者ID值，追蹤唯一使用者的存在。  此值以使用者的登入資訊為基礎，但不包含可個人識別的資訊。

此值也會傳遞至sendTrackingData回呼中的網站/應用程式。

此值可在各裝置間持續存在（無論登入發生的位置，MVPD都會為指定使用者產生相同的值）或暫時(每次登入時都會產生新值，MVPD會在其後端對應該新值。 MVPD提供給Adobe Primetime驗證的值通常會在工作階段和裝置間持續存在，但如同所述，持續性並未得到保證或驗證。

此值可用來計算不重複使用者。 所報告的值（根據請求者ID/間隔/MVPD）會針對特定間隔進行去重複化。 因此，每日不重複使用者的總數通常與每月值不同，而每月值的值則較低。

此數字包含來自Adobe Primetime驗證的所有事件，減去驗證嘗試（沒有使用者ID），但包括嘗試（可能失敗）的授權。

### 範例 {#examples}

#### 第1天 {#day1}

使用者XYZ前往網站觀看影片。

引發的事件：

* AuthN嘗試（尚未有不重複使用者）
* 已授予AuthN
   * 此時，我們會根據MVPD傳回的內容來唯一識別使用者，因此每日不重複使用者計數會增加1
   * 快取AuthN代號30天
* AuthZ嘗試/授予事件
   * 快取1天的AuthZ代號
* 成功播放要求事件

#### 第1天（稍後） {#day1-later-on}

用戶XYZ觀看了另一個視頻。

引發的事件：

* 成功播放要求事件（其餘內容會快取）
* 每日或每月獨特值沒有增加

#### 第3天 {#day3}

用戶XYZ觀看了另一個視頻。

引發的事件：

* AuthZ嘗試/授予事件
   * 自第1天開始的1天快取已過期
* 成功播放要求事件（其餘內容會快取）
* 每日不重複使用者增加1 — 每月不重複值仍為1

#### 第31天 {#day31}

用戶XYZ觀看了另一個視頻。

與第1天相同，因為AuthN快取已過期。

如果同一個用戶未通過授權，則每月的不重複用戶計數仍將增加1，因為有兩個事件包含用戶ID：授予的身份驗證和授權嘗試。

### 單一登入(SSO) {#single-sign-on-sso}

在某些情況下，不重複使用者的數量可能會大於成功驗證的數量。 當許多使用者透過其他網站/應用程式的單一登入(SSO)傳入，且只需要在目前的網站/應用程式上取得授權，通常就是這種情況。

### 比較用戶端和伺服器端不重複使用者 {#comparing-client-side-and-server-side-unique-users}

若使用者ID值來自 `sendTrackingData()` 用於用戶端以計算不重複使用者，則用戶端和伺服器端號碼應相符。

如果差異很大，以下原因通常會造成差異：

* 視訊播放獨特值與所有事件不重複值。 如前所述，Adobe Primetime驗證會計算除AuthN嘗試以外所有事件的不重複使用者。 這表示如果使用者僅驗證（在頁面上）但未檢視視訊，仍會觸發不重複使用者計數增加。

* 計算授權失敗的使用者數 — Adobe Primetime驗證會計算這些使用者以及報告的數字。

<!--
## Related Information {#related-information}

- [Entitlement Service Monitoring API](/help/authentication/entitlement-service-monitoring-api.md)

-->