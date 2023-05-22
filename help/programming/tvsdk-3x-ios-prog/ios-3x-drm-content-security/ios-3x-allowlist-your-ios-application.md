---
description: 您可以使用Adobe的machotools工具來允許列出您的iOS應用。
title: 允許列出您的iOS應用程式
exl-id: 3af75d9a-3b38-4d3c-9890-513a4abc1809
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 允許列出您的iOS應用程式 {#allowlist-your-ios-application}

您可以使用Adobe的machotools工具來允許列出您的iOS應用。

通常，在完成TVSDK應用程式時，可以使用Adobe PrimetimeDRM命令行工具來允許列出您的應用。

>[!TIP]
>
>您還可以使用這些工具建立DRM策略並加密內容。

允許列出應用可確保只能在視頻播放器中播放受保護的內容。 但是，允許列出iOS應用程式要求您完成與Apple的應用程式提交策略配合使用的特殊程式。

在提交iOS應用之前，您需要簽名並將其發佈到Apple。

>[!NOTE]
>
>Apple刪除開發人員的簽名，並用自己的證書重新簽名應用程式。

由於重新簽名，您在提交到AppleApp Store之前生成的允許清單資訊不可用。

要使用此提交策略，Adobe已建立 `machotools` 用於指紋iOS應用程式以建立摘要值、簽名此值並將此值注入iOS應用程式的工具。 在您為iOS應用指紋後，您可以將該應用提交到AppleApp Store。 當用戶從App Store運行您的應用時，Mighile DRM對應用程式指紋執行運行時計算，並使用先前在應用程式中注入的摘要值來確認它。 如果指紋匹配，則確認該應用被列為允許，並允許播放受保護的內容。

Adobe `machotools` 工具包含在[!DNL]中的iOSTVSDK SDK中 [...]/tools/DRM]資料夾。

要使用 `machotools`:

1. 生成密鑰對。

   要使用OpenSSL等實用程式，請開啟命令窗口並輸入以下內容：

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. 出現提示時，輸入密碼以保護私鑰。

   密碼應至少包含12個字元，並且字元應包含大寫和小寫ASCII字元和數字的混合。
1. 要使用OpenSSL為您生成強密碼，請開啟命令窗口並輸入以下命令：

   ```shell
   openssl rand -base64 8
   ```

1. 生成證書籤名請求(CSR)。

   要使用OpenSSL生成CSR，請開啟「命令窗口」，然後輸入以下內容：

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. 自簽名證書並輸入任何持續時間。

   以下示例給出一個20年的到期日：

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. 將自簽名證書轉換為PKCS#12檔案：

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   您可以使用自簽名證書來簽署您的iOS應用。

1. 更新PFX檔案和密碼的位置。
1. 在Xcode中生成應用程式之前，請轉至  **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** 並將以下命令添加到運行指令碼：

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. 執行 [!DNL machotools] 生成應用發佈者ID哈希值。

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. 建立新的DRM策略或更新現有策略以包括返回的發佈者ID哈希值。
1. 使用 [!DNL AdobePolicyManager.jar]，建立新的DRM策略（更新現有策略），以在包含的中包括返回的發佈者ID哈希值、可選的應用ID以及最小和最大版本屬性 [!DNL flashaccess-tools.properties] 的子菜單。

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. 使用新DRM策略打包內容，並確認在您的iOS應用中播放允許列出的內容。
