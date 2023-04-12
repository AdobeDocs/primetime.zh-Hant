---
title: Primetime TVE儀表板使用手冊
description: Primetime TVE儀表板使用手冊
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4386'
ht-degree: 0%

---


# Primetime TVE儀表板使用手冊 {#tve-db-user-guide}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#tve-db-intro}

[[!DNL Adobe] TVE儀表板（TVE儀表板）](https://console.auth.adobe.com/) 是自助式控制面板，目標使用者為與Adobe Primetime驗證產品團隊有業務關係的媒體公司（程式設計人員）。

請連絡您的技術客戶經理(TAM)以取得存取權。 若要取得存取權，您需要在Adobe Marketing Cloud組織中設定兩個新的使用者群組：

* TVE儀表板讀寫 — 此組的成員對儀表板的所有可編輯部分具有完全權限
* TVE儀表板只讀 — 此組的成員在整個儀表板中僅具有查看權限


在深入了解本使用手冊之前，建議您先完成下列資源，以充分了解Adobe Primetime驗證產品團隊提供的流程和功能，並熟悉本檔案中使用的術語：

* [TVE技術檔案](/help/authentication/technical-paper.md)
* [程式設計師啟動指南](/help/authentication/programmer-kickstart-guide.md)
* [權利流程](/help/authentication/entitlement-flow.md)
* [字彙表](/help/authentication/glossary.md)


繼續閱讀本使用手冊的下一節，您將了解如何管理公司的「頻道」、「程式設計人員」或「頻道與MVPD之間的整合」（「多頻道視訊節目經銷商」）的不同設定。

>[!IMPORTANT]
>「TVE控制面板」提供在「基本」和「進階工作區」之間切換的選項。 您可以切換右上角的圖示來完成此操作。 進階工作區的對象是具備相當多技術知識，且對Adobe Primetime驗證產品團隊所提供功能有進階知識的使用者。

![TVE控制面板工作區](assets/tve-basic-advanced-workspace.png)

*圖1:Adobe Primetime TVE控制面板「基本/進階工作區」下拉式清單*

## 環境 {#authn-environments}

根據使用者可能需要完成的工作，他/她可能需要在Adobe Primetime驗證環境之間切換。 如需Adobe Primetime驗證環境的詳細資訊，請參閱下列檔案： [了解Adobe Primetime驗證環境](/help/authentication/understanding-the-adobe-environments.md).

TVE Dashboard提供了兩個名為「預先鑑定」和「發行」的環境，每個環境都有兩個名為「測試」和「生產」的配置檔案，如下所示：

* [預先測試](https://console-prequal.auth-staging.adobe.com/)
* [預先製作](https://console-prequal.auth.adobe.com/)
* [發行測試](https://console.auth-staging.adobe.com/)
* [發行生產](https://console.auth.adobe.com/)

若要在環境之間切換，使用者可以從下拉式元素中按一下項目所代表的所需環境：

![TVE控制面板環境下拉式清單](assets/tve-dashboard-env.png)

*圖2:Adobe Primetime TVE儀表板環境下拉式清單*

>[!IMPORTANT]
>請務必注意，當您透過TVE控制面板對Adobe Primetime驗證設定進行管理變更時，我們強烈建議您遵循下列順序，以確保功能正常。

要通過TVE儀表板對Adobe Primetime身份驗證配置進行管理更改，請執行以下操作：

* 在 [發行測試並驗證](http://sp.auth-staging.adobe.com/apitest/api.html).
* 在 [生產前並驗證](http://sp.auth-staging.adobe.com/apitest/api.html).
* 在 [發行生產環境並驗證](http://sp.auth-staging.adobe.com/apitest/api.html).

>[!IMPORTANT]
>為了讓管理變更上線，使用者必須選取側欄左下角顯示的按鈕，以導覽至「檢閱及推播變更」區段，才能檢閱變更、新增新建立變更的說明，並選取「推播設定」以確認設定更新。

![Tve控制面板檢閱推播通知](assets/tve-review-push-notifications.png)

*圖3:Adobe Primetime TVE控制面板檢閱與推播變更通知*

## 章節 {#sections}

為媒體公司工作的用戶（程式設計師）可以從邊欄訪問TVE儀表板的以下部分：

* **管道**  — 包含與內容提供者相關的設定
* **程式設計師**  — 包含與父組織相關的設定，這些設定聚合一個或多個 **管道**
* **整合**  — 包含與 **管道** 和 **MVPD**
* **MVPD**  — 包含與可用 **MVPD**
* **報表**  — 包含三種報表的匯總資料：AuthN TTL、AuthZ TTL、SSO
* **變更記錄**  — 包含應用於TVE儀表板配置的最新修改

![TVE儀表板節](assets/tve-dashboard-sections.png)

*圖4:「Adobe Primetime TVE儀表板」部分*

### 管道 {#tve-db-channels-section}

此部分允許查看和編輯可用通道的設定或建立新通道。 按一下其中一個可用的管道時，畫面會顯示下列索引標籤：

* **管道資料**
   * **管道Id**  — 我們系統中使用的管道唯一ID，也稱為「請求者ID」。
   * **顯示名稱**  — 頻道的商業名稱。
* **一般設定**
   * **Analytics設定**  — 設定要轉送至Adobe Analytics的Adobe Primetime驗證事件。 如需啟用此功能前需要如何設定報表套裝ID(RSID)的詳細資訊，請連絡Adobe。
* **憑證**

   包含驗證流中使用的證書清單及其發證組織、發證日期和到期日。 這些憑證可作為私密/公開金鑰，並用於驗證用途。
* **網域**

   包含個別管道將與Adobe Primetime驗證通訊的網域清單。
* **整合**

   包含與可用MVPD的整合清單，以及每個可能啟用或未啟用整合的狀態。 按一下特定項目即可導覽至整合頁面。
* **註冊的應用程式**

   包含應用程式註冊清單。 如需詳細資訊，請檢閱檔案 [動態客戶端註冊管理](/help/authentication/dynamic-client-registration-management.md).

* **自訂配置**

   包含自訂配置清單。 如需詳細資訊，請參閱 [iOS/tvOS應用程式註冊](/help/authentication/iostvos-application-registration.md) 和 [動態客戶端註冊管理](/help/authentication/dynamic-client-registration-management.md)


#### 新增/刪除網域 {#add-delete-domains}

若要啟動為所選管道新增新網域的程式，您必須按一下網域清單下方的「新增網域」按鈕。 這將建立一個新的域項，您可以在其中指定域名。 如果網域清單中已存在較通用的網域，則不應新增子網域。

![將新網域新增至選取的管道區段](assets/add-domain-to-channel-sec.png)

*圖：「網域」索引標籤*

### 程式設計師 {#tve-db-programmers-section}

此部分允許查看和編輯可用程式設計師的設定或建立新設定。 按一下可用的程式設計師之一將返回帶有以下頁簽的螢幕：

* **程式設計師資料**
   * **程式設計師ID**  — 程式設計師在我們系統中使用的唯一id。
   * **顯示名稱**  — 程式設計師的商業名稱。
   * **標誌Url**  — 程式設計師的商業標識統一資源定位器(URL)。
   * **標誌預覽**  — 程式設計師的商業標誌預覽，從上述統一資源定位器(URL)下載。

* **憑證**

   包含驗證流中使用的證書清單及其發證組織、發證日期和到期日。 這些憑證可作為私密/公開金鑰，並用於驗證用途。

* **管道**

   包含屬於此特定程式設計師的通道清單。 按一下特定項目即可導覽至「管道」區段。

* **註冊申請**

   包含應用程式註冊清單。 如需詳細資訊，請參閱 [動態客戶端註冊管理](/help/authentication/dynamic-client-registration-management.md).

* **自訂配置**

   包含自訂配置清單。 如需詳細資訊，請參閱 [iOS/tvOS應用程式註冊](/help/authentication/iostvos-application-registration.md) 和 [動態客戶端註冊管理](/help/authentication/dynamic-client-registration-management.md).


### 整合 {#tve-db-integrations-sec}

本節可供檢視及編輯「頻道」和可用MVPD之間整合的設定，或建立新的MVPD。 使用「基本工作區」時，按一下其中一項可用的整合會傳回單一頁面，或使用「進階工作區」時，按一下包含下列標籤的畫面：

* **整合資料**
   * **整合Id** — 將MVPD唯一ID附加至以「_」字元分隔之管道唯一ID的結果。
   * **頻道顯示名稱**  — 頻道的商業名稱。
   * **管道Id**  — 我們系統中使用的管道唯一ID，也稱為「請求者ID」。
   * **MVPD顯示名稱** - MVPD的商業名稱。
   * **MVPD Id**  — 我們系統中使用的MVPD唯一ID。
* **一般設定**
   * **使用者中繼資料索引鍵**  — 設定特定整合可用的中繼資料索引鍵。
   * **平台特定設定**  — 為特定平台（例如TTL、SSO和IFrame）設定不同的設定。

* **驗證設定**
   * 包含與Adobe Primetime驗證功能相關的設定。
* **授權設定**
   * 包含與Adobe Primetime驗證授權功能相關的設定。
* **註銷設定**
   * 包含與Adobe Primetime驗證登出功能相關的設定。

#### 建立整合 {#create-integration}

若要建立新整合，請遵循下列步驟：

* 按一下「新增整合」按鈕
* 搜尋並選取通道
* 搜尋並選取MVPD
* 等待TVE控制面板計算「整合ID」並顯示可用的MVPD端點
* 選擇驗證、授權和註銷終結點或使用預設值
* 按一下「建立整合」按鈕
* 視MVPD設定而定，彈出畫面可能會出現，並要求其他屬性（這些屬性應該是MVPD預先提供的），否則會重新導向至新建立的整合頁面

![](assets/new-integration-window.png)



*圖5. 「Adobe Primetime TVE儀表板新整合」窗口*


#### 更新整合 {#update-integration}

若要更新現有整合，請從整合區段或管道區段（包含整合標籤）按一下該特定整合的表格項目。

使用基本工作區模式時，此區段可讓您查看和編輯最常更新的設定，例如驗證和授權Token TTL（存留時間），以及iFrame設定。 請記得，整合支援動態定義代號永續性TTL的MVPD時，可能會遺失TTL設定(請參閱 [MVPD整合需求](/help/authentication/mvpd-integr-features.md))。



使用進階工作區模式時，此區段可允許查看和編輯較不常見的設定。



若是基本和進階工作區模式，則可在平台層級變更這些設定（例如，為Android上的授權TTL代號選取自訂值，其他平台均預設為）。



>[!IMPORTANT]
>請務必了解設定繼承鏈：MVPD -> MVPD端點 — >整合 — >平台，其中Platform具有最特定的值，而MVPD是最一般的預設值。

![](assets/inheritance-chain-component.png)


*圖6. Adobe Primetime TVE儀表板屬性繼承鏈元件*


#### 平台特定設定 {#platform-sp-settings}

此子區段可用來覆寫特定平台的設定。 可用平台包括：

* **所有平台**  — 設定將應用於所有平台的值，而不管程式設計師實施如何，以備沒有為特定平台設定其他值時使用。
* **Android**  — 設定將套用至Adobe Primetime Authentication Android SDK上程式設計師實作的值。
* **無客戶端REST API**  — 設定將應用於通過Adobe Primetime Authentication REST API實現的程式設計師實施的值。
* **Fire TV**  — 設定將套用至Adobe Primetime Authentication FireTV SDK上程式設計師實作的值。
* **FlashSDK**  — 已棄用此平台。 **已棄用**
* **JavaScript SDK**  — 設定將應用於Adobe Primetime Authentication JavaScript SDK上的程式設計師實施的值。
* **Roku**  — 設定將應用於通過Adobe Primetime Authentication REST API的程式設計師實施以及將「Roku」作為設備類型發送的值。 若為Roku裝置，此值優先於為無用戶端REST API平台設定的值。
* **Xbox原生SDK**  — 已棄用此平台。 **已棄用**
* **Xbox 360 REST API**  — 設定將應用於通過Adobe Primetime Authentication REST API以及將「xbox」作為設備類型發送的程式設計師實施的值。 在Xbox 360裝置的情況下，這優先於為無客戶端REST API平台設定的值。
* **Xbox One REST API**  — 設定將應用於通過Adobe Primetime Authentication REST API以及將「xboxOne」作為設備類型發送的程式設計師實施的值。 在XboxOne裝置中，此值優先於為無客戶端REST Api平台設定的值。
* **iOS**  — 設定要套用至Adobe Primetime Authentication iOS SDK上程式設計師實作的值。
* **tvOS**  — 設定將套用至Adobe Primetime Authentication tvOS SDK上程式設計師實作的值。


![](assets/platform-sp-settings.png)

*圖7. Adobe Primetime TVE儀表板平台特定設定*


#### 啟用Platform單一登入 {#enable-platform-sso}

請依照下列步驟，針對特定整合和平台啟用/停用單一登入：

* 請確定您使用進階工作區模式
* 導覽至所需的整合
* 導覽至 **一般設定** 標籤
* 選取您要啟用或停用單一登入的平台
* 切換 **啟用單一登入** 標幟至所需值（是/否）

   >[!IMPORTANT]
   >請務必注意， **啟用單一登入** 標幟僅適用於iOS、tvOS、Roku和FireTV平台，且僅適用於與支援這些平台「單一登入」之MVPD的整合。

* 切換 **強制平台權限** 標幟至所需值（是/否）

   >[!IMPORTANT]
   >請務必注意， **強制平台權限** 標幟會控制使用者是否將強制執行「允許」或「拒絕」平台存取其電視提供者訂閱的決定。 考量情況，當 **啟用單一登入** 標幟設為「是」， **強制平台權限** 標幟也設為「是」，且使用者選擇拒絕平台存取其電視提供者訂閱，則個別應用程式（頻道）將無法使用其他應用程式（頻道）取得的Adobe Primetime驗證Token。


#### 啟用基於首頁的身份驗證 {#enable-hba}

請按照以下步驟啟用/禁用 **OAuth2** 基於MVPD:

* 請確定您使用進階工作區模式
* 導覽至所需的整合
* 導覽至 **驗證設定** 標籤
* 導覽至 **AuthN動態規則** 子標籤
* 切換 **嘗試HBA** 標幟至所需值（是/否）


>[!IMPORTANT]
>請記住，「HBA AuthN TTL」值絕不應被覆蓋，否則授權流可能會意外失敗。

伸手 **tve-support@adobe.com** 以取得為SAML型MVPD啟用首頁驗證的相關資訊。

### MVPD {#tve-db-mvpds-sec}

本節允許查看可用MVPD的設定。 按一下其中一個可用的MVPD會傳回具有下列標籤的畫面：

* **MVPD資料**
   * **MVPD Id**  — 我們系統中使用的MVPD唯一ID。
   * **顯示名稱** - MVPD的商業名稱，可能用於使用者的選擇器。
   * **標誌Url** - MVPD的商業標誌統一資源定位器(URL)。
   * **標誌預覽**  — 從上述統一資源定位器(URL)下載MVPD的商業標誌，以預覽其商業標誌。
* **一般設定**
   * **使用者中繼資料索引鍵**
      * 特定MVPD可用的中繼資料索引鍵。
   * **客戶端資料屬性**
      * **驗證/匯總器**  — 如果設為「是」，則使用者嘗試存取的每個新管道都需要新的驗證Token。
      * **已啟用被動驗證**  — 如果驗證/匯總標幟設為「是」，而被動式驗證啟用設為「是」，則背景會發生具有其他管道的驗證程式，而不需要完全瀏覽器重新導向，也不需要顯示選取器。
      * **驗證/瀏覽器工作階段**  — 如果設為「是」，則使用者在關閉瀏覽器後將登出。 如果設為「否」，則使用者可重新啟動瀏覽器並保持登入狀態。
      * **需要IFrame**  — 如果設為「是」，表示MVPD登入視窗需要iFrame。 「iFrame寬度」和「iFrame高度」欄位代表載入MVPD登入頁面的iFrame所需的大小。
* **驗證設定**
   * **選擇端點**
      * 此欄位指出MVPD公開的驗證端點。 端點會因使用的驗證協定而異。
   * **AuthN一般設定**
      * 此子頁簽顯示MVPD使用的驗證協定和協定相關資訊。
   * **AuthN憑證**
      * 此子標籤會顯示MVPD在驗證流程中使用的憑證，以及其核發組織、核發日期和到期日。 這些憑證可作為私密/公開金鑰，並用於驗證用途。
   * **AuthN動態規則**
      * 此子頁簽顯示適用於驗證進程的規則。 按圖表的「請求/回應/代號」 ，您就會看到反白顯示套用至驗證流程該部分的參數。
* **授權設定**
   * **選擇端點**
      * 此欄位表示MVPD公開的授權端點。 端點會因使用的授權通訊協定而異。 可用的授權通訊協定為SOAP、REST（適用於無用戶端裝置）、SAML、XACML和OAUTH。
   * **AuthZ一般設定**
      * 此子頁簽顯示MVPD使用的授權協定和協定相關資訊。
      * **預檢配置**
         * 它說明MVPD在單一呼叫中可預先授權的資源數、使用的PreFlight模型，以及逾時臨界值。 特定整合的資源數目有時可能不同。 您可以編輯「**預檢資源的最大數量**「屬性」，可在「一般設定」標籤下使用。 此屬性僅適用於指定的整合，如果設定，則將使用它，而非授權設定 — > PreFlight配置 — > PreFlight Max資源中定義的值。
      * **DOS保護**
         * 它描述了MVPD授權端點上的拒絕服務保護。 有關每個欄位的確切說明，請通過將游標移至DOS保護欄位上來查看工具提示。
      * 如果MVPD為 **TempPass**，則 **AuthZ一般設定** 也包含有關TempPass持續時間的資訊。
      * 如果MVPD為 **FlexibleTempPass**，則 **AuthZ一般設定** 也包含有關TempPass持續時間、最大資源數和標識欄位的資訊（請參見下圖）。
   * **AuthZ憑證**
      * 此子標籤會顯示MVPD在授權流程中使用的憑證，以及其核發組織、核發日期和到期日。 這些憑證可作為私密/公開金鑰，並用於驗證用途。
   * **AuthZ動態規則**
      * 此子頁簽顯示適用於授權進程的規則。 按圖表上的 **請求/回應/代號**，您可以看到醒目提示，指出套用至授權流程該部分的參數。
* **註銷設定**
   * **選擇端點**
      * 此欄位表示MVPD公開的登出端點。 提供的通訊協定可以是SAML或OAuth2。
      * **註銷常規設定**
         * 此子頁簽顯示MVPD使用的註銷協定和協定相關資訊。
         * **要求註銷響應已簽名**  — 如果設為「是」，則響應必須由受信任的證書籤名。
      * **註銷證書**
         * 此子頁簽顯示MVPD在註銷流程中使用的證書及其頒發機構、頒發日期和到期日。 這些憑證可作為私密/公開金鑰，並用於驗證用途。
      * **註銷動態規則**
         * 此子頁簽顯示適用於註銷過程的規則。 按圖表上的 **請求/回應/代號**，您可以看到醒目提示，指出套用至登出流程該部分的參數。

### 報表 {#tve-db-reports-sec}

若要導覽至本區段，請按一下[控制面板區段](#sections)」菜單。 這會導覽至含有3個標籤的畫面，其將在下列子區段中詳細說明： [驗證N TTL報表](#authn-ttl-reports), [AuthZ TTL報表](#authz-ttl-reports), [SSO報表](#sso-reports).

本節可讓您檢視並匯出數種報表的匯總資料，以供所有平台上具有各種MVPD的管道/s整合使用。

#### 平台 {#report-platforms}

所有報表會匯總下列平台中的值：

**瀏覽器**
顯示將應用於通過Adobe Primetime Authentication JavaScript SDK實現的程式設計師實施的值。

**行動：iOS**
顯示將應用於通過Adobe Primetime Authentication iOS SDK實現的程式設計師實施的值。

**行動：ANDROID**
顯示將應用於通過Adobe Primetime Authentication Android SDK實現的程式設計師實施的值。

**行動：其他**
顯示將應用於針對移動設備開發的Adobe Primetime Authentication REST API上的程式設計師實施的值。

**TVCD:ROKU**
顯示將應用於通過Adobe Primetime Authentication REST API實現的程式設計師實施以及將「Roku」作為設備類型發送的值。

**TVCD:FIRETV**
顯示將應用於Adobe Primetime Authentication FireTV SDK上的程式設計師實施的值。

**TVCD:APPLETV**
顯示將套用至Adobe Primetime Authentication tvOS SDK上程式設計師實作的值。

**TVCD:其他**
顯示將應用於針對TV連接設備開發的Adobe Primetime Authentication REST API上的Programmer實施的值。

**平台：未知**
顯示將應用到Programmer實施的值，其中Adobe Primetime Authentication Services檢測未知的設備類型。

回顧 [傳遞用戶端資訊](/help/authentication/passing-client-information-device-connection-and-application.md) 至Adobe Primetime Authentication REST API或SDK，以取得如何傳送所需裝置類型（例如「Roku」）的詳細資訊。

所有報表都會根據每個Adobe Primetime驗證環境專屬的設定來計算匯總值。 因此，在不同TVE儀表板環境之間切換時，您可以預期不同的報告資料。

請查看 [環境](#authn-environments) 一節，以取得與Adobe Primetime Authentication可用環境相關的詳細資訊。


##### 選取特定通道/ MVPD {#selecting-specific-channels-mvpds}

所有報表皆可選取特定頻道或選取要納入產生報表的特定MVPD，以使用篩選器。

若要選擇一個或多個通道，請使用 **下拉清單** 放在「為報表選取的管道」標籤後。 請參見圖8。/9./10. 影像。

若要選取一或多個MVPD/s，請使用 **下拉清單** 放在「為報表選取的MVPD」標籤後面。 請參見圖8。/9./10. 影像。

依預設，資料會匯總至您公司的所有管道（「所有管道」），以及整合這些管道的MVPD（「所有MVPD」）。

如果您選擇取消選取「所有頻道」或「所有MVPD」，而未選擇特定選項，UI會顯示「無可用資料」預留位置。


##### 匯出報表 {#export-report}

所有報表皆允許匯出逗號分隔值(CSV)格式檔案中的資料。

若要匯出資料，請使用視窗右上角的「匯出報表」按鈕。 請參見圖8。/9./10. 影像。

名為的檔案 **Report.csv** 會自動下載到您的電腦。 因此，請確定您瀏覽器的設定允許下載檔案。

計算Report.csv檔案時，畫面上會顯示「匯出資料」載入圖示，這需要 **幾分鐘** 取決於您要匯出的資料大小。

#### AuthN TTL報表(#authn-ttl-reports)

此報表會顯示為您的通道整合所設定的驗證Token的存留時間(TTL)，以及所有平台上各種MVPD。

驗證Token Time-To-Live，也稱為 **AuthN TTL**，會顯示在人類可讀的值中，例如： **天，小時，分鐘，秒**.

根據使用者體驗，AuthN TTL報表可讓您透過視覺化方式檢查使用者在考慮特定MVPD和特定平台時進行驗證的時間長度。

若要導覽至此類型的報表，請按一下「報表」區段中的「驗證TTL報表」標籤。

![AuthN TTL報表](assets/authn-ttl-reports.png)

*圖8:Adobe Primetime TVE控制面板驗證TTL報表標籤*

「AuthN TTL報表」表格包含頁面，且可依螢幕大小水準和垂直捲動。

如果您考慮變更AuthN TTL值，請檢閱 [整合](#tve-db-integrations-sec) 區段。

>[!IMPORTANT]
>「**由MVPD設定**「預留位置」用於當MVPD會強制執行AuthN TTL值，而非Adobe Primetime驗證設定時。


#### AuthZ TTL報表 {#authz-ttl-reports}

此報表會顯示為您的通道整合所設定的授權Token的存留時間(TTL)，以及所有平台上各種MVPD。

授權代號Time-To-Live，也稱為 **AuthZ TTL**，會顯示在人類可讀的值中，例如： **天，小時，分鐘，秒**.

根據使用者體驗，AuthZ TTL報表可讓您透過視覺化方式檢查使用者在考慮特定MVPD和特定平台時獲得授權的時間長度。

若要導覽至此類型的報表，請按一下「報表」區段中的「AuthZ TTL報表」標籤。

![AuthZ TTL報表](assets/authz-ttl-reports.png)

*圖9. Adobe Primetime TVE控制面板驗證Z TTL報表標籤*

AuthZ TTL報表表格包含頁面，且可依螢幕大小水準和垂直捲動。

如果您考慮變更AuthZ TTL值，請參閱 [整合](#tve-db-integrations-sec) 區段。

>[!IMPORTANT]
>「**由MVPD設定**「預留位置」用於MVPD會強制執行AuthZ TTL值，而非Adobe Primetime驗證設定的情況。


#### SSO報表 {#sso-reports}

此報表顯示為管道/s整合所設定的單一登入(SSO)狀態，以及所有平台上各種MVPD。

單一登入狀態，亦稱為 **SSO狀態**，會以三態顯示，並具有下列可能的值： **SSO已禁用、SSO已啟用、SSO不確定**.

就使用者體驗而言，SSO報表可讓您考量特定MVPD和特定平台，以視覺化方式檢查預期的使用者驗證SSO體驗。

若要導覽至此類型的報表，請按一下&#x200B;**SSO報表**&quot;頁簽&#x200B;**報表**」部分。


![TVE儀表板SSO報表頁簽](assets/sso-reports.png)


*圖10:Adobe Primetime TVE控制面板SSO報表標籤*

「SSO報表」表格包含頁面，且可依螢幕大小水準和垂直捲動。

如果您考慮變更SSO狀態，請檢閱 [整合](#tve-db-integrations-sec) 區段。

>[!IMPORTANT]
>&quot;**SSO不確定**「在啟用SSO且可能的情況下，會使用預留位置，但使用者平台設定/使用者決策（例如，封鎖第三方Cookie的使用者瀏覽器選項、使用者選擇拒絕平台存取其電視提供者訂閱）或MVPD設定（例如，要求對每個頻道進行驗證的MVPD）可能會阻止SSO的發生。

### 變更記錄 {#tve-db-changelog-sec}

本節顯示透過TVE控制面板推送至Adobe Primetime驗證環境和設定的所有修改清單。

有些欄會指出推播日期、執行修改的使用者以及推播的狀態。

此部分還允許比較兩個表條目，以縮小要檢查的特定修改範圍，甚至將比較作為郵件項共用。

### 意見反應 {#tve-db-feedback-sec}

本節可讓使用者傳送意見。 請依照下列步驟，向Adobe Primetime Authentication產品團隊提供意見反應：

* 按一下畫面右側的「意見回饋」按鈕
* 輸入主題
* 輸入消息
* 如果需要，請按一下「上傳螢幕截圖」按鈕，將螢幕截圖上傳到消息
* 按一下「提交」按鈕

![儀表板反饋表](assets/tve-dashboard-feedback.png)

*圖11:Adobe Primetime TVE儀表板反饋部分*

如需擷取螢幕擷取畫面的指示，請檢視下列連結：

* [如何在Windows上捕獲螢幕截圖](https://support.microsoft.com/en-us/windows/use-snipping-tool-to-capture-screenshots-00246869-1843-655f-f220-97299b865f6b#1TC=windows-7)

* [如何在Mac上擷取螢幕擷取畫面](https://support.apple.com/en-us/HT201361)

## 疑難排解 {#tve-db-troubleshoot}

### 維護模式 {#maintenance-mode}

![TVE應用程式在維護模式下](assets/tveapp-maintenance-mode.png)


*圖：TVE應用程式在維護模式下*


如果TVE儀表板處於「維護模式」，則用戶將無法查看或進行新更改。

如果發生這種情況，您必須等待Adobe Primetime驗證工程團隊在TVE儀表板上完成維護工作。

### 降級狀態 {#degraded-state}

![TVE應用程式處於降級狀態](assets/tve-degraded-state.png)


*圖：TVE應用程式處於降級狀態*

如果TVE儀表板處於「降級」狀態，則用戶將缺少搜索和排序功能，但用戶將能夠查看或進行新的更改。

如果發生這種情況，您必須等待Adobe Primetime驗證工程團隊在TVE儀表板上完成維護工作。
