---
title: 建立Flash Access管理器AIR應用程式
description: 建立Flash Access管理器AIR應用程式
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 構建Flash Access管理器AIR應用程式{#building-the-flash-access-manager-air-application}

若要從原始碼建立Flash Access管理器AIR檔案，您需要在電腦上安裝Flex和AIR SDK。 您必須先使用[!DNL amxmlc]編譯器將程式碼編譯MXML為SWF檔案，才能封裝並執行應用程式。 [!DNL amxmlc]編譯器可在Flex4或更新版SDK的[!DNL bin]目錄中找到。 如果需要，您可以將路徑環境變數設定為包含FlexSDK bin目錄，以便更輕鬆地在命令行上運行實用程式。

請依照下列程式建立Flash Access管理器AIR檔案：

1. 開啟命令shell或終端機，並導覽至Flash Access管理器AIR應用程式的專案資料夾（位於參考實作目錄中的[!DNL UI Tools\Flash Access Manager]）。
1. 輸入以下命令：

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   運行[!DNL amxmlc]會生成[!DNL FlashAccessManager.swf] ，該包含應用程式的編譯代碼。

Adobe AIRSDK包含AIR開發人員工具(ADT)公用程式，以封裝AIR應用程式並產生憑證。 AIR應用程式應以數位方式簽署；安裝未正確簽署或完全未簽署的應用程式時，使用者會收到警告。 若要使用命令列產生憑證，請在與AIR應用程式相同的檔案夾中開啟主控台視窗，然後輸入下列：

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

使用您選擇的密碼替換&#x200B;*some_password*。 幾秒後，ADT應完成其憑證產生程式，而您的應用程式目錄中應有新的[!DNL testCert.pfx]檔案。

接著，使用ADT命令將應用程式封裝在[!DNL .air]檔案中：

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

此命令指示ADT使用[!DNL testCert.pfx]中的鍵檔案來封裝您的應用程式。 在上行中，您可以配置ADT將整個應用程式封裝到名為[!DNL FlashAccessManager.air]的檔案中，並包括[!DNL FlashAccessManager-app.xml]和[!DNL FlashAccessManager.swf]檔案以及資產目錄中的映像。

在此程式中，系統會提示您輸入為新證書檔案設定的密碼。 請輸入它，稍候，[!DNL FlashAccessManager.air]檔案應該會出現在專案檔案所在的相同目錄中。
