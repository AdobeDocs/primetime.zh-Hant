---
description: 打包內容是準備視頻內容以在Web上回放的過程。 打包包括將原始視頻轉換為清單檔案，以及可選地使用針對不同設備和瀏覽器的不同DRM解決方案來加密內容。
title: 打包您的內容
exl-id: d6f922d6-afec-4314-a01e-b951c1f8a7e8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 打包您的內容 {#package-your-content}

打包內容是準備視頻內容以在Web上回放的過程。 打包包括將原始視頻轉換為清單檔案，以及可選地使用針對不同設備和瀏覽器的不同DRM解決方案來加密內容。

要準備內容，您可以使用Adobe離線打包程式或其他工具，如ExpressPlay的Bento4打包程式。 打包員都準備視頻以進行回放（例如，將原始檔案分片並放入清單），並使用您選擇的DRM解決方案（PlayReady、Widevine、FairPlay、Access等）保護視頻:

* [Adobe離線打包程式](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [ExpressPlay打包機](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. 包或獲取用於測試安裝的內容。

   打包時要記住的一個關鍵點是，在此打包步驟中使用的密鑰ID（內容ID）與您在後續許可證令牌請求中必須提供的密鑰ID（內容ID）相同。 密鑰ID是唯一標識CEK的項(該CEK可能儲存在您自己的密鑰管理資料庫中，或使用 [ExpressPlay的密鑰儲存服務](https://www.expressplay.com/developer/key-storage/)。

   >[!NOTE]
   >
   >對於熟悉Adobe訪問的客戶來說，這是不同解決方案工作方式的重要區別。 在Access中，許可證密鑰被嵌入到DRM元資料中，並與受保護內容來回傳遞。 在此處描述的多DRM系統中，實際許可證不會通過，而是安全地儲存並通過密鑰ID獲得。

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

下面是使用Widevine的Adobe離線打包器的打包示例。 打包器使用配置檔案(例如， [!DNL widevine.xml])，它看起來是這樣的：

```
<config> 
<in_path>sample.mp4</in_path> 
<out_type>dash</out_type> 
<out_path>dash2</out_path> 
<drm/> 
<drm_sys>widevine</drm_sys> 
<frag_dur>4</frag_dur> 
<target_dur>6</target_dur> 
<key_file_path>keyfile.bin</key_file_path> 
<widevine_content_id>2a</widevine_content_id> 
<widevine_provider>intertrust</widevine_provider> 
<widevine_key_id>7debe705d938c76bfd886f077b8fa5f7</widevine_key_id> 
</config>
```

* `in_path`  — 此入口指向本地打包機上源視頻的位置。
* `out_type`  — 此條目描述打包輸出的類型，在本例中為DASH(用於HTML5上的Widevine保護)。
* `out_path`  — 希望輸出到的本地電腦上的位置。
* `drm_sys`  — 要打包的DRM解決方案。 這要麼 `widevine`。 `fairplay`或 `playready`。

* `frag_dur` 和 `target_dur` 是與視頻播放相關的DASH特定持續時間條目。

* `key_file_path`  — 這是作為內容加密密鑰(CEK)的打包電腦上許可證檔案的位置。 它是Base-64編碼的16位元組十六進位字串。
* `widevine_content_id`  — 這是Widevine的&quot;鍋爐板&quot;;總是 `2a`。 (不要將此與 `widevine_key_id`。)

* `widevine_provider`  — 就我們而言，始終將此值設定為 `intertrust`。

* `widevine_key_id`  — 這是您在 `key_file_path` 的子菜單。 換句話說，它標識了用於加密內容的密鑰。 此ID是您自己建立的16位元組的十六進位字串。

如 [打包程式文檔](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)，「作為最佳做法，建立包含要用於生成輸出的常用選項的配置檔案。 然後，通過提供特定選項作為命令行參數來建立輸出。」 在這種情況下，我們的配置檔案相當完整，因此您可以按如下方式建立輸出：

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>命令行參數優先於配置檔案參數。 在本示例中，所需的所有內容都在配置檔案中，但我們已使用 `-out_path test_dash/`。
