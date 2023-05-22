---
title: 附錄B 「調試提示」
description: 附錄B 「調試提示」
exl-id: ea024797-315e-47c0-99ea-1ac49c8c9697
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 附錄B:調試提示 {#appendix-b-debugging-tips}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。


## 清除臨時資料 {#clearing-temporary-data}

Adobe Primetime認證儲存瀏覽器快取、LSO快取和cookie等臨時資料。 清除臨時資料非常重要，以確保在測試時獲得一張白紙。

- [清除瀏覽器快取和Cookie](#clearing-the-browser-cache-and-cookies)
- [清除LSO快取](#clearing-lsos-cache)\
    

## 清除瀏覽器快取和Cookie {#clearing-the-browser-cache-and-cookies}

瀏覽器是可靠的，但在火狐：&quot;Tools&quot; -\> &quot;Clear Recent History...&quot; -\>在&quot;Time range to clear:&quot;上選擇&quot;Everything&quot;;和「詳細資訊」：選中「Cookie」和「Cache」 -\>按一下「立即清除」。\
 

## 清除LSO快取 {#clearing-lsos-cache}

訪問 [Flash Player幫助](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html)。

選擇 ```entitlement.\*``` （取決於測試的內容），然後按一下「刪除網站」。\
 

## 調試工具 {#tools}

Adobe Primetime認證工程師使用以下調試工具：

- 火蟲 —  <http://www.getfirebug.com/>
- Flashbug（與Flash Player的調試版一起使用） <https://addons.mozilla.org/en-US/firefox/addon/14465/>
- Live http標頭 —  <https://addons.mozilla.org/en-US/firefox/addon/3829/>
- Fiddler - <http://www.fiddler2.com/fiddler2/>
- 查爾斯。 <http://www.charlesproxy.com/>
- Wireshark - <http://www.wireshark.org/>


<!--
## Related Information

- [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md)

- [Using Charles Proxy (Tech Note)](https://tve.zendesk.com/hc/en-us/articles/204962849-Using-Charles-Proxy)
-->
