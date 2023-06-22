---
title: Dynamic Client註冊管理
description: Dynamic Client註冊管理
exl-id: 2c3ebb0b-c814-4b9e-af57-ce1403651e9e
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 0%

---

# Dynamic Client註冊管理 {#dynamic-client-registration-management}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 概觀 {#overview}

隨著廣泛採用 [Android Chrome自訂標籤](https://developer.chrome.com/multidevice/android/customtabs){target_blanck}和 [Apple Safari檢視控制器](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target_blanck}在客戶的應用程式中，我們正在更新Adobe Primetime驗證中的使用者驗證流程。 更具體地說，我們無法再達成維護狀態的目標，因此驗證MVPD訂閱者的使用者代理流程可以在重新導向之間受到追蹤。 此作業先前是使用HTTP Cookie完成。 此限制是開始將所有API移轉至OAuth 2.0的驅動程式 [RFC6749](https://tools.ietf.org/html/rfc6749){target_blanck}。

透過此更新，Adobe驗證使用者端成為OAuth 2.0使用者端，並部署自訂OAuth 2.0授權伺服器以滿足Adobe Primetime驗證服務的需求。

使用者端應用程式若要使用OAuth 2.0授權，伺服器必須動態註冊以取得特定資訊（使用者端憑證），才能與其互動。 在註冊程式中，使用者端必須向使用者端註冊端點提供一組內建的中繼資料。

此中繼資料以軟體陳述式傳達，其中包含「software_id」，可讓我們的授權伺服器使用相同的軟體陳述式來關聯應用程式的不同執行個體。

A **軟體宣告** 是JSON Web權杖(JWT)，會以套件形式插入有關使用者端軟體的中繼資料值。 當作為使用者端註冊請求的一部分呈交給授權伺服器時，軟體陳述式必須使用JSON Web簽名(JWS)進行數位簽署或MAC化。

您可以在官方檔案中找到軟體陳述式及其運作方式的詳細說明 [RFC7591](https://tools.ietf.org/html/rfc7591).

軟體陳述式應隨應用程式部署在使用者裝置上。

在此更新之前，我們有兩個機制可允許應用程式執行對Adobe Primetime驗證的呼叫：

* 瀏覽器型使用者端是透過允許進行註冊 [網域清單](/help/authentication/programmer-overview.md#reg-and-init)
* 原生應用程式使用者端(例如iOS和Android應用程式)的註冊方式 **已簽署的請求者** 機制


使用使用者端註冊授權機制，您必須將應用程式新增到TVE儀表板。

若要讓客戶開始實作新的Android SDK和即將推出的iOS SDK，他們需要軟體宣告。 軟體陳述式會識別在TVE儀表板中建立的應用程式。

請依照下列各節中的步驟，在TVE控制面板中建立「註冊的應用程式」。

## 建立註冊的應用程式 {#create_app}

在TVE控制面板中建立註冊應用程式的方法有兩種：

* [程式設計師層級](#prog-level)  — 可讓您建立已註冊的應用程式，並將其連結至任何或所有程式設計師管道。

* [頻道層級](#channel-level)  — 可讓您建立僅永久連結至此管道的已註冊應用程式。

### 在程式設計人員層級建立註冊的應用程式 {#prog-level}

前往 **程式設計師** > **註冊的應用程式** 標籤。

![](assets/reg-app-progr-level.png)

在「註冊的應用程式」標籤中，按一下 **新增應用程式**. 在新視窗中填寫必填欄位。

如下圖所示，您應填寫的欄位包括：

* **應用程式名稱**  — 應用程式的名稱

* **已指派至頻道**  — 您的頻道名稱，t</span>此應用程式連結到的目標。 下拉式清單遮色片中的預設設定為 **所有管道。** 介面可讓您選取一個通道或所有通道。

* **應用程式版本**  — 預設為「1.0.0」，但我們強烈建議您使用自己的應用程式版本加以修改。 最佳實務是，如果您決定變更應用程式的版本，請透過為其建立新的註冊應用程式來反映該版本。

* **應用程式平台**  — 要連結的應用程式平台。 您可以選擇選取所有或多個值。

* **網域名**  — 要連結的應用程式網域。 下拉式清單中的網域是統一選取您所有管道中的所有網域。 您可以選擇從清單中選取多個網域。 網域的含義是重新導向URL [RFC6749](https://tools.ietf.org/html/rfc6749). 在使用者端註冊程式中，使用者端應用程式可請求允許使用重新導向URL來最終確定驗證流程。 當使用者端應用程式要求特定的重新導向URL時，將會根據與此軟體陳述式關聯的已註冊應用程式中列出的網域進行驗證。


![](assets/new-reg-app.png)


在填入具有適當值的欄位後，您必須按一下「完成」，應用程式才能儲存在設定中。

請注意， **沒有可修改已建立應用程式的選項**. 如果發現已建立的某個專案不再符合需求，則需要建立新的註冊應用程式，並搭配其符合需求的使用者端應用程式使用。


### 在通路層級註冊新的應用程式 {#channel-level}

若要在管道層級建立註冊的應用程式，請導覽至「管道」功能表，然後選擇要為其建立應用程式的管道。 接著，在導覽至「註冊的應用程式」索引標籤後，按一下「新增應用程式」按鈕。

![](assets/reg-new-app-channel-level.png)

如下所示，與在程式設計人員層級執行的相同動作相比，這裡有些微差異，只是「指派的管道」下拉式清單未啟用，因此沒有選項可以將註冊的應用程式繫結到目前管道以外的其他管道。

![](assets/new-reg-app-channel.png)

## 列出應用程式 {#list-reg-app}

建立註冊的應用程式後，可以取得軟體陳述式，將授權伺服器呈現為請求的一部分。

您可以導覽至已建立註冊應用程式的程式設計師或頻道（會在其中列出這些應用程式）來完成此操作。 

如下圖所示，清單中的每個專案都將以其所繫結之平台的名稱、版本和符號來識別。

![](assets/reg-app-list.png)

您可以逐一執行下列動作：

* [檢視](#view)
* [下載軟體宣告](#download-statement)

### 檢視註冊的應用程式 {#view}

在應用程式清單中，選擇其中一個應用程式並按一下「檢視」按鈕，將顯示建立應用程式時使用的詳細資訊。 如前所述，沒有任何選項可修改任何內容。


![](assets/view-reg-app.png)


### 下載軟體宣告 {#download-statement}

按一下需要軟體陳述式之清單專案上的「下載」按鈕將會產生文字檔。 此檔案將包含類似於以下範例輸出的內容。


![](assets/download-software-statement.png)

以「software_statement」為前置詞並新增目前的時間戳記，可唯一識別檔案的名稱。

請注意，對於相同的註冊應用程式，每次按一下下載按鈕時都會收到不同的軟體陳述式，但這不會使先前為此應用程式取得的軟體陳述式失效。 發生此情況是因為它們是根據動作要求當場產生。

有一個 **限制** 下載動作的相關資訊。 如果在建立註冊的應用程式後不久按一下「下載」按鈕以請求軟體陳述式，而且此陳述式尚未儲存，且設定json未同步，則頁面底部會顯示下列錯誤訊息。 

![](assets/error-sw-statement-notready.png)

這會包裝從核心接收的HTTP 404 Not Found錯誤碼，因為已註冊應用程式的ID尚未傳播，而且核心並不知道它。

解決方案是在建立已註冊的應用程式後，最多等待2分鐘讓設定同步。 發生此情況後，將不會再收到錯誤訊息，且包含軟體陳述式的文字檔將可供下載。

如需端對端流程運作方式的詳細資訊，或深入瞭解執行要求的方式以及預期的回應，請參閱下文相關資訊中的連結，連同其他實用連結。

<!--
## Related Information {#related}

* [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
* [TVE Dashboard User Guide](/help/authentication/tve-dashboard-user-guide.md)
-->

## 功能示範 {#tutorial}

請觀看 [此網路研討會](https://my.adobeconnect.com/pzkp8ujrigg1/) 其中提供更多功能的內容，並包含如何使用TVE儀表板管理軟體陳述式，以及如何使用Adobe提供的示範應用程式來測試產生的陳述式（做為Android SDK的一部分）。
