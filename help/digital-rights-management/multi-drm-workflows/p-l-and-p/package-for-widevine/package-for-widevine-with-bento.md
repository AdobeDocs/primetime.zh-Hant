---
description: 我們使用Bento4封裝程式和Adobe離線封裝程式來製作加密的DASH內容。 Bento4將作為輸入的未加密mp4內容。
seo-description: 我們使用Bento4封裝程式和Adobe離線封裝程式來製作加密的DASH內容。 Bento4將作為輸入的未加密mp4內容。
seo-title: 使用Bento4封裝您的內容
title: 使用Bento4封裝您的內容
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: 75702ea2a524d7b38bb9ac83cb094c8482b1098f
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 封裝Widevine和PlayReady的內容 {#package-for-widevine}

我們使用Bento4封裝程式和Adobe離線封裝程式來製作加密的DASH內容。 Bento4將作為輸入的未加密mp4內容。

## 使用Bento4封裝您的內容{#package-your-content-with-bento}

Bento4封裝程式預期輸入mp4會預先分割。 Bento4封裝器散發包含此工具。

**呼叫Bento4**

典型的Bento4封裝調用如下所示：

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
```

以下範例結合了PlayReady和Widevine方案。 在此特定情況下，封裝程式將Widevine內容保護和PlayReady內容保護初始化資料新增至輸出的DASH內容。

```
/mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

where

標幟的 `--encryption-key` 值為形式 `<base16 encoded key id>:<base16 encoded encryption key>`。

此標 `--widevine-header=provider:intertrust#content_id:2a` 幟會告訴封裝程式將pssh方塊包含在資訊清單中，TVSDK目前需要此方塊才能播放。

PlayReady授權購 `-playready-header` 買的值。

## 使用Adobe Offline Packager封裝您的內容 {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager會將輸入未加密的mp4內容。

**呼叫Adobe Offline Packager**

典型的adobe離線封裝呼叫如下所示：

```
java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path "Jaigo.mp4"
-out_path "Jaigo_DASH"
-key_file_path "Jaigo_DASH/_info/key.B64.random"
-widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
-widevine_provider intertrust
-playready_LA_URL
http://pr.test.expressplay.com/playready/RightsManager.asmx
-playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
-content_id c595f214d84dc7ecf31a8ebf1b7ddda5
```

在此特定情況下，離線封裝程式會將Widevine內容保護和PlayReady內容保護初始化資料新增至輸出的DASH內容。 值是用 `-key_file_path` 於基64編碼密鑰。 其值用於 `-playready_LA_URL` PlayReady授權購買。

conf_path參數指向將包含以下內容的配置檔案：

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

因為某些Android裝置— 主要是Amazon Fire TV — 不支援音訊解密，音訊加密是選用的。
