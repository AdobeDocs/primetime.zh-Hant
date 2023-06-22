---
title: iOS SDK 3.2+上的SFSafariViewController支援
description: iOS SDK 3.2+上的SFSafariViewController支援
exl-id: 6691550f-c36f-4fae-aa77-082ca7d8a60a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# iOS SDK 3.2+上的SFSafariViewController支援 {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>


**由於安全性需求，某些MVPD的登入頁面必須以SFSafariViewController呈現，而非Web檢視。**

有些MVPD會要求其登入頁面以安全的瀏覽器控制項（如SFSafariViewController）顯示。 它們會主動封鎖Web檢視，因此為了能夠使用它們進行驗證，我們必須使用SVC。 

## 相容性 {#compatiblity}

從iOS SDK 3.1版開始，AccessEnabler SDK會根據伺服器設定，自動顯示SFSafariViewController中特定MVPD的登入頁面。

SDK 3.1版會自動從應用程式的根檢視控制器顯示SFSafariViewController。 雖然這可簡化實作人員的登入頁面管理，但在某些情況下，由於應用程式的特定實作（例如已可見的強制回應視窗），無法從根檢視控制器呈現SFSafariViewController。

在這種情況下，3.2版引進了程式設計師手動管理SVC的功能。

## 手動SVC管理 {#manual-svc-management}

若要手動管理SVC，實作人員必須執行下列步驟：
 

1. 呼叫 **setOptions([&quot;handleSVC&quot;：true])** AccessEnabler初始化之後（請確定在驗證開始前執行此呼叫）。 這將啟用「手動」SVC管理，SDK不會自動呈現SVC，而是在需要時呼叫 **navigate(toUrl：*{url}* useSVC：true)**.  

1. 實作選擇性回呼 **navigateToUrl:useSVC:** 在實施內，您必須使用提供的URL使用SFSafariViewController執行個體建立svc執行個體，並將其顯示在畫面上：

   ```obj-c
   func navigate(toUrl url: String!, useSVC: Bool) {
       svc =  SFSafariViewController(url: URL(string: url)!)
       svc.delegate = self
       myController.present(svc, animated: true)
       }
   ```

   ***附註：***

   - *您可以按您想要的任何方式自訂SFSafariViewController。 例如，在iOS 11+上，您可以將「完成」標籤變更為「取消」。*
   - *為了能夠關閉svc，您需要它的參考，請勿在 **navigateToUrl：useSVC***
   - *對「myController」使用您自己的檢視控制器*\
       

1. 在您的應用程式委派實作中 **application（\_app： UIAapplication，開啟URL： URL，選項： \[UIAapplicationOpenURLOptionsKey： Any\]） -\> Bool**，新增程式碼以關閉svc。 您應該已經有可呼叫的程式碼 **accessEnabler.handleExternalURL()**. 新增以下專案：

   ```obj-c
   if(svc != nil) {
       svc.dismiss(animated: true)
   }
   ```

   同樣地，svc是您在步驟2建立的SFSafariViewController的參照。\
    

1. 實作 **safariViewControllerDidFinish（\_控制器： SFSafariViewController）** 從 **SFSafariViewControllerDelegate** 以便擷取使用者何時使用「完成」按鈕取消了svc。 在此函式中，若要通知SDK驗證已取消，您必須呼叫：

   ```obj-c
   accessEnabler.setSelectedProvider(nil)
   ```
