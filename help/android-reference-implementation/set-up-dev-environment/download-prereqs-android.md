---
title: 下載及設定必要軟體
description: 安裝程式簡單明瞭。 如果您的系統上已安裝JDK，您可以略過此步驟，但請注意，您的JDK、Eclipse IDE和作業系統必須相容。
exl-id: c2884a55-4f5e-4da8-807d-633625d7fef9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 下載及設定必要軟體 {#download-and-configure-prerequisite-software}

1. 下載JDK，從 [https://www.oracle.com/technetwork/java/javase/downloads/](https://www.oracle.com/technetwork/java/javase/downloads/).

   安裝程式簡單明瞭。 如果您的系統上已安裝JDK，您可以略過此步驟，但請注意，您的JDK、Eclipse IDE和作業系統必須相容。
1. 從下載適用於Java開發人員的Eclipse IDE [https://www.eclipse.org/downloads](https://www.eclipse.org/downloads).

   解壓縮套件後，您可以直接執行Eclipse。 沒有安裝程式。
1. 下載Android SDK ADT套件組合，從 [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html).

   此套件組合包含Eclipse。 如果您的系統上已安裝Eclipse，您可以從以下網站下載適用於您平台的SDK工具： [!UICONTROL Use An Existing IDE] 區段。

   拆開包裝並安裝到您記得的位置。 您需要在稍後的步驟中參考此內容。
1. 設定Android SDK。
   1. 開啟終端機(在Mac OS X中)或命令提示（在Windows中）。
   1. 導覽至您下載/解壓縮Android SDK的目錄。
   1. 前往tools資料夾，其中包含名為的檔案 [!DNL android].
   1. 執行以下命令：

      * 若為Mac OS X/Unix：

         ```
         chmod +x android 
         android update sdk --no-ui
         ```

      * 對於Windows：

         ```
         android update sdk --no-ui
         ```

         此程式需要一些時間。

1. 設定Eclipse。
   1. 啟動Eclipse。

      在Windows上，如果Eclipse未啟動，且報告的問題為Eclipse找不到必要的Java檔案，請嘗試下列操作：

      * 新增 `-vm C:\[path to your JDK bin]\javaw.exe` 至您的 [!DNL eclipse.ini] 檔案。
   1. 選取  **[!UICONTROL Help]** > **[!UICONTROL Install New Software]** .
   1. 按一下 **[!UICONTROL Add...]**.
   1. 輸入 `Android` 名稱。
   1. 輸入 `https://dl-ssl.google.com/android/eclipse/` 的 **[!UICONTROL Work with]** 連結。
   1. 按一下 **[!UICONTROL OK]**.

      您應該會看到類似以下的對話方塊：

      ![](assets/available_software.jpg)

   1. 選取產生的套件（開發人員工具和NDK外掛程式中的套件）並按一下 **[!UICONTROL Next]**.

      以下載Android開發工具(ADT)。
   1. 下載完成後，請重新啟動Eclipse。

   Android SDK現已安裝。 1.設定Eclipse，使其可找到Android SDK並將其用作資源。
   1. 開啟Eclipse。
   1. 選取  **[!UICONTROL Window]** > **[!UICONTROL Preferences]** 在Windows上；  **[!UICONTROL ADT]** > **[!UICONTROL Preferences]** 在Mac OS X上。
   1. 選取 **[!UICONTROL Android]** 標籤。
   1. 瀏覽至Android SDK的位置。
   1. 按一下 **[!UICONTROL Apply]**.

      ![步驟結果](assets/ss2.jpg)
