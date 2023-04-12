---
title: Dynamic Client註冊管理
description: Dynamic Client註冊管理
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 0%

---


# Dynamic Client註冊管理 {#dynamic-client-registration-management}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#overview}

隨著 [Android Chrome自訂分頁](https://developer.chrome.com/multidevice/android/customtabs){target_blanck}和 [Apple Safari檢視控制器](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target_blanck}在客戶的應用程式中，我們正在更新Adobe Primetime驗證中的使用者驗證流程。 更具體地說，我們無法再達到維持狀態的目標，以便在重新導向之間追蹤驗證MVPD訂閱者的使用者代理流程。 此作業先前是使用HTTP Cookie完成。 此限制是開始將所有API移轉至OAuth 2.0的驅動程式 [RFC6749](https://tools.ietf.org/html/rfc6749){target_blanck}。

透過此更新，Adobe驗證用戶端會變成OAuth 2.0用戶端，且已部署自訂OAuth 2.0授權伺服器，以符合Adobe Primetime驗證服務的需求。

為了客戶端應用程式利用OAuth 2.0授權，伺服器必須動態註冊以獲取特定資訊（客戶端憑據），才能與其交互。 作為註冊過程的一部分，客戶端必須向客戶端註冊端點呈現一組內置元資料。

該元資料作為軟體語句傳送，該語句包含「software_id」，允許我們的授權伺服器使用相同的軟體語句將不同的應用程式實例關聯起來。

A **軟體語句** 是JSON Web Token(JWT)，它將用戶端軟體的中繼資料值聲明為套件。 當作為客戶端註冊請求的一部分向授權伺服器呈現時，必須使用JSON Web Signature(JWS)對軟體語句進行數字簽名或MACed。

您可以在官方檔案中找到更詳細的說明，說明哪些軟體陳述式及其運作方式 [RFC7591](https://tools.ietf.org/html/rfc7591).

軟體語句應與用戶設備上的應用程式一起部署。

在此更新前，我們提供兩種機制，讓應用程式執行對Adobe Primetime驗證的呼叫：

* 瀏覽器型用戶端可透過 [網域清單](/help/authentication/programmer-overview.md#reg-and-init)
* 原生應用程式用戶端(例如iOS和Android應用程式)會透過 **簽名請求者** 機構


使用「客戶端註冊授權」機制，必須將應用程式添加到TVE儀表板。

若要讓客戶開始實作新的Android SDK和即將推出的iOS SDK，他們需要軟體陳述式。 軟體語句標識在TVE儀表板中建立的應用程式。

按照以下各節中的步驟，在TVE儀表板中建立註冊應用程式。

## 建立註冊的應用程式 {#create_app}

在TVE儀表板中建立註冊應用程式有兩種方式：

* [程式設計人員級別](#prog-level)  — 允許您建立註冊應用程式，並將其連結到任何或所有程式設計師通道。

* [管道層級](#channel-level)  — 允許您建立一個永久連結到此渠道的註冊應用程式。

### 在程式設計師級別建立註冊的應用程式 {#prog-level}

前往 **程式設計師** > **註冊的應用程式** 標籤。

![](assets/reg-app-progr-level.png)

在「註冊的應用程式」頁簽中，按一下 **添加新應用程式**. 在新視窗中填寫必填欄位。

如下圖所示，您應填入的欄位為：

* **應用程式名稱**  — 應用程式的名稱

* **指派給管道**  — 管道名稱，t</span>此應用程式連結到的。 下拉式遮色片中的預設設定為 **所有通道。** 介面可讓您選取一個通道或所有通道。

* **應用程式版本**  — 預設情況下，此值會設為「1.0.0」，但強烈建議您使用自己的應用程式版本加以修改。 如果您決定更改應用程式的版本，最好通過為其建立新的註冊應用程式來反映它。

* **應用程式平台**  — 應用程式連結的平台。 您可以選擇全部或多個值。

* **網域名稱**  — 要連結的應用程式的網域。 下拉式清單中的網域是所有管道中所有網域的統一選取項目。 您可以選擇從清單中選取多個網域。 網域的含義是重新導向URL [RFC6749](https://tools.ietf.org/html/rfc6749). 在客戶端註冊過程中，客戶端應用程式可以請求允許使用重定向URL來最終定版驗證流。 當客戶端應用程式請求特定的重定向URL時，會根據與軟體語句關聯的此註冊應用程式中列出的白名域來驗證它。


![](assets/new-reg-app.png)


將適當的值填入欄位後，您必須按一下「完成」，才能將應用程式儲存在設定中。

請注意 **沒有選項可修改已建立的應用程式**. 如果發現已建立的物品不再滿足要求，則需要建立新的註冊應用程式，並將其與滿足要求的客戶應用程式一起使用。


### 在通道級別註冊新應用程式 {#channel-level}

要在渠道級別建立註冊應用程式，請導航至「渠道」菜單，並選擇要為其建立應用程式的渠道。 然後，導覽至「已註冊應用程式」標籤後，按一下「新增應用程式」按鈕。

![](assets/reg-new-app-channel-level.png)

如下所示，與在程式設計師級別執行的相同操作相比，此處稍有不同的是「已分配通道」下拉清單，該下拉清單未啟用，因此除了當前通道之外，沒有選項將註冊的應用程式綁定到其他通道。

![](assets/new-reg-app-channel.png)

## 列出應用程式 {#list-reg-app}

在建立註冊應用程式之後，有可能獲得軟體語句以將授權伺服器作為請求的一部分呈現。

可以通過導航到為其建立註冊應用程式的程式設計師或渠道，在渠道中列出註冊應用程式。 

如下所示，清單中的每個項目都將以其綁定到的平台的名稱、版本和符號來標識。

![](assets/reg-app-list.png)

您可以針對每個目標：

* [檢視](#view)
* [下載軟體語句](#download-statement)

### 查看註冊的應用程式 {#view}

在應用程式清單中，選擇其中一個應用程式並按一下「查看」按鈕，將顯示建立應用程式時使用的詳細資訊。 如前所述，沒有可修改任何內容的選項。


![](assets/view-reg-app.png)


### 下載軟體聲明 {#download-statement}

按一下需要軟體語句的清單條目上的「下載」按鈕將生成文本檔案。 此檔案將包含與以下範例輸出類似的內容。


![](assets/download-software-statement.png)

檔案的名稱會加上前置詞&quot;software_statement&quot;並新增目前時間戳記，以唯一識別。

請注意，對於同一註冊應用程式，每次按下下載按鈕時都會收到不同的軟體語句，但這不會使以前為此應用程式獲取的軟體語句無效。 之所以會發生此情況，是因為這些事件是根據動作要求即時產生。

有一個 **限制** 關於下載動作。 如果在建立註冊應用程式後不久按一下「下載」按鈕，要求提供軟體陳述式，但該語句尚未保存，且配置json未同步，則頁面底部將顯示以下錯誤消息。 

![](assets/error-sw-statement-notready.png)

這包含從核心收到的HTTP 404 Not Found錯誤碼，因為已註冊應用程式的ID尚未傳播，且核心不知道。

解決方案是在建立註冊應用程式後，最多等待2分鐘以同步配置。 發生此情況後，將不會再收到錯誤訊息，且將可下載包含軟體陳述式的文字檔。

如需端對端程式如何運作的詳細資訊，或若要深入了解請求的執行方式以及預期的回應，請參閱以下相關資訊中的連結，以及其他實用連結。

<!--
## Related Information {#related}

* [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
* [TVE Dashboard User Guide](/help/authentication/tve-dashboard-user-guide.md)
-->

## 功能示範 {#tutorial}

請看 [本網路研討會](https://my.adobeconnect.com/pzkp8ujrigg1/) 本課程提供功能的更多內容，並包含示範，說明如何使用TVE控制面板管理軟體陳述式，以及如何使用Adobe隨Android SDK提供的示範應用程式來測試產生的陳述式。
