---
title: iOS SDK 3.2+上的SFSafariViewController支援
description: iOS SDK 3.2+上的SFSafariViewController支援
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# iOS SDK 3.2+上的SFSafariViewController支援 {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>


**由於安全性要求，某些MVPD的登入頁面必須顯示在SFSafariViewController中，而非Web檢視。**

某些MVPD要求其登入頁面必須以安全的瀏覽器控制項（例如SFSafariViewController）顯示。 它們主動阻止Web視圖，因此為了能夠與它們進行身份驗證，我們必須使用SVC。 

## 相容性 {#compatiblity}

從iOS SDK 3.1版開始，AccessEnabler SDK會根據伺服器配置，在SFSafariViewController中自動顯示特定MVPD的登入頁面。

SDK 3.1版會自動從應用程式的根檢視控制器顯示SFSafariViewController。 雖然這可簡化實作者的登入頁面管理，但在某些情況下，由於應用程式的特定實作，無法從根檢視控制器呈現SFSafariViewController（就像已顯示的強制回應控制器）。

對於這種情況，3.2版引入了程式設計師手動管理SVC的能力。

## 手動SVC管理 {#manual-svc-management}

要手動管理SVC，實施者必須執行以下步驟：
 

1. 呼叫 **setOptions([&quot;handleSVC&quot;:true])** 在AccessEnabler初始化後（確保在驗證開始之前執行此呼叫）。 這將啟用「手動」SVC管理，SDK不會自動呈現SVC，而是在需要時調用 **navigate(toUrl:*{url}* useSVC:true)**.  

1. 實作選用回呼 **navigateToUrl:useSVC:** 在實施內，您必須使用提供的url，使用SFSafariViewController實例建立svc實例，並在螢幕上顯示：

   ```obj-c
   func navigate(toUrl url: String!, useSVC: Bool) {
       svc =  SFSafariViewController(url: URL(string: url)!)
       svc.delegate = self
       myController.present(svc, animated: true)
       }
   ```

   ***附註：***

   - *您可以按任意方式自定義SFSafariViewController。 例如，在iOS 11以上版本中，您可以將「完成」標籤變更為「取消」。*
   - *為了能夠關閉svc，您需要對其進行引用，請不要在 **navigateToUrl:useSVC***
   - *對「myController」使用您自己的視圖控制器*\
       

1. 在應用程式的委派實作中 **application(\_app):UIApplication，開啟url:URL，選項：\[UIApplicationOpenURLoptionsKey:Any\])-\>布爾**，添加代碼以關閉svc。 您應該已有一些程式碼可呼叫 **accessEnabler.handleExternalURL()**. 在下面添加：

   ```obj-c
   if(svc != nil) {
       svc.dismiss(animated: true)
   }
   ```

   同樣， svc是對您在步驟2建立的SFSafariViewController的引用。\
    

1. 實作 **safariViewControllerDidFinish(\_ controller:SFSafariViewController)** 從 **SFSafariViewControllerDelegate** 以便在用戶使用「完成」按鈕取消svc時捕獲。 在此函式中，若要通知SDK驗證已取消，您需要呼叫：

   ```obj-c
   accessEnabler.setSelectedProvider(nil)
   ```

