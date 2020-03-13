---
description: 我們使用Bento4封裝程式和Adobe離線封裝程式來製作加密的DASH內容。 Bento4將作為輸入的未加密mp4內容。
seo-description: 我們使用Bento4封裝程式和Adobe離線封裝程式來製作加密的DASH內容。 Bento4將作為輸入的未加密mp4內容。
seo-title: 使用Bento4封裝您的內容
title: 使用Bento4封裝您的內容
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 封裝Widevine和PlayReady的內容 {#package-for-widevine}

我們使用Bento4封裝程式和Adobe離線封裝程式來製作加密的DASH內容。 Bento4將作為輸入的未加密mp4內容。

## 使用Bento4封裝您的內容{#package-your-content-with-bento}

Bento4封裝程式預期輸入mp4會預先分割。 Bento4封裝器散發包含此工具。

**呼叫Bento4**

典型的Bento4封裝調用如下所示：

    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtiles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
    —widevine
    
    -widevine-header=provider:intertrust#content_id:2a &quot;CC_300_640x360.mp4&quot;-o&quot;CC_30_30403x036_虛線&quot;
>
    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtiles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;

以下範例結合了PlayReady和Widevine方案。 在此特定情況下，封裝程式將Widevine內容保護和PlayReady內容保護初始化資料新增至輸出的DASH內容。

    /mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtiles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc077c7c5ac215b3b
    —playready
    
    
    
    
    
    —header=\&quot;LA_READY:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;-devine-header=provider:intertrust#content_id:2a &quot;CC_300_640x360.mp4&quot;-o &quot;CC_300_640x360_DASH&quot;其中

標幟的 `--encryption-key` 值為形式 `<base16 encoded key id>:<base16 encoded encryption key>`。

此標 `--widevine-header=provider:intertrust#content_id:2a` 幟會告訴封裝程式將pssh方塊包含在資訊清單中，TVSDK目前需要此方塊才能播放。
PlayReady授權購 `-playready-header` 買的值。

## 使用Adobe Offline Packager封裝您的內容 {#package-your-content-with-adobe-offline-packager}

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