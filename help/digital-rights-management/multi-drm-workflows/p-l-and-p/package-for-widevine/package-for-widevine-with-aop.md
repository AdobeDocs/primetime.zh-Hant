---
description: AdobeOffline Packager會取得未加密的mp4內容作為輸入。
title: 使用Adobe離線封裝程式封裝您的內容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 使用Adobe離線封裝程式封裝您的內容{#package-your-content-with-adobe-offline-packager}

AdobeOffline Packager會取得未加密的mp4內容作為輸入。

**呼叫Adobe離線封裝程式**

典型的Adobe離線封裝程式呼叫看起來類似下列呼叫：

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
    -widevine_provider intertrust
    -playready_LA_URL
    http://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
    -content_id c595f214d84dc7ecf31a8ebf1b7ddda5

在此特定情況下，離線封裝程式會將Widevine內容保護和PlayReady內容保護初始化資料新增至輸出DASH內容。 的值 `-key_file_path` 適用於base64編碼金鑰。 的值 `-playready_LA_URL` 用於PlayReady授權贏取。

conf_path引數指向包含下列內容的組態檔：

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

由於某些Android裝置(主要是Amazon Fire TV)不支援音訊解密，因此可選擇使用音訊加密。
