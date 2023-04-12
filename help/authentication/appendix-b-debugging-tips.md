---
title: 附錄B "調試提示"
description: 附錄B "調試提示"
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 附錄B:除錯提示 {#appendix-b-debugging-tips}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


## 清除臨時資料 {#clearing-temporary-data}

Adobe Primetime驗證會儲存暫時資料，例如瀏覽器快取、LSO快取和Cookie。 清除臨時資料非常重要，以確保在測試時可以顯示空白。

- [清除瀏覽器快取和Cookie](#clearing-the-browser-cache-and-cookies)
- [清除LSOs快取](#clearing-lsos-cache)\
    

## 清除瀏覽器快取和Cookie {#clearing-the-browser-cache-and-cookies}

瀏覽器可靠，但在Firefox中：&quot;Tools&quot; -\> &quot;Clear Recent History...&quot; -\>在&quot;Time range to clear:&quot;上，選擇&quot;Everything&quot;;和「細節」上：檢查「Cookie」和「快取」 — \>按一下「立即清除」。\
 

## 清除LSOs快取 {#clearing-lsos-cache}

存取 [Flash Player說明](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html).

選取 ```entitlement.\*``` （視測試內容而定），然後按一下「刪除網站」。\
 

## 偵錯工具 {#tools}

Adobe Primetime驗證工程師使用下列除錯工具：

- Firebug - <http://www.getfirebug.com/>
- Flashbug（適用於Flash播放器的除錯版本） <https://addons.mozilla.org/en-US/firefox/addon/14465/>
- 即時http標題 —  <https://addons.mozilla.org/en-US/firefox/addon/3829/>
- Fiddler - <http://www.fiddler2.com/fiddler2/>
- 查爾斯 —  <http://www.charlesproxy.com/>
- Wireshark - <http://www.wireshark.org/>


<!--
## Related Information

- [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md)

- [Using Charles Proxy (Tech Note)](https://tve.zendesk.com/hc/en-us/articles/204962849-Using-Charles-Proxy)
-->