---
title: 建立Flash Access管理員AIR應用程式
description: 建立Flash Access管理員AIR應用程式
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 建立Flash Access管理員AIR應用程式 {#building-the-flash-access-manager-air-application}

若要從原始程式碼建置Flash Access管理員AIR檔案，您的電腦上必須安裝Flex和AIR SDK。 您必須先使用，將MXML程式碼編譯成SWF檔案，才能封裝並執行應用程式。 [!DNL amxmlc] 編譯器。 此 [!DNL amxmlc] 編譯器可在以下網址找到： [!DNL bin] Flex 4或更新版本SDK的目錄。 如有需要，您可以設定路徑環境變數，使其納入Flex SDK bin目錄，以便更輕鬆地在命令列上執行公用程式。

使用以下程式來建置Flash Access管理員AIR檔案：

1. 開啟命令殼層或終端機，並導覽至Flash Access管理員AIR應用程式的專案資料夾( [!DNL UI Tools\Flash Access Manager] （位於「參考實作」目錄中）。
1. 輸入下列命令：

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   執行中 [!DNL amxmlc] 產生 [!DNL FlashAccessManager.swf]，其中包含應用程式的編譯程式碼。

Adobe AIR SDK包含AIR開發人員工具(ADT)公用程式，以封裝AIR應用程式並產生憑證。 AIR應用程式應經過數位簽署；安裝未正確簽署或完全未簽署的應用程式時，使用者會收到警告。 若要使用命令列產生憑證，請開啟與AIR應用程式位於相同資料夾中的主控台視窗，然後輸入下列內容：

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

替代 *some_password* 並提供您選擇的密碼。 幾秒後，ADT應該會完成其憑證產生程式，而且您應該有新的 [!DNL testCert.pfx] 應用程式目錄中的檔案。

接下來，使用ADT將應用程式封裝到 [!DNL .air] 檔案，使用下列指令：

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

這個命令會告訴ADT使用中的金鑰檔案來封裝您的應用程式 [!DNL testCert.pfx]. 在上面的行中，您可以設定ADT將整個應用程式封裝到名為的檔案中 [!DNL FlashAccessManager.air]，並包含檔案 [!DNL FlashAccessManager-app.xml] 和 [!DNL FlashAccessManager.swf] 和資產目錄的影像。

在此程式中，系統會提示您輸入您為新憑證檔案設定的密碼。 輸入內容、等待片刻，然後 [!DNL FlashAccessManager.air] 檔案應該會出現在與專案檔案相同的目錄中。
