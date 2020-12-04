---
description: 資訊清單伺服器會傳回M3U8格式的主播放清單，符合建議的HTTP即時串流標準。 它由一組變型傳輸流(TS)組成，每組傳輸流包含針對不同比特率和格式的相同內容的轉譯。 Adobe Primetime廣告插入新增EXT-X-MARKER指令標籤，以供用戶端視訊播放器解讀。
seo-description: 資訊清單伺服器會傳回M3U8格式的主播放清單，符合建議的HTTP即時串流標準。 它由一組變型傳輸流(TS)組成，每組傳輸流包含針對不同比特率和格式的相同內容的轉譯。 Adobe Primetime廣告插入新增EXT-X-MARKER指令標籤，以供用戶端視訊播放器解讀。
seo-title: EXT-X-MARKER指令
title: EXT-X-MARKER指令
uuid: e349bf89-b196-47b4-a362-9913fa28b2c6
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---


# EXT-X-MARKER指令{#ext-x-marker-directive}

資訊清單伺服器會傳回M3U8格式的主播放清單，符合建議的HTTP即時串流標準。 它由一組變型傳輸流(TS)組成，每組傳輸流包含針對不同比特率和格式的相同內容的轉譯。 Adobe Primetime廣告插入新增EXT-X-MARKER指令標籤，以供用戶端視訊播放器解讀。

如需EXT-X-MARKER標籤的詳細資訊，請參閱[Adobe Primetime HTTP Live Streaming Profile](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf)。

>[!NOTE]
>
>只有當引導資料庫資訊清單伺服器URL不包含`pttrackingmode`參數時，才可使用此功能。

>[!NOTE]
>
>EXT-X-MARKER標籤會新增至廣告區段，而非內容區段。

[HTTP即時串流](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23)的草稿標準說明變型播放清單的內容和格式。 EXT-X-MARKER標籤指示客戶端調用回調。 它包含下列元件：

* **程** 式串流內容中此回呼事件的IDU唯一識別碼（字串）。

* **回** 呼事件的TYPEype（字串）:PodBegin、PodEnd、PrerollPodBegin、PrerollPodEnd或AdBegin

* **** DURATIONL從帶有指令仍然有效的標籤的段的開頭開始的時間長度（以秒為單位）。

* **OFFSETO** 可選。必須呼叫回呼時，相對於區段播放開始的偏移（以秒為單位）。

   * `PodBegin` 和 `PrerollPodBegin` 在DATA屬性中包含信標資訊，並在區段開始時引發。因此，`OFFSET`標籤不在此處可用。

   * `AdBegin` 包含DATA屬性中的信標資訊，而曝光標籤會在區段開始時引發。因此，`OFFSET`標籤也不在此處提供。

   * `PodEnd` 和 `PrerollPodEnd` 在DATA屬性中包含信標資訊，但會在目前區段的結尾引發，因為這些標籤預期會在pod中最後一個廣告的最後區段結束時引發。在此例中，`OFFSET`設為`<duration of segment>`，以指定信標會在目前區段的結尾處引發。

* **在** 呼叫回呼時，以雙引號括住的DATABase64編碼字串，包含要傳遞至應用程式的資料。它包含符合VMAP1.0和VAST3.0規格的廣告追蹤資訊。

* **COUNT** 廣告分段中將銜接的廣告數量。

   僅當TYPE元件設定為PodBegin或PrerollPodBegin時才適用。

* **** BREAKDURTotal填入廣告插播的持續時間（以秒為單位）。

   僅當TYPE元件設定為PodBegin或PrerollPodBegin時才適用。

構造回呼時，請按如下方式解譯EXT-X-MARKER元件：

* 當標籤包含`OFFSET`時，在指定的偏移處觸發回呼，該偏移與該區段中的內容播放的開始位置相關。 否則，當該區段中的內容開始播放時，就會立即觸發回呼。
* 使用`DURATION`來追蹤廣告內容的進度，並請求URL以追蹤事件。
* 將`ID`、`TYPE`和`DATA`傳遞至回呼。

使用`PrerollPodBegin`和`PrerollPodEnd`的`TYPE`值來確定在即時／線性流中首先播放的TS段。

>[!NOTE]
>
>`PrerollPodBegin`和`PrerollPodEnd`值僅在前滾廣告插入即時串流時可用。

資訊清單伺服器在下列區段中包含EXT-X-MARKER標籤：

* 廣告分段中的第一個區段，用來追蹤廣告Pod的開頭。
* 廣告的第一個區段，用來追蹤廣告Pod中個別廣告的開始／完成／進度。
* 廣告分段中追蹤廣告pod結尾的最後一個區段。

資訊清單伺服器會傳送`VMAP1.0-conformant` XML檔案，以追蹤每個廣告插播的開始和結束。 它是廣告伺服器傳回的實際VMAP1.0回應的篩選版本，主要包含下列追蹤事件：

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

資訊清單伺服器會針對每個廣告創意插入程式內容，傳送VAST3.0相容的XML檔案來追蹤該廣告。 每個XML檔案包含描述插入線性廣告創意的`<InLine>`元素，或包裝函式廣告（即連結或重新導向廣告）的`<Wrapper>`元素，以及任何相關的配套廣告和擴充功能。 如果VAST回應包含序列屬性，例如當廣告是廣告pod的一部分時，檔案會包含該屬性。 以下是追蹤個別廣告的範例VAST3.0相容XML檔案：

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
