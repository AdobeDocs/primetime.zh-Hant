---
title: 下載和配置必備軟體
description: 安裝過程簡單明瞭。 如果系統上已安裝了JDK，則可以跳過此步驟，但要注意JDK、Eclipse IDE和OS需要相容。
exl-id: c2884a55-4f5e-4da8-807d-633625d7fef9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 下載和配置必備軟體 {#download-and-configure-prerequisite-software}

1. 從下載JDK [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/)。

   安裝過程簡單明瞭。 如果系統上已安裝了JDK，則可以跳過此步驟，但要注意JDK、Eclipse IDE和OS需要相容。
1. 從下載Eclipse IDE for Java開發人員 [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads)。

   解壓縮包後，可以直接運行Eclipse。 沒有安裝程式。
1. 從下載Android SDK ADT包 [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)。

   此捆綁包包括Eclipse。 如果系統上已安裝Eclipse，則可以從 [!UICONTROL Use An Existing IDE] 的子菜單。

   解壓縮並安裝到您將記住的位置。 您需要在稍後的步驟中參考此內容。
1. 配置Android SDK。
   1. 開啟終端(在MacOS X中)或命令提示符（在Windows中）。
   1. 導航到下載/解壓縮Android SDK的目錄。
   1. 轉到工具資料夾，該資料夾包含名為 [!DNL android]。
   1. 運行以下命令：

      * 對於MacOS X/Unix:

         ```
         chmod +x android 
         android update sdk --no-ui
         ```

      * 對於Windows:

         ```
         android update sdk --no-ui
         ```

         這個過程需要一段時間。

1. 配置Eclipse。
   1. 啟動Eclipse。

      在Windows上，如果Eclipse未啟動，並且報告的問題是Eclipse找不到所需的Java檔案，請嘗試以下操作：

      * 添加 `-vm C:\[path to your JDK bin]\javaw.exe` 到 [!DNL eclipse.ini] 的子菜單。
   1. 選擇  **[!UICONTROL Help]** > **[!UICONTROL Install New Software]** 。
   1. 按一下 **[!UICONTROL Add...]**。
   1. 輸入 `Android` 的下界。
   1. 輸入 `https://dl-ssl.google.com/android/eclipse/` 為 **[!UICONTROL Work with]** 的子菜單。
   1. 按一下 **[!UICONTROL OK]**。

      您應看到類似以下對話框：

      ![](assets/available_software.jpg)

   1. 選擇生成的包（開發人員工具和NDK插件中的包），然後按一下 **[!UICONTROL Next]**。

      這將下載Android開發工具(ADT)。
   1. 下載完成後，重新啟動Eclipse。

   Android SDK現已安裝。 1。配置Eclipse，以便找到Android SDK並將其用作資源。
   1. 開啟Eclipse。
   1. 選擇  **[!UICONTROL Window]** > **[!UICONTROL Preferences]** 在Windows上；  **[!UICONTROL ADT]** > **[!UICONTROL Preferences]** 在MacOS X上。
   1. 選擇 **[!UICONTROL Android]** 頁籤。
   1. 瀏覽到Android SDK的位置。
   1. 按一下 **[!UICONTROL Apply]**。

      ![步驟結果](assets/ss2.jpg)
