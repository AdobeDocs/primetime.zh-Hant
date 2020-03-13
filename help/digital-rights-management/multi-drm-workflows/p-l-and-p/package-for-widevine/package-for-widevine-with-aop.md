---
description: Adobe Offline Packager會將輸入未加密的mp4內容。
seo-description: Adobe Offline Packager會將輸入未加密的mp4內容。
seo-title: 使用Adobe Offline Packager封裝您的內容
title: 使用Adobe Offline Packager封裝您的內容
uuid: d0676147-c20f-49ea-93a6-9c8dbbbba992
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 使用Adobe Offline Packager封裝您的內容{#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager會將輸入未加密的mp4內容。

**呼叫Adobe Offline Packager**

典型的adobe離線封裝呼叫如下所示：

    java -jarOfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84decf31a8ebf1b7dda5
    -widevine_provider intertrest
    -playready_LA_
    
    
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx95f214dc7ecf31a8ebf8dbf1dddbf5-id5-playready_c595f214d84dc7ecf31a8ebf1b7dda5

在此特定情況下，離線封裝程式會將Widevine內容保護和PlayReady內容保護初始化資料新增至輸出的DASH內容。 值是用 `-key_file_path` 於基64編碼密鑰。 其值用於 `-playready_LA_URL` PlayReady授權購買。

conf_path參數指向將包含以下內容的配置檔案：

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config

因為某些Android裝置— 主要是Amazon Fire TV — 不支援音訊解密，音訊加密是選用的。
