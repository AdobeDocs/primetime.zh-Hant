---
description: 資訊清單伺服器會傳回M3U8格式的主播放清單，符合建議的HTTP即時資料流標準。 它包含一組變體傳輸資料流(TS)，每個資料流都包含相同內容的轉譯以供不同的位元速率和格式使用。 Adobe Primetime廣告插入會新增EXT-X-MARKER指示詞標籤，以供使用者端視訊播放器解譯。
title: EXT-X-MARKER指令
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# EXT-X-MARKER指令 {#ext-x-marker-directive}

資訊清單伺服器會傳回M3U8格式的主播放清單，符合建議的HTTP即時資料流標準。 它包含一組變體傳輸資料流(TS)，每個資料流都包含相同內容的轉譯以供不同的位元速率和格式使用。 Adobe Primetime廣告插入會新增EXT-X-MARKER指示詞標籤，以供使用者端視訊播放器解譯。

如需EXT-X-MARKER標籤的詳細資訊，請參閱 [Adobe Primetime HTTP Live Streaming Profile](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>只有啟動程式資訊清單伺服器URL不包含 `pttrackingmode` 引數。

>[!NOTE]
>
>EXT-X-MARKER標籤會新增至廣告區段，而非內容區段。

草稿標準位於 [HTTP即時資料流](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) 說明變體播放清單的內容和格式。 EXT-X-MARKER標籤會指示使用者端叫用回呼。 它包含下列元件：

* **ID** 程式串流內容中此回呼事件的唯一識別碼（字串）。

* **型別** 回呼事件的型別（字串）： PodBegin、PodEnd、PrerollPodBegin、PrerollPodEnd或AdBegin

* **持續時間** 從攜帶指示詞對其保持有效之標籤的區段開始算起的時間長度（以秒為單位）。

* **位移** 選填。 必須叫用回呼時，相對於區段播放開始的位移（以秒為單位）。

   * `PodBegin` 和 `PrerollPodBegin` 包含DATA屬性中的信標資訊，並在區段開頭引發。 因此 `OFFSET` 標籤在這裡無法使用。

   * `AdBegin` 包含DATA屬性中的信標資訊，而曝光標籤會在該區段開頭引發。 因此 `OFFSET` 標籤在此也不可用。

   * `PodEnd` 和 `PrerollPodEnd` 包含DATA屬性中的信標資訊，但會在目前區段結尾引發，因為這些標籤預期會在Pod中最後一個廣告區段的結尾引發。 在這種情況下， `OFFSET` 設為 `<duration of segment>` ，以指定在目前區段的結尾引發信標。

* **資料** 以雙引號括住的Base64編碼字串，其中包含要在叫用回呼時傳遞至應用程式的資料。 其中包含符合VMAP1.0和VAST3.0規格的廣告追蹤資訊。

* **計數** 將在廣告插播中拼接的廣告數量。

   僅適用於TYPE元件設為PodBegin或PrerollPodBegin時。

* **BREAKDUR** 已填入廣告插播的總持續時間（以秒為單位）。

   僅適用於TYPE元件設為PodBegin或PrerollPodBegin時。

建構回呼時，請將EXT-X-MARKER元件解譯如下：

* 當標籤包含 `OFFSET`，會在相對於該區段中內容播放開始的指定位移處觸發回呼。 否則，只要該區段中的內容開始播放，就會立即觸發回呼。
* 使用 `DURATION` 以追蹤廣告內容的進度，並要求用於追蹤事件的URL。
* 通過 `ID`， `TYPE`、和 `DATA` 至回呼。

使用 `PrerollPodBegin`、和 `PrerollPodEnd` 值 `TYPE` 決定要在即時/線性資料流中首先播放哪個TS區段。

>[!NOTE]
>
>此 `PrerollPodBegin`、和 `PrerollPodEnd` 只有在將前段廣告插入即時資料流時，才可使用值。

資訊清單伺服器包含EXT-X-MARKER標籤，位於下列區段中：

* 廣告插播中的第一個區段，用於追蹤廣告Pod的開始。
* 廣告的第一個區段，用於追蹤廣告Pod中個別廣告的開始/完成/進度。
* 廣告插播中的最後一個區段，用於追蹤廣告Pod的結尾。

資訊清單伺服器傳送 `VMAP1.0-conformant` 追蹤每個廣告插播開始和結束的XML檔案。 這是廣告伺服器傳回的實際VMAP1.0回應的篩選版本，主要包含追蹤事件，如下所示：

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

資訊清單伺服器會針對插入程式內容中的每個廣告創意，傳送VAST3.0-conformant XML檔案以追蹤該廣告。 每個XML檔案都包含 `<InLine>` 說明插入線性廣告創意的元素，或 `<Wrapper>` 元素（包裝廣告） （亦即連結或重新導向的廣告）以及任何關聯的隨附廣告和副檔名。 如果VAST回應包含序列屬性（例如，當廣告是廣告Pod的一部分時），則檔案會包含該屬性。 以下是追蹤個別廣告的VAST3.0-conformant XML檔案範例：

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
