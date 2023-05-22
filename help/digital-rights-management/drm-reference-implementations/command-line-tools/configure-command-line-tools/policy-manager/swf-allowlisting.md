---
title: SWF應用程式允許清單
description: SWF應用程式允許清單
copied-description: true
exl-id: ae8b7f52-897f-43f9-ac7b-665d4b8c16b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# SWF應用程式允許清單 {#swf-application-allowlisting}

要允許列出SWF應用程式，可以遵循以下兩種策略之一：

* 可以指定SWF的URL。 這是一種非常靈活的方法，尤其是在您定期重建SWF的開發環境中。
* 可以指定SWFHASH。 這是您的SWF的加密摘要值。 此方法不那麼靈活（但要嚴格得多），因為SWFHASH將在應用程式更改和重建時更改。 在這種情況下，綁定到先前HASH的所有內容將無法在新播放器上播放，並且必須重新打包。 的 [!DNL PolicyManager.jar] 如果您指定 [!DNL .swf] 的子菜單。

   另一方面，如果您通過Flash/Adobe Medium伺服器(FMS/AMS)使用黃金時段DRM，則可以提供指向特定SWF的路徑，FMS/AMS將自動散列SWF，以便您插入DRM策略，該策略用於打包由FMS/AMS流式傳輸的內容。

請參閱 `policy.allowedSWFApplication.n` 在 *配置屬性* 的雙曲餘切值。
