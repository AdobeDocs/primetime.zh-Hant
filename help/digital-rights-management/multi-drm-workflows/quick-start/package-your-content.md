---
description: 封裝內容是準備視訊內容以供透過網路播放的程式。 封裝包括將原始視訊轉換為資訊清單檔案，以及選擇使用不同裝置和瀏覽器的不同DRM解決方案來加密內容。
title: 封裝您的內容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 封裝您的內容 {#package-your-content}

封裝內容是準備視訊內容以供透過網路播放的程式。 封裝包括將原始視訊轉換為資訊清單檔案，以及選擇使用不同裝置和瀏覽器的不同DRM解決方案來加密內容。

若要準備您的內容，您可以使用AdobeOffline Packager或其他工具，例如ExpressPlay的Bento4封裝程式。 封裝者會準備視訊以進行播放（例如，將原始檔案分割並放入資訊清單），並使用您選擇的DRM解決方案（PlayReady、Widevine、FairPlay、Access等）來保護視訊:

* [Adobe離線封裝程式](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [ExpressPlay封裝](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. 封裝或以其他方式取得內容以用於測試您的設定。

   封裝時請謹記的一個要點，就是您在此封裝步驟中使用的金鑰ID （內容ID）與您後續的授權權杖請求中必須提供的金鑰ID （內容ID）相同。 金鑰ID是唯一可識別您CEK的專案(可儲存在您自己的金鑰管理資料庫中，或透過以下方式儲存： [ExpressPlay的金鑰儲存服務](https://www.expressplay.com/developer/key-storage/).

   >[!NOTE]
   >
   >對於熟悉Adobe存取的人來說，這是不同解決方案運作方式的重要差異。 在Access中，授權金鑰內嵌於DRM中繼資料中，並與受保護的內容來回傳遞。 在此說明的多DRM系統中，實際授權並未傳遞，而是安全地儲存並透過金鑰ID取得。

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

以下是使用Widevine的Adobe Offline Packager封裝範例。 封裝程式會使用組態檔(例如 [!DNL widevine.xml])，如下所示：

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

* `in_path`  — 此專案指向本機封裝電腦上的來源視訊位置。
* `out_type`  — 此專案說明封裝輸出的型別，在此例中為DASH (用於HTML5上的Widevine保護)。
* `out_path`  — 本機電腦上您要輸出輸出的位置。
* `drm_sys`  — 您封裝的DRM解決方案。 這將會是 `widevine`， `fairplay`，或 `playready`.

* `frag_dur` 和 `target_dur` 是與視訊播放相關的DASH特定期間專案。

* `key_file_path`  — 這是封裝電腦上用作內容加密金鑰(CEK)的授權檔案位置。 它是Base-64編碼的16位元組十六進位字串。
* `widevine_content_id`  — 這是Widevine的「樣板」；永遠是 `2a`. (請勿將此問題與 `widevine_key_id`.)

* `widevine_provider`  — 針對我們的目的，請一律將此專案設為 `intertrust`.

* `widevine_key_id`  — 這是您在「 」中指定的授權識別碼 `key_file_path` 登入點。 換言之，這可以識別您用來加密內容的金鑰。 此ID是您自行建立的16位元組HEX字串。

如 [Packager檔案](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)，「最佳實務是建立包含您要用於產生輸出的常用選項的設定檔。 然後，提供特定選項作為命令列引數來建立輸出。」 在此案例中，我們的設定檔案相當完整，因此您可以建立您的輸出，如下所示：

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>命令列引數的優先順序高於設定檔案引數。 在此範例中，所有必要專案都在設定檔案中，但我們已使用覆寫在設定檔案中指定的輸出路徑 `-out_path test_dash/`.
