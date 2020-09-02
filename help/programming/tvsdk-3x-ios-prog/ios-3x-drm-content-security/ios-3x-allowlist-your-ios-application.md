---
description: 您可以使用Adobe的Machotools工具來允許列出您的iOS應用程式。
seo-description: 您可以使用Adobe的Machotools工具來允許列出您的iOS應用程式。
seo-title: 允許列出您的iOS應用程式
title: 允許列出您的iOS應用程式
uuid: bc558f5f-d4e6-4c1c-81eb-f8bd61c63016
translation-type: tm+mt
source-git-commit: eb9f0a2f6d2118b953c711dfdc0402d1d923b016
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# 允許列出您的iOS應用程式 {#allowlist-your-ios-application}

您可以使用Adobe的Machotools工具來允許列出您的iOS應用程式。

通常，當您完成TVSDK應用程式時，可以使用Adobe Primetime DRM命令列工具來允許列出您的應用程式。

>[!TIP]
>
>您也可以使用這些工具來建立DRM原則並加密內容。

允許列出您的應用程式，可確保受保護的內容只能在視訊播放器中播放。 不過，允許列出iOS應用程式時，您必須完成與Apple的應用程式提交政策搭配使用的特殊程式。

在送出iOS應用程式之前，您必須先簽名並發佈至Apple。

>[!NOTE]
>
>Apple會移除您開發人員的簽名，並使用自己的憑證重新簽署應用程式。

由於重新簽署，您在提交至Apple App Store之前產生的允許清單資訊無法使用。

為了使用此提交政策，Adobe已建立工具，將您的iOS應用程式指紋為指紋，以建立摘要值、簽署此值，並將此值插入您的iOS應用程式。 `machotools` 在您為iOS應用程式指紋後，就可以將應用程式送出至Apple App Store。 當使用者從App Store執行您的應用程式時，Primetime DRM會執行應用程式指紋的執行時期計算，並以先前在應用程式中插入的摘要值加以確認。 如果指紋符合，則確認應用程式已列出允許，並允許受保護的內容播放。

Adobe工 `machotools` 具隨附於iOS TVSDK SDK的[!DNL [...]/tools/DRM]資料夾。

若要使用 `machotools`:

1. 生成密鑰對。

   要使用OpenSSL等實用程式，請開啟命令窗口並輸入以下內容：

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. 出現提示時，輸入密碼以保護私密金鑰。

   密碼至少應包含12個字元，且字元應包含大寫和小寫ASCII字元與數字的混合。
1. 要使用OpenSSL為您生成強口令，請開啟命令窗口並輸入以下內容：

   ```shell
   openssl rand -base64 8
   ```

1. 產生憑證簽署要求(CSR)。

   要使用OpenSSL生成CSR，請開啟「命令窗口」並輸入以下內容：

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. 自行簽署憑證並輸入任何期間。

   下列範例提供20年的有效期：

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. 將自簽名證書轉換為PKCS#12檔案：

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   您可以使用自簽名憑證來簽署您的iOS應用程式。

1. 更新PFX檔案和密碼的位置。
1. 在Xcode中建立應用程式之前，請前往 **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** 並將下列命令新增至您的執行指令碼：

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. 執行 [!DNL machotools] 以產生應用程式Publisher ID雜湊值。

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. 建立新的DRM原則或更新您現有的原則，以包含傳回的發佈者ID雜湊值。
1. 使用 [!DNL AdobePolicyManager.jar]建立新的DRM原則（更新您現有的原則），將傳回的發佈者ID雜湊值、選用的應用程式ID，以及最小和最大版本屬性包含在包含的檔 [!DNL flashaccess-tools.properties] 案中。

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. 使用新的DRM原則封裝內容，並確認在iOS應用程式中播放允許列出的內容。
