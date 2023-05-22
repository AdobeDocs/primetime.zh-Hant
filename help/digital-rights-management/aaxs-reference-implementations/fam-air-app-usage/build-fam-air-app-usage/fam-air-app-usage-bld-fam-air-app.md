---
title: 構建Flash Access經理AIR應用程式
description: 構建Flash Access經理AIR應用程式
copied-description: true
exl-id: f15fe9d2-d5e8-43ef-a1d5-1211752d54da
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 構建Flash Access經理AIR應用程式 {#building-the-flash-access-manager-air-application}

要從原始碼生成Flash Access管理器AIR檔案，您需要在電腦上安裝Flex和AIRSDK。 在打包並運行應用程式之前，必須使用MXML以下命令將代碼編譯為SWF檔案 [!DNL amxmlc] 編譯器。 的 [!DNL amxmlc] 可在 [!DNL bin] SDK的目錄。 如果需要，可以將路徑環境變數設定為包括FlexSDK bin目錄，以便更輕鬆地在命令行上運行實用程式。

請按下列步驟生成Flash Access管理器AIR檔案：

1. 開啟命令shell或終端，並導航到Flash Access管理器AIR應用程式的項目資料夾( [!DNL UI Tools\Flash Access Manager] )。
1. 輸入以下命令：

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   正在運行 [!DNL amxmlc] 產 [!DNL FlashAccessManager.swf]，其中包含應用程式的已編譯代碼。

Adobe AIRSDK包括AIR開發工具(ADT)實用程式，用於打包AIR應用程式並生成證書。 AIR的申請應該用數字簽名；安裝未正確簽名或完全未簽名的應用程式時，用戶將收到警告。 要使用命令行生成證書，請在與AIR應用程式相同的資料夾中開啟控制台窗口，然後鍵入以下內容：

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

替代 *部分密碼* 你選擇的密碼。 幾秒鐘後，ADT應完成其證書生成過程，您應該有一個新的 [!DNL testCert.pfx] 檔案。

接下來，使用ADT將應用程式打包到 [!DNL .air] 檔案，使用命令：

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

此命令指示ADT使用中的密鑰檔案來打包應用程式 [!DNL testCert.pfx]。 在上行中，您將配置ADT以將整個應用程式打包到一個名為 [!DNL FlashAccessManager.air]，並包括檔案 [!DNL FlashAccessManager-app.xml] 和 [!DNL FlashAccessManager.swf] 以及資產目錄中的影像。

在此過程中，系統將提示您輸入為新證書檔案設定的密碼。 進去，等一下，然後 [!DNL FlashAccessManager.air] 檔案應顯示在與項目檔案相同的目錄中。
