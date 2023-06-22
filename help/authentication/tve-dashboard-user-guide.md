---
title: Primetime TVE儀表板使用手冊
description: Primetime TVE儀表板使用手冊
exl-id: 6f7f7901-db3a-4c68-ac6a-27082db9240a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '4386'
ht-degree: 0%

---

# Primetime TVE儀表板使用手冊 {#tve-db-user-guide}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 簡介 {#tve-db-intro}

[[!DNL Adobe] TVE儀表板（TVE儀表板）](https://console.auth.adobe.com/) 是一個自助儀表板，目標讀者為與Adobe Primetime驗證產品團隊有業務關係的媒體公司（程式設計師）使用者。

請聯絡您的技術客戶經理(TAM)以取得存取權。 若要取得存取權，您需要在Adobe Marketing Cloud組織中設定兩個新使用者群組：

* TVE儀表板讀寫 — 此群組的成員在儀表板的所有可編輯區段上擁有完整許可權
* 唯讀TVE控制面板 — 此群組的成員僅擁有整個控制面板的檢視許可權


在深入瞭解本使用手冊之前，建議您先瀏覽下列資源，以充分瞭解Adobe Primetime驗證產品團隊提供的流程和功能，並熟悉本檔案所使用的術語：

* [TVE技術檔案](/help/authentication/technical-paper.md)
* [程式設計人員Kickstart指南](/help/authentication/programmer-kickstart-guide.md)
* [權益流程](/help/authentication/entitlement-flow.md)
* [字彙表](/help/authentication/glossary.md)


繼續本使用手冊的後續章節，您會發現管理公司頻道、程式設計師或頻道與MVPD （多頻道視訊程式經銷商）之間整合的不同設定的方式。

>[!IMPORTANT]
>TVE儀表板提供在基本和進階工作區之間切換的選項。 您可以切換右上角的圖示來完成此操作。 進階工作區的目標讀者是具備大量技術知識以及Adobe Primetime驗證產品團隊所提供功能的進階知識的使用者。

![TVE儀表板工作區](assets/tve-basic-advanced-workspace.png)

*圖1： Adobe Primetime TVE控制面板「基本/進階工作區」下拉式清單*

## 環境 {#authn-environments}

根據使用者可能需要完成的工作，他/她可能需要在Adobe Primetime驗證環境之間切換。 如需Adobe Primetime驗證環境的詳細資訊，請參閱以下檔案： [瞭解Adobe Primetime驗證環境](/help/authentication/understanding-the-adobe-environments.md).

TVE Dashboard提供名為Prequal (Prequalification)和Release的兩個環境，每個環境都有名為Staging和Production的兩個設定檔，如下所示：

* [預先測試](https://console-prequal.auth-staging.adobe.com/)
* [預先生產](https://console-prequal.auth.adobe.com/)
* [發行預備](https://console.auth-staging.adobe.com/)
* [發行生產](https://console.auth.adobe.com/)

若要在環境之間切換，使用者可以從以下所示的下拉式元素中按一下專案所代表的所需環境：

![TVE儀表板環境下拉式清單](assets/tve-dashboard-env.png)

*圖2： Adobe Primetime TVE儀表板環境下拉式清單*

>[!IMPORTANT]
>請務必注意，在透過TVE儀表板對您的Adobe Primetime驗證設定進行管理變更時，我們強烈建議您依照下列順序進行，以確保正常運作。

若要透過TVE儀表板對您的Adobe Primetime驗證設定進行管理變更：

* 在中執行變更 [發行測試版並進行驗證](http://sp.auth-staging.adobe.com/apitest/api.html).
* 在中執行變更 [預先生產並進行驗證](http://sp.auth-staging.adobe.com/apitest/api.html).
* 在中執行變更 [發佈生產環境並進行驗證](http://sp.auth-staging.adobe.com/apitest/api.html).

>[!IMPORTANT]
>若要讓管理變更上線，使用者必須透過選取按鈕（將顯示在側欄的左下方）導覽至「檢閱和推播變更」區段，以便檢閱變更、新增新建立變更的說明，並透過選取「推播設定」確認設定更新。

![存放儀表板檢閱推播通知](assets/tve-review-push-notifications.png)

*圖3： Adobe Primetime TVE控制面板檢閱和推播變更通知*

## 區段 {#sections}

為媒體公司工作的使用者（程式設計師）可以從側邊欄存取TVE儀表板的以下區段：

* **頻道**  — 包含與內容提供者相關的設定
* **程式設計師**  — 包含與彙總一或多個專案的上層組織相關的設定 **頻道**
* **整合**  — 包含與以下專案之間的整合相關的設定： **頻道** 和 **MVPDs**
* **MVPDs**  — 包含與可用專案相關的設定 **MVPDs**
* **報表**  — 包含三種報表型別的彙總資料：AuthN TTL、AuthZ TTL、SSO
* **變更記錄**  — 包含套用至TVE儀表板設定的最新修改

![TVE儀表板區段](assets/tve-dashboard-sections.png)

*圖4： Adobe Primetime TVE控制面板區段*

### 頻道 {#tve-db-channels-section}

此區段可讓您檢視和編輯可用頻道的設定或建立新頻道。 按一下其中一個可用的「色版」會傳回含有下列標籤的畫面：

* **管道資料**
   * **管道Id**  — 我們系統中使用的管道唯一ID，也稱為「請求者ID」。
   * **顯示名稱**  — 頻道的商業名稱。
* **一般設定**
   * **Analytics設定**  — 設定Adobe Primetime驗證事件以轉送至Adobe Analytics。 如需在啟用此功能之前需要如何設定報表套裝ID (RSID)的詳細資訊，請聯絡Adobe。
* **憑證**

   包含驗證流程中使用的憑證清單，以及它們的發行組織、發行日期和到期日。 這些憑證可作為私人/公開金鑰，並用於驗證用途。
* **網域**

   包含各個管道將與Adobe Primetime驗證通訊的網域清單。
* **整合**

   包含與可用MVPD的整合清單，以及每個可能啟用或未啟用的整合狀態。 按一下特定專案，即可導覽至整合頁面。
* **註冊的應用程式**

   包含應用程式註冊清單。 如需更多詳細資訊，請檢閱檔案 [動態使用者端註冊管理](/help/authentication/dynamic-client-registration-management.md).

* **自訂配置**

   包含自訂配置清單。 如需詳細資訊，請參閱 [iOS/tvOS應用程式註冊](/help/authentication/iostvos-application-registration.md) 和 [動態使用者端註冊管理](/help/authentication/dynamic-client-registration-management.md)


#### 新增/刪除網域 {#add-delete-domains}

若要啟動為所選管道新增網域的程式，您需要按一下「網域」清單下方的「新增網域」按鈕。 這將建立一個新的網域專案，您可以在其中指定網域名稱。 如果網域清單中已存在較通用的網域，則不應新增子網域。

![新增網域至選取的管道區段](assets/add-domain-to-channel-sec.png)

*圖：管道中的「網域」索引標籤*

### 程式設計師 {#tve-db-programmers-section}

此區段可讓您檢視和編輯可用程式設計人員的設定或建立新設定。 按一下其中一個可用的程式設計人員將傳回包含以下標籤的畫面：

* **程式設計師資料**
   * **程式設計師ID**  — 我們系統中使用的程式設計師唯一id。
   * **顯示名稱**  — 程式設計師的商業名稱。
   * **標誌Url**  — 程式設計師的商業標誌統一資源定位器(URL)。
   * **標誌預覽**  — 程式設計師的商業標誌預覽，可從上述統一資源定位器(URL)下載。

* **憑證**

   包含驗證流程中使用的憑證清單，以及它們的發行組織、發行日期和到期日。 這些憑證可作為私人/公開金鑰，並用於驗證用途。

* **頻道**

   包含屬於此特定程式設計師的管道清單。 按一下特定專案，即可導覽至管道區段。

* **註冊的應用程式**

   包含應用程式註冊清單。 如需詳細資訊，請參閱 [動態使用者端註冊管理](/help/authentication/dynamic-client-registration-management.md).

* **自訂配置**

   包含自訂配置清單。 如需詳細資訊，請參閱 [iOS/tvOS應用程式註冊](/help/authentication/iostvos-application-registration.md) 和 [動態使用者端註冊管理](/help/authentication/dynamic-client-registration-management.md).


### 整合 {#tve-db-integrations-sec}

此區段可讓您檢視及編輯頻道與可用MVPD之間整合的設定，或建立新設定。 使用基本工作區時，按一下其中一個可用整合將會傳回單一頁面，或使用進階工作區時，則會傳回包含以下索引標籤的畫面：

* **整合資料**
   * **整合ID** — 將MVPD的唯一ID附加至以「_」字元分隔的管道唯一ID的結果。
   * **頻道顯示名稱**  — 頻道的商業名稱。
   * **管道Id**  — 我們系統中使用的管道唯一ID，也稱為「請求者ID」。
   * **MVPD顯示名稱** - MVPD的商業名稱。
   * **MVPD Id**  — 我們系統中使用的MVPD唯一ID。
* **一般設定**
   * **使用者中繼資料索引鍵**  — 設定可用於特定整合的中繼資料索引鍵。
   * **平台特定設定**  — 為特定平台設定不同的設定（例如TTL、SSO和IFrames）。

* **驗證設定**
   * 包含與Adobe Primetime驗證功能相關的設定。
* **授權設定**
   * 包含與Adobe Primetime驗證授權功能相關的設定。
* **登出設定**
   * 包含與Adobe Primetime驗證登出功能相關的設定。

#### 建立整合 {#create-integration}

若要建立新的整合，請遵循下列步驟：

* 按一下「新增整合」按鈕
* 搜尋並選取頻道
* 搜尋並選取MVPD
* 等候TVE儀表板計算「整合ID」並顯示可用的MVPD端點
* 選取驗證、授權和登出端點，或使用預設值
* 按一下「建立整合」按鈕
* 視MVPD設定而定，會出現快顯視窗並要求其他屬性，這些屬性應已由MVPD預先提供，否則將重新導向至新建立的整合頁面

![](assets/new-integration-window.png)



*圖5. Adobe Primetime TVE儀表板新整合視窗*


#### 更新整合 {#update-integration}

若要更新現有的整合，請從「整合」區段或包含「整合」索引標籤的「管道」區段，按一下該特定整合的表格專案。

使用基本工作區模式時，本節將允許檢視及編輯最常更新的設定，例如驗證和授權權杖TTL （存留時間）以及iFrame設定。 請記住，與支援動態定義權杖持續性TTL的MVPD的整合可能會遺失TTL設定(請參閱中的專案1.19 [MVPD整合需求](/help/authentication/mvpd-integr-features.md))。



使用進階工作區模式時，此區段將允許檢視及編輯較不常見的設定。



在基本和進階工作區模式中，這些設定可在平台層級變更（例如，為Android上的授權TTL權杖選取自訂值，在所有其他平台上預設值）。



>[!IMPORTANT]
>請務必瞭解設定繼承鏈： MVPD -> MVPD端點 — >整合 — > Platform，其中Platform具有最特定的值，而MVPD是最一般的預設值。

![](assets/inheritance-chain-component.png)


*圖6. Adobe Primetime TVE儀表板屬性繼承鏈元件*


#### 平台特定設定 {#platform-sp-settings}

此子區段可用於覆寫特定平台的設定。 可用的平台包括：

* **所有平台**  — 設定將套用至所有平台的值，不論程式設計人員實施為何，以防沒有針對特定平台設定的其他值。
* **Android**  — 設定將套用至Adobe Primetime Authentication Android SDK上程式設計人員實作的值。
* **無使用者端REST API**  — 設定將套用至程式設計人員實作(透過Adobe Primetime驗證REST API)的值。
* **Fire TV**  — 設定將套用至Adobe Primetime Authentication FireTV SDK上程式設計人員實作的值。
* **FLASHSDK**  — 此平台已淘汰。 **已棄用**
* **JavaScript SDK**  — 設定將套用至Adobe Primetime Authentication JavaScript SDK上程式設計人員實作的值。
* **Roku**  — 設定將透過Adobe Primetime Authentication REST API套用至程式設計人員實作，且以裝置型別傳送「Roku」的值。 在Roku裝置的情況下，優先於為無使用者端REST API平台設定的值。
* **Xbox原生SDK**  — 此平台已淘汰。 **已棄用**
* **Xbox 360 REST API**  — 設定將透過Adobe Primetime驗證REST API套用至程式設計人員實作，以及傳送「xbox」作為裝置型別的值。 在Xbox 360裝置的情況下，這會優先於為Clienless REST API平台設定的值。
* **Xbox One REST API**  — 設定將透過Adobe Primetime Authentication REST API套用至程式設計人員實作，以及傳送「xboxOne」作為裝置型別的值。 在XboxOne裝置的情況下，這會優先於為Clienless REST Api平台設定的值。
* **iOS**  — 設定將套用至Adobe Primetime Authentication iOS SDK上程式設計人員實作的值。
* **tvOS**  — 設定將套用至Adobe Primetime Authentication tvOS SDK上程式設計人員實作的值。


![](assets/platform-sp-settings.png)

*圖7. Adobe Primetime TVE儀表板平台專屬設定*


#### 啟用平台單一登入 {#enable-platform-sso}

請依照下列步驟，為特定整合和平台啟用/停用單一登入：

* 請確定您使用的是進階工作區模式
* 導覽至所需的整合
* 導覽至 **一般設定** 標籤
* 選取您要啟用或停用單一登入的所需平台
* 切換 **啟用單一登入** 標幟為所要的值（是/否）

   >[!IMPORTANT]
   >請務必注意 **啟用單一登入** 標幟僅適用於iOS、tvOS、Roku和FireTV平台，且僅適用於與在這些平台上支援單一登入的MVPD整合。

* 切換 **強制執行平台許可權** 標幟為所要的值（是/否）

   >[!IMPORTANT]
   >請務必注意 **強制執行平台許可權** 標幟控制是否將強制執行使用者允許或拒絕平台存取其電視提供者訂閱的決策。 考慮以下情況 **啟用單一登入** 標幟設為「是」， **強制執行平台許可權** 標幟也設為「是」，且使用者選擇拒絕平台存取其電視提供者訂閱，則個別應用程式（頻道）將無法使用其他應用程式（頻道）取得的Adobe Primetime驗證權杖。


#### 啟用以家庭為基礎的驗證 {#enable-hba}

請依照下列步驟，為啟用/停用Home-Base驗證 **OAuth2** 根據MVPD：

* 請確定您使用的是進階工作區模式
* 導覽至所需的整合
* 導覽至 **驗證設定** 標籤
* 導覽至 **AuthN動態規則** 子標籤
* 切換 **嘗試HBA** 標幟為所要的值（是/否）


>[!IMPORTANT]
>請記住，「HBA AuthN TTL」值絕不可覆寫，否則授權流程可能會意外失敗。

請聯絡 **tve-support@adobe.com** 以取得為以SAML為基礎的MVPD啟用Home-Base Authentication的相關資訊。

### MVPDs {#tve-db-mvpds-sec}

此區段允許檢視可用MVPD的設定。 按一下其中一個可用的MVPD會傳回含有下列標籤的畫面：

* **MVPD資料**
   * **MVPD Id**  — 我們系統中使用的MVPD唯一ID。
   * **顯示名稱** - MVPD的商業名稱，可用於使用者的選擇器。
   * **標誌Url** - MVPD的商業標誌統一資源定位器(URL)。
   * **標誌預覽** - MVPD的商業標誌預覽，可從上述統一資源定位器(URL)下載。
* **一般設定**
   * **使用者中繼資料索引鍵**
      * 適用於特定MVPD的中繼資料索引鍵。
   * **使用者端資料屬性**
      * **驗證/彙總**  — 如果設為「是」，則使用者嘗試存取的每個新管道都需要新的驗證權杖。
      * **被動驗證已啟用**  — 如果Auth / Aggregator旗標設為「是」，且Passive AuthN Enabled設為「是」，則背景中將發生使用其他頻道的驗證程式，而不需要完整的瀏覽器重新導向和顯示選擇器。
      * **驗證/瀏覽器工作階段**  — 如果設為「是」，則使用者將在關閉瀏覽器後登出。 如果設為「否」，則使用者可以重新啟動瀏覽器並保持登入。
      * **需要IFrame**  — 若設為「是」，則表示MVPD登入視窗需要iFrame。 「iFrame寬度」和「iFrame高度」欄位代表iFrame載入MVPD登入頁面所需的大小。
* **驗證設定**
   * **選取端點**
      * 此欄位會指出MVPD公開的驗證端點。 端點可能會因使用的驗證通訊協定而異。
   * **AuthN一般設定**
      * 此子頁簽會顯示MVPD使用的驗證通訊協定和通訊協定相關資訊。
   * **AuthN憑證**
      * 此子索引標籤會顯示MVPD在驗證流程中使用的憑證，以及其簽發者組織、發行日期和到期日。 這些憑證可作為私人/公開金鑰，並用於驗證用途。
   * **AuthN動態規則**
      * 此子標籤會顯示套用至驗證程式的規則。 按下圖表的「請求/回應/代號」時，您可以看到反白顯示套用至驗證流程該部分的引數。
* **授權設定**
   * **選取端點**
      * 此欄位會指出MVPD公開的授權端點。 端點可能會因使用的授權通訊協定而異。 可用的授權通訊協定有SOAP、REST （適用於無使用者端裝置）、SAML、XACML和OAUTH。
   * **AuthZ一般設定**
      * 此子頁簽會顯示MVPD使用的授權通訊協定和通訊協定相關資訊。
      * **預檢設定**
         * 它說明在一次呼叫中MVPD可預先授權的資源數量、使用的PreFlight模型，以及逾時臨界值。 有時，特定整合的資源數量可能會不同。 可透過編輯&quot;**預檢資源的最大數量**」屬性，可在「一般設定」標籤下使用。 此屬性僅適用於指定的整合，且若設定此屬性，將會取代授權設定 — > PreFlight設定 — > PreFlight最大資源中定義的值。
      * **DOS保護**
         * 它說明MVPD授權端點上的拒絕服務保護。 如需每個欄位的確切說明，請將游標停留在DOS保護欄位上以檢視工具提示。
      * 如果MVPD是 **暫時傳遞**，然後 **AuthZ一般設定** 也包含有關TempPass持續時間的資訊。
      * 如果MVPD是 **FlexibleTempPass**，然後 **AuthZ一般設定** 也包含有關TempPass持續時間、資源最大數量和識別欄位的資訊（請參閱下圖）。
   * **AuthZ憑證**
      * 此子索引標籤會顯示MVPD在授權流程中使用的憑證，以及其簽發者組織、發行日期和到期日。 這些憑證可作為私人/公開金鑰，並用於驗證用途。
   * **AuthZ動態規則**
      * 此子頁簽會顯示適用於授權程式的規則。 按下圖表的 **請求/回應/權杖**，您會看到醒目提示套用至該授權流程部分的引數。
* **登出設定**
   * **選取端點**
      * 此欄位會指出MVPD公開的登出端點。 提供的通訊協定可以是SAML或OAuth2。
      * **登出一般設定**
         * 此子頁簽會顯示MVPD使用的登出通訊協定和通訊協定相關資訊。
         * **需要簽署的登出回應**  — 如果設為「是」，則回應必須由受信任的憑證簽署。
      * **登出憑證**
         * 此子索引標籤會顯示MVPD在登出流程中使用的憑證，以及其簽發者組織、發行日期和到期日。 這些憑證可作為私人/公開金鑰，並用於驗證用途。
      * **登出動態規則**
         * 此子標籤會顯示適用於登出程式的規則。 按下圖表的 **請求/回應/權杖**，您會看到反白顯示套用至該部分登出流程的引數。

### 報表 {#tve-db-reports-sec}

若要導覽至本節，請按一下「[儀表板區段](#sections)「 」功能表。 這會導覽至包含3個索引標籤的畫面，下列子區段將詳細顯示該畫面： [AuthN TTL報表](#authn-ttl-reports)， [AuthZ TTL報表](#authz-ttl-reports)， [SSO報告](#sso-reports).

此區段可讓您檢視和匯出多種型別報表的彙總資料，以便您在所有平台上整合各種MVPD的管道。

#### 平台 {#report-platforms}

所有報表都會彙總下列平台中的值：

**瀏覽器**
顯示將套用至Adobe Primetime Authentication JavaScript SDK上程式設計人員實作的值。

**行動： IOS**
顯示將套用至Adobe Primetime Authentication iOS SDK上程式設計人員實作的值。

**行動裝置：ANDROID**
顯示將套用至Adobe Primetime Authentication Android SDK上程式設計人員實作的值。

**行動：其他**
顯示將套用至程式設計人員實作的值(透過為行動裝置開發的Adobe Primetime Authentication REST API)。

**TVCD： ROKU**
顯示將透過Adobe Primetime Authentication REST API套用至程式設計人員實作的值，以及將「Roku」作為裝置型別傳送的值。

**TVCD： FIRETV**
顯示將套用至Adobe Primetime Authentication FireTV SDK上程式設計人員實作的值。

**TVCD： APPLETV**
顯示將套用至Adobe Primetime Authentication tvOS SDK上程式設計人員實作的值。

**TVCD：其他**
顯示將套用至程式設計人員實作的值(透過為電視連線裝置開發的Adobe Primetime Authentication REST API)。

**平台：未知**
顯示將套用至Adobe Primetime驗證服務偵測到未知裝置型別的程式設計人員實作的值。

檢閱的機制 [傳遞使用者端資訊](/help/authentication/passing-client-information-device-connection-and-application.md) 至Adobe Primetime驗證REST API或SDK，以取得有關如何傳送所需裝置型別（例如「Roku」）的詳細資訊。

所有報表彙總值是根據每個Adobe Primetime驗證環境的特定設定計算而得。 因此，在不同的TVE儀表板環境之間切換時，您可以預期不同的報表資料。

請檢閱 [環境](#authn-environments) 區段，以瞭解與Adobe Primetime驗證可用環境相關的更多詳細資料。


##### 選取特定通道/ MVPD {#selecting-specific-channels-mvpds}

所有報表都可透過選取特定通道或選取要包含在結果報表中的特定MVPD來允許使用篩選器。

若要選取一個或多個管道，請使用 **下拉式清單** 置於「為報表選取的管道」標籤之後。 請參閱圖8。/9./10. 下方影像數。

若要選取一或多個MVPD，請使用 **下拉式清單** 置於「為報表選取的MVPD」標籤之後。 請參閱圖8。/9./10. 下方影像數。

依預設，資料會在貴公司的所有頻道（「所有頻道」）與其整合的MVPD（「所有MVPD」）中進行彙總。

如果您選擇取消選取「所有頻道」或「所有MVPD」而未選擇特定選項，UI將顯示「沒有可用的資料」預留位置。


##### 匯出報告 {#export-report}

所有報表都允許匯出逗號分隔值(CSV)格式檔案的資料。

若要匯出資料，請使用置於視窗右上角的「匯出報告」按鈕。 請參閱圖8。/9./10. 下方影像數。

名為的檔案 **Report.csv** 將會自動下載到您的電腦。 因此，請確定您的瀏覽器設定允許下載檔案。

計算Report.csv檔案時，「匯出資料」載入圖示會出現在畫面上，這可能要用上 **到幾分鐘** 視您要匯出的資料大小而定。

#### AuthN TTL報表(#authn-ttl-reports)

此報表顯示針對您管道整合而設定的驗證Token與所有平台上的各種MVPD的存留時間(TTL)。

驗證Token存留時間，也稱為 **驗證TTL**，會以人類可讀的值顯示，例如： **天、小時、分鐘、秒**.

就使用者體驗而言，AuthN TTL報表可讓您根據特定MVPD和特定平台，以視覺化方式檢查使用者驗證的時間長度。

若要導覽至此型別的報表，請按一下「報表」區段中的「驗證TTL報表」索引標籤。

![AuthN TTL報表](assets/authn-ttl-reports.png)

*圖8： Adobe Primetime TVE控制面板驗證TTL報告標籤*

「AuthN TTL報表」表格包含頁面，並可依據熒幕大小進行水平和垂直捲動。

如果您考慮變更AuthN TTL值，請檢閱 [整合](#tve-db-integrations-sec) 區段。

>[!IMPORTANT]
>「**由MVPD設定**「預留位置用於MVPD會強制執行AuthN TTL值而非Adobe Primetime驗證設定的情況。


#### AuthZ TTL報表 {#authz-ttl-reports}

此報表顯示針對您管道整合而設定的授權權杖的存留時間(TTL)，以及所有平台上的各種MVPD。

授權權杖存留時間，也稱為 **AuthZ TTL**，會以人類可讀的值顯示，例如： **天、小時、分鐘、秒**.

就使用者體驗而言，AuthZ TTL報表可讓您透過視覺化方式，檢查使用者在考慮特定MVPD和特定平台後獲得授權的時間長度。

若要導覽至此型別的報告，請按一下「報告」區段中的「AuthZ TTL報告」索引標籤。

![AuthZ TTL報表](assets/authz-ttl-reports.png)

*圖9. Adobe Primetime TVE控制面板AuthZ TTL報告標籤*

「AuthZ TTL報表」表格包含頁面，並可依據熒幕大小進行水平和垂直捲動。

如果您考慮變更AuthZ TTL值，請參閱 [整合](#tve-db-integrations-sec) 區段。

>[!IMPORTANT]
>「**由MVPD設定**「預留位置用於MVPD會強制執行AuthZ TTL值而非Adobe Primetime驗證設定的情況。


#### SSO報告 {#sso-reports}

此報表顯示針對您管道與所有平台之各種MVPD的整合所設定的「單一登入」(SSO)狀態。

「單一登入」狀態，也稱為 **SSO狀態**，會顯示為tri-state ，其可能值如下： **SSO停用、SSO啟用、SSO不確定**.

就使用者體驗而言，SSO報告可讓您檢視預期的使用者驗證SSO體驗，並考量特定MVPD和特定平台。

若要導覽至此型別的報告，請按一下「**SSO報告**「 」標籤來自「**報表**「 」區段。


![TVE儀表板SSO報告標籤](assets/sso-reports.png)


*圖10： Adobe Primetime TVE控制面板SSO報告標籤*

「SSO報表」表格包含頁面，並可依據熒幕大小進行水平和垂直捲動。

如果您考慮變更SSO狀態，請檢閱 [整合](#tve-db-integrations-sec) 區段。

>[!IMPORTANT]
>&quot;**SSO不確定**「預留位置用於已啟用且可能使用SSO的情況，但使用者平台設定/使用者決定（例如封鎖第三方Cookie的使用者瀏覽器選項、使用者選擇拒絕平台存取其電視提供者訂閱）或MVPD設定（例如MVPD要求每個頻道進行驗證）可能會導致SSO無法發生。

### 變更記錄 {#tve-db-changelog-sec}

此區段顯示透過TVE控制面板推送至Adobe Primetime驗證環境和設定的所有修改清單。

有些欄會指出推送日期、操作修改的使用者以及推送的狀態。

此區段也允許比較兩個表格專案，以縮小您要檢查的特定修改範圍，甚至將比較結果共用為郵件專案。

### 意見反應 {#tve-db-feedback-sec}

此區段可讓使用者傳送意見反應。 請依照下列步驟，向Adobe Primetime驗證產品團隊提供意見回饋：

* 按一下畫面右側的「意見回饋」按鈕
* 輸入主旨
* 輸入訊息
* 如有需要，請按一下「上傳熒幕擷圖」按鈕，將熒幕擷圖上傳至訊息
* 按一下「提交」按鈕

![儲存儀表板回饋意見表單](assets/tve-dashboard-feedback.png)

*圖11： Adobe Primetime TVE控制面板意見回饋區段*

如需如何擷取熒幕擷圖的指示，請檢視下列連結：

* [如何在Windows上擷取熒幕擷取畫面](https://support.microsoft.com/en-us/windows/use-snipping-tool-to-capture-screenshots-00246869-1843-655f-f220-97299b865f6b#1TC=windows-7)

* [如何在Mac上擷取熒幕擷取畫面](https://support.apple.com/en-us/HT201361)

## 疑難排除 {#tve-db-troubleshoot}

### 維護模式 {#maintenance-mode}

![處於維護模式的TVE應用程式](assets/tveapp-maintenance-mode.png)


*圖：處於維護模式的TVE應用程式*


如果TVE儀表板處於「維護模式」，那麼使用者將無法檢視或進行新的變更。

如果發生這種狀況，您必須等候Adobe Primetime驗證工程團隊完成TVE儀表板的維護工作。

### 降級狀態 {#degraded-state}

![TVE應用程式處於降級狀態](assets/tve-degraded-state.png)


*圖：TVE應用程式處於降級狀態*

如果TVE儀表板處於「降級狀態」，則使用者將缺乏搜尋和排序功能，但使用者將能夠檢視或進行新變更。

如果發生這種狀況，您必須等候Adobe Primetime驗證工程團隊完成TVE儀表板的維護工作。
