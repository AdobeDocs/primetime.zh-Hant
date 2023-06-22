---
description: 我們使用Bento4封裝程式和Adobe離線封裝程式來編寫加密的DASH內容。 Bento4會以未加密的mp4內容作為輸入。
title: 使用Bento4封裝您的內容
exl-id: c873eaf6-c738-4f95-a900-a8aecb03754d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 封裝Widevine和PlayReady的內容 {#package-for-widevine}

我們使用Bento4封裝程式和Adobe離線封裝程式來編寫加密的DASH內容。 Bento4會以未加密的mp4內容作為輸入。

## 使用Bento4封裝您的內容{#package-your-content-with-bento}

Bento4封裝程式預期輸入mp4會預先分割。 Bento4 Packager散發包含此功能的工具。

**正在撥打Bento4**

典型的Bento4封裝程式呼叫如下所示：

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

以下範例結合了PlayReady和Widevine配置。 在此特定情況下，封裝程式會將Widevine內容保護和PlayReady內容保護初始化資料新增至輸出的DASH內容。

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

位置

的值 `--encryption-key` 旗標在表單中 `<base16 encoded key id>:<base16 encoded encryption key>`.

此 `--widevine-header=provider:intertrust#content_id:2a` flag會告訴封裝程式將pssh方塊納入資訊清單中，哪個TVSDK目前需要播放此方塊。

的值 `-playready-header` 用於PlayReady授權贏取。

## 使用Adobe離線封裝程式封裝您的內容 {#package-your-content-with-adobe-offline-packager}

AdobeOffline Packager會以未加密的mp4內容作為輸入。

**呼叫Adobe離線封裝程式**

典型的Adobe離線封裝程式呼叫看起來類似以下呼叫：

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

在此特定情況下，離線封裝程式會將Widevine內容保護和PlayReady內容保護初始化資料新增至輸出DASH內容。 的值 `-key_file_path` 適用於base64編碼金鑰。 的值 `-playready_LA_URL` 用於PlayReady授權贏取。

conf_path引數指向包含下列內容的組態檔：

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

由於某些Android裝置(主要是Amazon Fire TV)不支援音訊解密，因此可選擇使用音訊加密。
