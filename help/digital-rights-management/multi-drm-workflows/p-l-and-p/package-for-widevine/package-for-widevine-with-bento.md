---
description: 我們使用Bento4打包器和Adobe離線打包器編寫加密的DASH內容。 Bento4作為輸入未加密的mp4內容。
title: 使用Bento4打包您的內容
exl-id: c873eaf6-c738-4f95-a900-a8aecb03754d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 為Widevine和PlayReady打包內容 {#package-for-widevine}

我們使用Bento4打包器和Adobe離線打包器編寫加密的DASH內容。 Bento4作為輸入未加密的mp4內容。

## 使用Bento4打包您的內容{#package-your-content-with-bento}

Bento4打包器期望輸入mp4是預碎的。 Bento4打包器分發包含用於此的工具。

**正在調用Bento4**

典型的Bento4打包程式調用如下所示：

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

下面的示例將PlayReady和Widevine方案組合在一起。 在此特定情況下，打包員將Widevine內容保護和PlayReady內容保護初始化資料添加到輸出DASH內容中。

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

何處

的值 `--encryption-key` 標誌在窗體中 `<base16 encoded key id>:<base16 encoded encryption key>`。

的 `--widevine-header=provider:intertrust#content_id:2a` 標誌指示打包程式將pssh框包含在清單中，TVSDK當前需要該框來播放。

的值 `-playready-header` 用於PlayReady許可證獲取。

## 使用Adobe離線打包程式打包您的內容 {#package-your-content-with-adobe-offline-packager}

Adobe離線打包器將作為輸入未加密的mp4內容。

**正在調用Adobe離線打包程式**

典型的adobe離線打包程式調用如下所示：

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

在此特定情況下，離線打包器將WideVine內容保護和PlayReady內容保護初始化資料添加到輸出DASH內容中。 值 `-key_file_path` 是用於base64編碼的密鑰。 值 `-playready_LA_URL` 用於PlayReady許可證獲取。

conf_path參數指向包含以下內容的配置檔案：

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

因為某些安卓設備 — 主要是Amazon消防電視 — 不支援音頻解密，所以音頻加密是可選的。
