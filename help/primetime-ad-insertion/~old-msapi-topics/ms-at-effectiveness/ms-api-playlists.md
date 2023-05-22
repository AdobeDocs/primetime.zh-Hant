---
description: 清單伺服器返回M3U8格式的主播放清單，符合建議的HTTP即時流標準。 它由一組變型傳輸流(TS)組成，每個流包含針對不同比特率和格式的相同內容的格式副本。 Adobe Primetime廣告插入添加了EXT-X-MARKER指令標籤，由客戶端視頻播放器進行解釋。
title: EXT-X-MARKER指令
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# EXT-X-MARKER指令 {#ext-x-marker-directive}

清單伺服器返回M3U8格式的主播放清單，符合建議的HTTP即時流標準。 它由一組變型傳輸流(TS)組成，每個流包含針對不同比特率和格式的相同內容的格式副本。 Adobe Primetime廣告插入添加了EXT-X-MARKER指令標籤，由客戶端視頻播放器進行解釋。

有關EXT-X-MARKER標籤的詳細資訊，請參見 [Adobe PrimetimeHTTP即時流式處理配置檔案](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf)。

>[!NOTE]
>
>僅當引導清單伺服器URL不包含 `pttrackingmode` 的下界。

>[!NOTE]
>
>EXT-X-MARKER標籤被添加到廣告段而不是內容段。

標準草稿位於 [HTTP即時流](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) 描述變型播放清單的內容和格式。 EXT-X-MARKER標籤指示客戶端調用回調。 它包含以下元件：

* **ID** 程式流上下文中此回調事件的唯一標識符（字串）。

* **類型** 回調事件的類型（字串）:PodBegin、PodEnd、PrerollPodBegin、PrerollPodEnd或AdBegin

* **持續時間** 從攜帶指令仍然有效的標籤的段開始開始的時間長度（秒）。

* **偏移** 可選。 在必須調用回調時，相對於段回放開始的偏移量（秒）。

   * `PodBegin` 和 `PrerollPodBegin` 包含DATA屬性中的信標資訊，並在段開始時激發。 所以 `OFFSET` 此處不提供標籤。

   * `AdBegin` 包含DATA屬性中的信標資訊，在該段的開頭觸發印象標籤。 所以 `OFFSET` 此處也不提供標籤。

   * `PodEnd` 和 `PrerollPodEnd` 包含DATA屬性中的信標資訊，但在當前段的末尾激發，因為這些標籤預期在pod中最後一個廣告的末尾激發。 在這個例子中， `OFFSET` 設定為 `<duration of segment>` 指定在當前段結束時激發信標。

* **資料** Base64編碼的字串，用雙引號括起來，其中包含調用回調時要傳遞給應用程式的資料。 它包含符合VMAP1.0和VAST3.0規範的廣告跟蹤資訊。

* **計數** 在廣告分段中將縫製的廣告數。

   僅當TYPE元件設定為PodBegin或PrerollPodBegin時，才適用。

* **佈雷克杜爾** 填充廣告分段的總持續時間（秒）。

   僅當TYPE元件設定為PodBegin或PrerollPodBegin時，才適用。

構建回調時，按如下方式解釋EXT-X-MARKER元件：

* 當標籤包含 `OFFSET`，在指定的偏移量處觸發回調，該偏移量相對於該段中內容回放的開始。 否則，當該段中的內容開始播放時立即觸發回調。
* 使用 `DURATION` 跟蹤廣告內容的進度並請求跟蹤事件的URL。
* 通過 `ID`。 `TYPE`, `DATA` 回電。

使用 `PrerollPodBegin`, `PrerollPodEnd` 值 `TYPE` 確定在即時/線性流中首先播放的TS段。

>[!NOTE]
>
>的 `PrerollPodBegin`, `PrerollPodEnd` 僅當預滾動廣告插入即時流時，值才可用。

清單伺服器包括以下段中的EXT-X-MARKER標籤：

* 廣告片段的第一段，用於跟蹤廣告莢的開始。
* 廣告的第一段，用於跟蹤廣告盒內單個廣告的開始/完成/進度。
* 廣告片段的最後一段，用於跟蹤廣告盒的結尾。

清單伺服器發送 `VMAP1.0-conformant` XML文檔，用於跟蹤每個廣告分段的開始和結束。 它是廣告伺服器返回的實際VMAP1.0響應的篩選版本，主要包含跟蹤事件，如下所示：

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<vmap:VMAP xmlns:vmap="https://www.iab.net/vmap-1.0" version="1.0"> 
    <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start"> 
        <vmap:TrackingEvents> 
            <vmap:Tracking event="breakStart"> 
                https://MyServer.com/breakstart.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="breakEnd"> 
                https://MyServer.com/breakend.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="error"> 
                https://MyServer.com/error.gif 
            </vmap:Tracking> 
        </vmap:TrackingEvents> 
    </vmap:AdBreak> 
</vmap:VMAP> 
</AdTrackingFragment> 
</AdTrackingFragments>
```

對於每個廣告，清單伺服器插入程式內容，它發送一個VAST3.0一致的XML文檔來跟蹤該廣告。 每個XML文檔都包含 `<InLine>` 描述線性和創造性插入的元素，或 `<Wrapper>` 包裝廣告（即連結或重定向廣告）和任何相關的伴生廣告和擴展。 如果VAST響應包含序列屬性，例如當廣告是廣告盒的一部分時，文檔將包含該屬性。 以下是用於跟蹤單個廣告的VAST3.0一致XML文檔示例：

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<VAST xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"  
      version="3.0"  
      xsi:noNamespaceSchemaLocation="https://service.videoplaza.com/schema/iab/vast-3.0.xsd"> 
<Ad id="903395"> 
    <InLine> 
      <AdSystem version="1.0">Auditude</AdSystem> 
      <AdTitle/> 
      <Error>https://ad.qa.auditude.com/adserver/?ErrAd1=[ERRORCODE]</Error> 
      <Impression id="urn:aeid:903395">https://ad.qa.auditude.com/adserver/e?type=adimp&amp; 
                 cid=127860991&amp; 
                 z=50183&amp; 
                 a=903395&amp; 
                 s=ef8c51dc&amp; 
                 t=1355309735&amp; 
                 w=100000&amp; 
                 uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                 l=1355280906&amp; 
                 u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                 br=1&amp; 
                 sq=1&amp; 
                 pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                 ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                               ?Cashcash=[CACHEBUSTING] 
                               ?Asset=[ASSETURI] 
      </Impression> 
      <Creatives> 
        <Creative> 
          <Linear> 
            <Duration>00:00:15</Duration> 
            <TrackingEvents> 
              ... 
              <Tracking event="firstQuartile"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=25&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking>                
              <Tracking event="midpoint"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=50&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="firstQuartile"> 
                https://www.Tweeeen.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                       ?Cashcash=[CACHEBUSTING] 
                                       ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="midpoint"> 
                https://www.Fiftyyyy.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                        ?Cashcash=[CACHEBUSTING] 
                                        ?Asset=[ASSETURI] 
              </Tracking> 
              ... 
            </TrackingEvents> 
            <VideoClicks> 
              <ClickTracking> 
                https://www.MP4-Vid-ClickTrack.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                                  ?Cashcash=[CACHEBUSTING] 
                                                  ?Asset=[ASSETURI] 
              </ClickTracking> 
              <ClickThrough> 
                https://www.cnn.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                   ?Cashcash=[CACHEBUSTING] 
                                   ?Asset=[ASSETURI] 
              </ClickThrough> 
              ... 
            </VideoClicks> 
            <AdParameters>campaign_id=7012</AdParameters> 
            <MediaFiles> 
              ...            
            </MediaFiles> 
          </Linear> 
        </Creative> 
        <Creative> 
          <CompanionAds> 
            <Companion id="103" width="300" height="250"> 
              <StaticResource creativeType="image/jpeg"> 
                https://ad.qa.auditude.com/adserver/c/z=50183; 
                  l=1355280906; 
                  u=956c3cd141086a1da44dcae8ea4ed14a; 
                  uid=_CxLm0b1SeKD8KXco__5TQ; 
                  cid=127860991; 
                  s=ef8c51dc; 
                  t=1355309735; 
                  br=1; 
                  sq=1; 
                  pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur 
                    %3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8; 
                  ax=0%2c0%2c1720%2c0; 
                  w=100000; 
                  a=903395; 
                  a1=103/c300x250.jpeg 
              </StaticResource> 
              <CompanionClickThrough> 
                https://ad.qa.auditude.com/adserver/l/a=903395%3Ba1=103 
                  %3Ba2=1%3Bz=50183%3Bl=1355280906%3Bu=956c3cd141086a1da44dcae8ea4ed14a 
                  %3Bcid=127860991%3Bs=ef8c51dc%3Buid=_CxLm0b1SeKD8KXco__5TQ 
                  %3Bt=1355309735%3Bbr=1%3Bsq=1%3Bpod=id%3a1%2cctype%3al%2cptype 
                  %3ap%2cdur%3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8 
                  %3Bax=0%2c0%2c1720%2c0 
              </CompanionClickThrough> 
              <AdParameters>campaign_id=7012</AdParameters> 
            </Companion> 
          </CompanionAds> 
        </Creative> 
        ... 
      </Creatives> 
      <Extensions> 
        <Extension type="Behavior"> 
          ... 
        </Extension> 
      </Extensions> 
    </InLine> 
  </Ad> 
  </VAST> 
</AdTrackingFragment> 
</AdTrackingFragments> 
```
