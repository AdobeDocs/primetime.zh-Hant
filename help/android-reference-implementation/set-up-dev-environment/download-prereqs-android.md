---
seo-title: 下載並設定先決條件軟體
title: 下載並設定先決條件軟體
description: 安裝程式非常簡單。 如果您的系統上已安裝JDK，則可以跳過此步驟，但請注意，您的JDK、Eclipse IDE和OS需要相容。
seo-description: 安裝程式非常簡單。 如果您的系統上已安裝JDK，則可以跳過此步驟，但請注意，您的JDK、Eclipse IDE和OS需要相容。
uuid: ca29144f-8088-4c8d-93cf-aa59007da034
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---


# 下載並配置先決條件軟體{#download-and-configure-prerequisite-software}

1. 從[https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/)下載JDK。

   安裝程式非常簡單。 如果您的系統上已安裝JDK，則可以跳過此步驟，但請注意，您的JDK、Eclipse IDE和OS需要相容。
1. 從[https://www.eclipse.org/downloads](https://www.eclipse.org/downloads)下載適用於Java開發人員的Eclipse IDE。

   解壓縮套件後，您就可以直接執行Eclipse。 沒有安裝程式。
1. 從[https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)下載Android SDK ADT Bundle。

   此套件包含Eclipse。 如果您的系統已安裝Eclipse，您可從[!UICONTROL Use An Existing IDE]區段下載適用於您平台的SDK工具。

   拆開包裝並安裝到您記得的位置。 您需要在稍後的步驟中參考此項。
1. 設定Android SDK。
   1. 開啟終端機（在Mac OS X中）或命令提示（在Windows中）。
   1. 導覽至您下載／解壓縮Android SDK的目錄。
   1. 轉到工具資料夾，該資料夾包含名為[!DNL android]的檔案。
   1. 運行以下命令：

      * 對於Mac OS X/Unix:

         ```
         chmod +x android 
         android update sdk --no-ui
         ```

      * 針對Windows:

         ```
         android update sdk --no-ui
         ```

         這個過程需要一段時間。

1. 設定Eclipse。
   1. 啟動Eclipse。

      在Windows上，如果Eclipse未啟動，且報告的問題是Eclipse找不到必要的Java檔案，請嘗試下列動作：

      * 將`-vm C:\[path to your JDK bin]\javaw.exe`新增至[!DNL eclipse.ini]檔案。
   1. 選擇&#x200B;**[!UICONTROL Help]** > **[!UICONTROL Install New Software]**。
   1. 按一下 **[!UICONTROL Add...]**.
   1. 輸入`Android`作為名稱。
   1. 為&#x200B;**[!UICONTROL Work with]**&#x200B;連結輸入`https://dl-ssl.google.com/android/eclipse/`。
   1. 按一下 **[!UICONTROL OK]**.

      您應該會看到類似下列的對話方塊：

      ![](assets/available_software.jpg)

   1. 選取產生的套件（「開發人員工具」和「NDK增效模組」中的套件），然後按一下&#x200B;**[!UICONTROL Next]**。

      這會下載Android開發工具(ADT)。
   1. 下載完成後，請重新啟動Eclipse。

   Android SDK現已安裝。 1.設定Eclipse，以便找到Android SDK並將其當做資源使用。
   1. 開啟Eclipse。
   1. 在Windows上選擇&#x200B;**[!UICONTROL Window]** > **[!UICONTROL Preferences]**; **[!UICONTROL ADT]** > **[!UICONTROL Preferences]**（在Mac OS X上）。
   1. 選擇&#x200B;**[!UICONTROL Android]**&#x200B;頁籤。
   1. 瀏覽至Android SDK的位置。
   1. 按一下 **[!UICONTROL Apply]**.

      ![步驟結果](assets/ss2.jpg)


