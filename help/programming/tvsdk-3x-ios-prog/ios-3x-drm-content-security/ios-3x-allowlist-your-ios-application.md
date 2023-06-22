---
description: 您可以使用Adobe的Machotools工具，允許列出iOS應用程式。
title: 允許列出您的iOS應用程式
exl-id: 3af75d9a-3b38-4d3c-9890-513a4abc1809
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 允許列出您的iOS應用程式 {#allowlist-your-ios-application}

您可以使用Adobe的Machotools工具，允許列出iOS應用程式。

通常，當您完成TVSDK應用程式時，可以使用Adobe Primetime DRM命令列工具來允許列出您的應用程式。

>[!TIP]
>
>您也可以使用這些工具來建立DRM原則並加密內容。

將您的應用程式列入允許清單，可確保受保護的內容只能在您的視訊播放器中播放。 不過，允許列出iOS應用程式，需要您完成與Apple應用程式提交原則搭配使用的特殊程式。

在提交iOS應用程式之前，您需要先簽署該應用程式並將其發佈到Apple。

>[!NOTE]
>
>Apple會刪除開發人員的簽名，並使用他們自己的憑證重新簽署應用程式。

由於重新簽署，您在提交至Apple App Store之前產生的允許清單資訊無法使用。

若要使用此提交原則，Adobe已建立 `machotools` 此工具會為iOS應用程式建立指紋，以建立摘要值、簽署此值，並將此值插入您的iOS應用程式中。 為iOS應用程式建立指紋後，您可以將應用程式提交至Apple App Store。 當使用者從App Store執行您的應用程式時，Primetime DRM會執行應用程式指紋的執行階段計算，並使用先前插入應用程式的摘要值來確認它。 如果指紋相符，則確認應用程式允許列出，並允許播放受保護的內容。

Adobe `machotools` 工具包含在[！DNL]的iOS TVSDK SDK中 [...]/tools/DRM]資料夾。

使用 `machotools`：

1. 產生金鑰組。

   若要使用OpenSSL等公用程式，請開啟命令視窗並輸入下列內容：

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. 出現提示時，請輸入密碼以保護私密金鑰。

   密碼應包含至少12個字元，且字元應混合使用大寫和小寫ASCII字元和數字。
1. 若要使用OpenSSL為您產生強式密碼，請開啟命令視窗並輸入下列內容：

   ```shell
   openssl rand -base64 8
   ```

1. 產生憑證申請檔(CSR)。

   若要使用OpenSSL來產生CSR，請開啟「命令視窗」並輸入下列內容：

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. 自行簽署憑證並輸入任何持續時間。

   以下範例提供20年的有效期：

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. 將自我簽署憑證轉換為PKCS#12檔案：

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   您可以使用自我簽署憑證來簽署您的iOS應用程式。

1. 更新PFX檔案和密碼的位置。
1. 在Xcode中建立應用程式之前，請前往  **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** 並將以下命令新增至您的執行指令碼：

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. 執行 [!DNL machotools] 以產生您的應用程式發佈者ID雜湊值。

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. 建立新的DRM原則或更新現有原則以包含傳回的發行者ID雜湊值。
1. 使用 [!DNL AdobePolicyManager.jar]，建立新的DRM原則（更新您現有的原則）以包含傳回的發行者ID雜湊值、選用的「應用程式ID」，以及包含的最小和最大版本屬性 [!DNL flashaccess-tools.properties] 檔案。

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. 使用新的DRM原則封裝內容，並確認在iOS應用程式中播放允許清單中的內容。
