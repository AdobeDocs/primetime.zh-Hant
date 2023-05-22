---
title: Adobe Primetime認證與Android 6「棉花糖」新權限模型
description: Adobe Primetime認證與Android 6「棉花糖」新權限模型
exl-id: 3c96769e-b25b-48ab-bb74-40f13d4e5a84
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Adobe Primetime認證與Android 6「棉花糖」新權限模型 {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

新的Android 6 Marshmallow版本引入了對權限模型的一些更新，這可能會影響使用現有Adobe Primetime身份驗證SDK 1.8及更舊版本的應用的行為。 

作為一項新功能，新的Android作業系統 [精確控制應用程式在安裝時和運行時所需的權限](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html)。

>[!IMPORTANT]
>
>下面介紹的更改將 **僅影響專門為Android 6.0開發的應用程式** (targetSdkVersion=23)。 升級到Android 6.0時，它們不會影響用戶設備上已安裝的較舊應用程式。 


具體來說，對於在Android Studio中使用 [API級別23](http://developer.android.com/sdk/api_diff/23/changes.html) 如果使用Adobe Primetime身份驗證SDK，則開發人員需要編寫自定義代碼（請參閱下面的代碼段） [觸發允許/拒絕權限對話框](https://developer.android.com/training/permissions/requesting.html)。 

以下是用於請求對設備外部儲存的寫入訪問的代碼摘錄：

```java
// Here, thisActivity is the current activity
if (ContextCompat.checkSelfPermission(thisActivity,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
        != PackageManager.WRITE_EXTERNAL_STORAGE) {

    // Should we show an explanation?
    if (ActivityCompat.shouldShowRequestPermissionRationale(thisActivity,
            Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

        // Show an expanation to the user *asynchronously* -- don't block
        // this thread waiting for the user's response! After the user
        // sees the explanation, try again to request the permission.

    } else {

        // No explanation needed, we can request the permission.

        ActivityCompat.requestPermissions(thisActivity,
                new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE);

        // MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE is an
        // app-defined int constant. The callback method gets the
        // result of the request.
    }
}
```




**從用戶的角度**，在安裝時，用戶會收到一個窗口，提示他們確認檔案的讀/寫權限（請參見下圖2）。 這導致以下兩種結果之一：

1. 如果用戶 **確認** 權限、常規驗證流將被保留，令牌將儲存在全局儲存中。 只要令牌有效，用戶將在應用中和使用Adobe Primetime身份驗證的應用之間保持身份驗證。
1. 如果用戶 **否認** 在儲存中的權限、寫入操作將失敗，用戶將僅在退出應用之前進行身份驗證。 請注意，在前台和後台之間切換時，某些應用程式會重新初始化，這樣在執行此操作時用戶將註銷。 令牌未儲存，用戶每次使用應用時都需要進行身份驗證。 


>[!TIP]
>
>目前正在開發一種引入儲存彈性的功能，用於Adobe Primetime驗證SDK 1.9。新SDK的目標 **在10月最後一週發佈**。 當不能使用常規儲存時，應用程式將回退到在應用程式的沙盒儲存中寫入。 這包括在API級別23中開發的應用程式中，用戶不接受全局儲存中的讀/寫權限的情況。 每個應用都單獨儲存令牌，這意味著將禁用使用Adobe Primetime身份驗證的應用之間的單一登錄。


![](assets/android-permissions-request.png)

*圖：針對API級別23編寫的應用的權限請求對話框*

>[!IMPORTANT]
>
> Adobe建議 **其合作夥伴使用API 22級(targetSdkVersion=22)或更舊版本開發應用，以確保在身份驗證過程中獲得盡可能最好的用戶體驗**。
