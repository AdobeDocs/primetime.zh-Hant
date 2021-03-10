---
title: SWF應用程式允許清單
description: SWF應用程式允許清單
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# SWF應用程式允許列出{#swf-application-allowlisting}

若要允許列出SWF應用程式，您可以遵循下列兩種策略之一：

* 您可以指定SWF的URL。 這是非常有彈性的方式，尤其是在您定期重建SWF的開發環境中。
* 您可以指定SWF雜湊。 這是SWF的加密摘要值。 此方法不那麼靈活（但要嚴格得多），因為當應用程式變更並重建時，SWF雜湊會改變。 在此情況下，系結至先前HASH的所有內容將無法在新播放器上播放，而且必須重新封裝。 如果您指定[!DNL .swf]檔案，[!DNL PolicyManager.jar]工具會自動計算雜湊。

   另一方面，如果您透過Flash/Adobe Medium伺服器(FMS/AMS)使用Primetime DRM，則可提供特定SWF的路徑，而FMS/AMS會自動雜湊SWF，讓您插入DRM原則，以封裝FMS/AMS串流的內容。

如需詳細資訊，請參閱&#x200B;*Configuration properties*&#x200B;中的`policy.allowedSWFApplication.n`。
