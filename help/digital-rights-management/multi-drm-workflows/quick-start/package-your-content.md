---
description: 封裝內容是準備視訊內容以便在網路上播放的程式。 封裝包括將原始視訊轉換為資訊清單檔案，並可選擇使用不同裝置和瀏覽器的不同DRM解決方案來加密內容。
seo-description: 封裝內容是準備視訊內容以便在網路上播放的程式。 封裝包括將原始視訊轉換為資訊清單檔案，並可選擇使用不同裝置和瀏覽器的不同DRM解決方案來加密內容。
seo-title: 封裝您的內容
title: 封裝您的內容
uuid: b9bc6104-a1ea-4ea0-a0a4-af8a606e5d47
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 封裝您的內容 {#package-your-content}

封裝內容是準備視訊內容以便在網路上播放的程式。 封裝包括將原始視訊轉換為資訊清單檔案，並可選擇使用不同裝置和瀏覽器的不同DRM解決方案來加密內容。

若要準備內容，您可以使用Adobe Offline Packager或其他工具，例如ExpressPlay的Bento4封裝程式。 封裝程式都會準備視訊以供播放（例如，將原始檔案分割並放入資訊清單中），並使用您選擇的DRM解決方案（PlayReady、Widevine、FairPlay、存取等）來保護視訊:

* [Adobe Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [ExpressPlay Packager](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. 封裝或取得內容以用於測試您的設定。

   封裝時需要記住的一個要點是，您在此封裝步驟中使用的金鑰ID（內容ID）與您在後續的授權Token要求中必須提供的ID相同。 Key ID是唯一識別CEK的項目(可能會儲存在您自己的金鑰管理資料庫中，或是使用 [ExpressPlay的Key Storage Service儲存](https://www.expressplay.com/developer/key-storage/)。

   >[!NOTE]
   >
   >對於熟悉Adobe Access的人而言，這是不同解決方案運作方式的重要差異。 在Access中，授權金鑰內嵌在DRM中繼資料中，並與受保護的內容來回傳遞。 在此處所述的多DRM系統中，實際的授權不會傳遞，而是會安全地儲存並透過金鑰ID取得。

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

以下是使用Adobe Offline Packager for Widevine的封裝範例。 Packager使用配置檔案(例如 [!DNL widevine.xml])，其外觀類似：

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

* `in_path` -此入口指向您本機封裝機器上來源視訊的位置。
* `out_type` -此條目描述打包輸出的類型，在本例中為DASH（用於HTML5上的Widevine保護）。
* `out_path` -您希望輸出移至本機電腦的位置。
* `drm_sys` -您要封裝的DRM解決方案。 這可以是 `widevine`、 `fairplay`或 `playready`。

* `frag_dur` 和是 `target_dur` 與視訊播放相關的DASH特定持續時間項目。

* `key_file_path` -此為授權檔案在包裝機器上的位置，用作您的內容加密金鑰(CEK)。 它是Base-64編碼的16位元組十六進位字串。
* `widevine_content_id` -這是Widevine的「沸點板」;總是這樣 `2a`。 (請勿將此與混淆 `widevine_key_id`。)

* `widevine_provider` -為了我們的目的，請始終將此設定為 `intertrust`。

* `widevine_key_id` -這是您在條目中指定的許可證的標 `key_file_path` 識符。 換言之，這可識別您用來加密內容的金鑰。 此ID是您自行建立的16位元組HEX字串。

如 [Packager檔案所述](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf),「最佳實務是，建立組態檔，其中包含您要用來產生輸出的常用選項。 然後，通過提供特定選項作為命令行參數來建立輸出。」 在這種情況下，我們的配置檔案相當完整，因此您可以按如下方式建立輸出：

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>命令行參數優先於配置檔案參數。 在此示例中，所需的一切都在配置檔案中，但我們已使用覆蓋在配置檔案中指定的輸出路徑 `-out_path test_dash/`。

