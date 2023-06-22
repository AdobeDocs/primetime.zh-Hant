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

若要允許列出SWF應用程式，您可以遵循以下兩種策略之一：

* 您可以指定SWF的URL。 這是一種非常靈活的方法，尤其是在您定期重建SWF的開發環境中。
* 您可以指定SWF雜湊。 這是您SWF的密碼編譯摘要值。 此方法較不靈活（但更為嚴格），因為應用程式變更並重新建置時，SWFHASH會變更。 在此情況下，所有繫結至先前HASH的內容將無法在新播放器上播放，且必須重新封裝。 此 [!DNL PolicyManager.jar] 如果您指定 [!DNL .swf] 檔案。

   另一方面，如果您透過Flash/Adobe Medium伺服器(FMS/AMS)使用Primetime DRM，您可以提供特定SWF的路徑，FMS/AMS會自動雜湊這些SWF，供您插入用來封裝FMS/AMS串流內容的DRM原則。

另請參閱 `policy.allowedSWFApplication.n` 在 *設定屬性* 以取得詳細資訊。
