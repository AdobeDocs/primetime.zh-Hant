---
description: AdobeOffline Packager會將輸入未加密的mp4內容。
title: 使用AdobeOffline Packager封裝您的內容
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 使用AdobeOffline Packager{#package-your-content-with-adobe-offline-packager}封裝您的內容

AdobeOffline Packager會將輸入未加密的mp4內容。

**呼叫AdobeOffline Packager**

典型的adobe離線封裝呼叫如下所示：

    java -jarOfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84decf31a8ebf1b7dda5
    -widevine_provider intertrest
    -playready_LA_
    
    
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx95f214dc7ecf31a8ebf8dbf1dddbf5-id5c595f214d84dc7ecf31a8ebf1b7dda5

在此特定情況下，離線封裝程式會將Widevine內容保護和PlayReady內容保護初始化資料新增至輸出的DASH內容。 `-key_file_path`的值用於基本64編碼的密鑰。 `-playready_LA_URL`的值用於PlayReady授權購買。

conf_path參數指向將包含以下內容的配置檔案：

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>假&lt;/encrypt_audio>
    &lt;/config>

因為某些Android裝置— 主要是Amazon火電— 不支援音訊解密，音訊加密是選用的。
