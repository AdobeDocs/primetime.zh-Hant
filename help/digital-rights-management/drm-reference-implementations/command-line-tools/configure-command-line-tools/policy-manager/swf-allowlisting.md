---
title: SWF應用程式允許清單
description: SWF應用程式允許清單
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# SWF應用程式允許清單 {#swf-application-allowlisting}

若要允許列出SWF應用程式，您可以遵循以下兩種策略之一：

* 您可以指定SWF的URL。 這是一種非常靈活的方法，尤其是在您定期重建SWF的開發環境中。
* 您可以指定SWF雜湊。 這是您SWF的密碼編譯摘要值。 此方法較不靈活（但更為嚴格），因為應用程式變更並重新建置時，SWFHASH將會變更。 在此情況下，與先前雜湊繫結的所有內容將無法在新播放器上播放，且必須重新封裝。 此 [!DNL PolicyManager.jar] 如果您指定 [!DNL .swf] 檔案。

  另一方面，如果您是透過Flash/Adobe Media Server(FMS/AMS)使用Primetime DRM，您可以提供您特定SWF的路徑，FMS/AMS會自動將SWF雜湊成插入用來封裝FMS/AMS串流內容的DRM政策。

另請參閱 `policy.allowedSWFApplication.n` 在 *設定屬性* 以取得詳細資訊。
