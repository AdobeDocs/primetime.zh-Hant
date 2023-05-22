---
description: Adobe離線打包器將作為輸入未加密的mp4內容。
title: 使用Adobe離線打包程式打包您的內容
exl-id: 4433d76a-57c0-41e6-b358-5408b0fe87e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 使用Adobe離線打包程式打包您的內容{#package-your-content-with-adobe-offline-packager}

Adobe離線打包器將作為輸入未加密的mp4內容。

**正在調用Adobe離線打包程式**

典型的adobe離線打包程式調用如下所示：

    java -jarOfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
    -widevine提供程式信任
    -playready_LA_URL
    http://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
    -content_id c595f214d84dc7ecf31a8ebf1b7ddda5

在此特定情況下，離線打包器將WideVine內容保護和PlayReady內容保護初始化資料添加到輸出DASH內容中。 值 `-key_file_path` 是用於base64編碼的密鑰。 值 `-playready_LA_URL` 用於PlayReady許可證獲取。

conf_path參數指向包含以下內容的配置檔案：

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>假&lt;/encrypt_audio>
    &lt;/config>

因為某些安卓設備 — 主要是Amazon消防電視 — 不支援音頻解密，所以音頻加密是可選的。
