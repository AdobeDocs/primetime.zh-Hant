---
title: iOSSDK 3.2+上的SFSafariViewController支援
description: iOSSDK 3.2+上的SFSafariViewController支援
exl-id: 6691550f-c36f-4fae-aa77-082ca7d8a60a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# iOSSDK 3.2+上的SFSafariViewController支援 {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>


**由於安全要求，某些MVPD的登錄頁必須顯示在SFSafariViewController中，而不是Web視圖中。**

某些MVPD要求其登錄頁在安全瀏覽器控制項（如SFSafariViewController）中顯示。 它們正在主動阻止Web視圖，因此為了能夠通過它們進行身份驗證，我們必須使用SVC。 

## 相容性 {#compatiblity}

從iOSSDK 3.1版開始，AccessEnabler SDK根據伺服器配置自動顯示SFSafariViewController中特定MVPD的登錄頁。

SDK 3.1版自動從應用程式的根視圖控制器中顯示SFSafariViewController。 雖然這簡化了實施者的登錄頁管理，但是，由於應用的特定實現（如已可見的模式控制器），有些情況下無法從根視圖控制器呈現SFSafariViewController。

對於此類情況，3.2版引入了程式設計師手動管理SVC的能力。

## 手動SVC管理 {#manual-svc-management}

為了手動管理SVC，實施者必須執行以下步驟：
 

1. 呼叫 **setOptions([&quot;handleSVC&quot;:true])** 在AccessEnabler初始化後（確保在驗證開始之前執行此調用）。 這將啟用「手動」 SVC管理， SDK不會自動顯示SVC，而是在需要時調用 **導航（到Url）:*{url}* useSVC:true)**。  

1. 實現可選回調 **導航至URL:useSVC:** 在實現中，必須使用提供的url使用SFSafariViewController實例建立svc實例，並將其顯示在螢幕上：

   ```obj-c
   func navigate(toUrl url: String!, useSVC: Bool) {
       svc =  SFSafariViewController(url: URL(string: url)!)
       svc.delegate = self
       myController.present(svc, animated: true)
       }
   ```

   ***附註：***

   - *可以以任何方式自定義SFSafariViewController。 例如，在iOS11+上，可以將「完成」標籤更改為「取消」。*
   - *為了能夠取消svc，您需要對它進行引用，請不要在 **導航至Url:useSVC***
   - *將您自己的視圖控制器用於「myController」*\
       

1. 在應用程式的委託實施中 **應用程式(\_app):UIApplication，開啟URL:URL，選項：\[UIApplicationOpenURLOptionsKey:任何\])-\>布爾**，添加代碼以關閉svc。 你應該已經有一些代碼 **accessEnabler.handleExternalURL()**。 下面添加：

   ```obj-c
   if(svc != nil) {
       svc.dismiss(animated: true)
   }
   ```

   同樣，svc是對您在步驟2中建立的SFSafariViewController的引用。\
    

1. 實施 **SafariViewControllerDidFinish(\_控制器：SFSafariViewController)** 從 **SFSafariViewControllerDelegate** 以便在用戶使用「完成」按鈕取消svc時捕獲。 在此函式中，為了通知SDK已取消身份驗證，您需要調用：

   ```obj-c
   accessEnabler.setSelectedProvider(nil)
   ```
