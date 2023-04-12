---
title: Adobe Primetime驗證與Android 6「Marshmallow」新權限模型
description: Adobe Primetime驗證與Android 6「Marshmallow」新權限模型
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---



# Adobe Primetime驗證與Android 6「Marshmallow」新權限模型 {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

新的Android 6 Marshmallow版本會對權限模型導入一些更新，這可能會影響使用現有Adobe Primetime驗證SDK 1.8版及更舊版本之應用程式的行為。 

作為新功能，新的Android作業系統提供 [對應用程式在安裝時和執行階段所需權限的精細控制](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html).

>[!IMPORTANT]
>
>下列說明的變更將 **只會影響專為Android 6.0開發的應用程式** (targetSdkVersion=23)。 升級至Android 6.0時，這些設定不會影響已安裝在使用者裝置上的舊版應用程式。 


尤其是在Android Studio中開發的應用程式中，使用 [API層級23](http://developer.android.com/sdk/api_diff/23/changes.html) 若使用Adobe Primetime Authentication SDK，開發人員將需要編寫自訂程式碼（請參閱下列程式碼片段） [觸發允許/拒絕權限對話方塊](https://developer.android.com/training/permissions/requesting.html). 

以下是用於請求對設備外部儲存器的寫入訪問的代碼摘要：

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




**從用戶的角度**，安裝時，系統會向使用者顯示視窗，提示他們確認檔案的讀/寫權限（請參閱下圖2）。 這將產生以下兩個結果之一：

1. 若使用者 **確認** 權限、一般驗證流程將會保留，且權杖會儲存在全域儲存中。 只要Token有效，使用者就會在應用程式中和使用Adobe Primetime驗證的應用程式中保持驗證狀態。
1. 若使用者 **否認** 儲存空間中的權限、寫入動作會失敗，使用者只有在退出應用程式前才會通過驗證。 請注意，在前景和背景之間切換時，有些應用程式會重新初始化，因此執行此動作時，使用者將會登出。 代號「不會」儲存，使用者每次使用應用程式時都需要驗證。 


>[!TIP]
>
>引入儲存可復原性的功能目前正在開發Adobe Primetime驗證SDK 1.9。新的SDK針對 **在10月的最後一週發行**. 每當無法使用一般儲存時，應用程式會回復到寫入應用程式的沙箱儲存空間。 這涵蓋在API第23層開發的應用程式中，使用者不接受全域儲存的讀/寫權限的情況。 代號會個別儲存於每個應用程式，這表示將停用使用Adobe Primetime驗證之應用程式間的單一登入。


![](assets/android-permissions-request.png)

*圖：針對寫入目標API層級23的應用程式的權限要求對話方塊*

>[!IMPORTANT]
>
> Adobe建議 **其合作夥伴若要使用API 22級(targetSdkVersion=22)或更舊版本來開發應用程式，以確保驗證程式中盡可能提供最佳的使用者體驗**. 
