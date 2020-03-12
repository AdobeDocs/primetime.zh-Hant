---
seo-title: SWF應用程式白名單
title: SWF應用程式白名單
uuid: e3021ae9-54f4-4bcf-a274-515ae765f74b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# SWF應用程式白名單{#swf-application-whitelisting}

若要將SWF應用程式列入白名單，您可以遵循下列兩種策略之一：

* 您可以指定SWF的URL。 這是非常有彈性的方式，尤其是在您定期重建SWF的開發環境中。
* 您可以指定SWF雜湊。 這是SWF的加密摘要值。 此方法不那麼靈活（但要嚴格得多），因為當應用程式變更並重建時，SWF雜湊會改變。 在此情況下，系結至先前HASH的所有內容將無法在新播放器上播放，而且必須重新封裝。 如果 [!DNL PolicyManager.jar] 您指定檔案，工具會自動計算雜 [!DNL .swf] 湊。

   另一方面，如果您透過Flash/Adobe Media Server(FMS/AMS)使用Primetime DRM，則可提供特定SWF的路徑，而FMS/AMS會自動雜湊SWF，讓您插入DRM政策，以封裝FMS/AMS串流的內容。

如需詳 `policy.allowedSWFApplication.n` 細資 *訊，請參閱* 「設定屬性」。
