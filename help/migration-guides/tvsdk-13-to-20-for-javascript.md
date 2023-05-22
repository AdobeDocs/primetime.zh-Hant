---
title: TVSDK轉換 — 1.3到2.0（對於JavaScript）
description: 2.0的許多方法簽名和API元素名稱已更改。查看這些表以查看所有API更改詳細資訊。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
exl-id: 4b251e26-cee6-4d96-bb55-6c47195da4d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---

# TVSDK轉換 — 1.3到2.0（對於JavaScript） {#tvsdk-conversion-to-for-javascript}

2.0的許多方法簽名和API元素名稱已更改。查看這些表以查看所有API更改詳細資訊。

## 在JavaScript中實現回調函式 {#implement-callback-functions-in-javascript}

方法文檔中的注釋建議您需要實施的回調簽名。

對於JavaScript,API語法基於Web ID。 對於TVSDK介面，方法名稱為 *方法名稱*()。 對於應用程式要實現的方法，調用了讀/寫屬性 *方法名稱*&#x200B;將CallbackFunc添加到介面中，您的應用程式應將其設定為指向實現該方法的函式。 例如：

```shell
// An app implementable interface
interface ContentFactory
{
    /*
     * AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item);
     */
    attribute Object retrieveAdPolicySelectorCallbackFunc;
 
    /*
     * ContentResolverList retrieveResolvers(MediaPlayerItem item);
     */
    attribute Object retrieveResolversCallbackFunc;
 
    /*
     * OpportunityGeneratorList retrieveGenerators(MediaPlayerItem item);
     */
    attribute Object retrieveGeneratorsCallbackFunc;
};

// this is how to implement it
var factory = new AdobePSDK.ContentFactory();
factory.retrieveAdPolicySelectorCallbackFunc = function(item)
{
    // return your adPolicySelector according to the item
    return adPolicySelector;
}
 
mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig ();
playerConfig.adFactory = factory;
// Use this config to load new MediaResource
```

## 2.0的廣告工作流API元素更改 {#advertising-workflow-api-element-changes-for}

這些表比較了1.3版和2.0版之間JavaScript TVSDK的廣告工作流API元素。

本主題中的表：

* TimedMetadata
* AdSigningMode
* 廣告元資料
* 自定義範圍元資料
* 替換時間範圍
* 放置
* 機會
* 保留
* 時間軸/時間軸項/時間軸標籤
* 廣告中斷
* Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakStatedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* 時間軸操作
* 廣告中斷放置
* 音頻設定

### TimedMetadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMetadata</strong>:介面TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0; <br /> const unsigned short METADATA_TYPE_ID3 = 1; <br /> 只讀屬性unsignedshort類型； <br /> 只讀屬性長時間；<br /> 只讀屬性DomString id;<br /> 只讀屬性DomString名稱；<br /> 只讀屬性DomString內容； <br /> 只讀屬性對象元資料；<br /> }; </p> </td> 
   <td><p>介面TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0;<br /> const unsigned short METADATA_TYPE_ID3 = 1;<br /> 只讀屬性unsigned short metadataType;<br /> 只讀屬性長時間；<br /> 只讀屬性long id;<br /> 只讀屬性DomString名稱；<br /> <br /> 只讀屬性對象元資料；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>:（2.0無更改）</td> 
   <td><p>介面TimedMetadataList {<br /> 只讀屬性unsigned long length;<br /> GetterTimedMetadata（無符號長索引）;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdSigningMode {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AdSignlingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CUES , <br /> const unsigned short MODE_SERVER_MAP , <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>這將替換MetadataKeys::MANIFEST_CUES鍵。</td> 
  </tr> 
 </tbody> 
</table>

### 廣告元資料 {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面廣告元資料{ <br /> 屬性AdSigningMode; <br /> 屬性AdBreakStatedPolicy adBreakAsWatch; <br /> 屬性boolean livePreroll; <br /> 屬性布爾delayAdLoading; <br /> };</p> </td> 
   <td>此功能由<p>元資料鍵：:ADVERTISING_METADATA</p> 按鈕</td> 
  </tr> 
 </tbody> 
</table>

### 自定義範圍元資料 {#customrangemetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> 屬性unsigned short type; <br /> 屬性布爾adjustSeekPosition; <br /> 屬性TimeRangeList timeRangeList; <br /> };</p> </td> 
   <td>（2.0的新增內容）</td> 
  </tr> 
 </tbody> 
</table>

### 替換時間範圍 {#replacetimerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面ReplaceTimeRange { <br /> 屬性unsigned long begin; <br /> 只讀屬性unsigned long end; <br /> 屬性unsigned long duration; <br /> attribute unsigned long replaceDuration; <br /> };</p> </td> 
   <td>（2.0的新增內容）</td> 
  </tr> 
 </tbody> 
</table>

### 放置 {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面放置{ <br /> const unsigned short TYPE_MID_ROLL; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> 只讀屬性unsignedshort類型； <br /> 只讀屬性長時間； <br /> 只讀屬性長持續時間； <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> 只讀屬性unsigned short模式； <br /> 只讀屬性TimeRange範圍； <br /> };</p> </td> 
   <td>（2.0的新增內容）</td> 
  </tr> 
 </tbody> 
</table>

### 機會 {#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面機會{ <br /> 只讀屬性DomString id; <br /> 只讀屬性放置； <br /> 只讀屬性對象設定； <br /> 只讀屬性對象customParameters; <br /> }; </p> </td> 
   <td>（2.0的新增內容）</td> 
  </tr> 
 </tbody> 
</table>

### 保留 {#reservation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面保留{ <br /> 只讀屬性TimeRange範圍； <br /> 只讀屬性長保持； <br /> }; </p> </td> 
   <td> （2.0的新增內容）</td> 
  </tr> 
 </tbody> 
</table>

### 時間軸/時間軸項/時間軸標籤 {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p><strong>時間軸</strong>:介面時間線 <br /> {只讀屬性TimelineMarkerList timelineMarkers; <br /> 只讀屬性TimelineItemList timelineItems; <br /> double convertToLocalTime（雙倍時間）; <br /> double convertToVirtualTime（雙倍時間）; <br /> };</p> </td> 
   <td><p>介面時間軸{<br /> 只讀屬性TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>時間軸項</strong>:介面TimelineItem :<br /> 時間軸標籤{<br /> 只讀屬性long id; <br /> 只讀屬性TimeRange virtualRange; <br /> 只讀屬性TimeRange localRange; <br /> 只讀屬性布爾值監視； <br /> 只讀屬性布爾臨時值 <br /> }; </p> </td> 
   <td>（2.0的新增內容）</td> 
  </tr> 
  <tr> 
   <td><strong>時間軸標籤</strong>:（2.0無更改）</td> 
   <td><p>介面TimelineMarker {<br /> 只讀屬性雙時間；<br /> 只讀屬性雙持續時間；<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 廣告中斷 {#adbreak}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AdBreak {<br /> <br /> <br /> <br /> 只讀屬性雙持續時間；<br /> 只讀屬性AdList廣告；<br /> <br /> <br /> 只讀屬性AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>介面AdBreak {<br /> 只讀屬性雙時間；<br /> 只讀屬性雙replaceDuration;<br /> <br /> 只讀屬性雙持續時間；<br /> 只讀屬性AdList adList;<br /> <br /> 只讀屬性DomString資料；<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>廣告</strong>:介面Ad {<br /> 只讀屬性AdAsset primaryAsset;<br /> 只讀屬性AdAssetList companionAssets;<br /> <br /> 只讀屬性雙持續時間；<br /> 只讀屬性DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0;<br /> const unsigned short ADTYPE_NON-LINEAR = 1;<br /> <br /> 只讀屬性unsigned short adType;<br /> 只讀屬性AdInsertionType adInsertionType; <br /> <br /> 只讀屬性布爾可按一下； <br /> 只讀屬性boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>介面Ad {<br /> 只讀屬性AdAsset primaryAsset;<br /> 只讀屬性AdAssetList companionAssets;<br /> <br /> 只讀屬性雙持續時間；<br /> 只讀屬性DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0;<br /> const unsigned short ADTYPE_NON-LINEAR = 1;<br /> <br /> 只讀屬性unsignedshort類型；<br /> 只讀屬性AdInsertionType insertionType; <br /> 只讀屬性對象跟蹤器；<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>廣告資產</strong>:（2.0無更改）</td> 
   <td><p>介面AdAsset {<br /> 只讀屬性DomString id;<br /> 只讀屬性雙持續時間；<br /> 只讀屬性MediaResource資源；<br /> 只讀屬性AdClick adClick;<br /> 只讀屬性對象元資料；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>廣告點擊</strong>:（2.0無更改）</td> 
   <td><p>介面AdClick {<br /> 只讀屬性DomString id;<br /> 只讀屬性DomString標題；<br /> 只讀屬性DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>廣告清單</strong>:（2.0無更改）</td> 
   <td><p>介面AdList {<br /> 只讀屬性unsigned long length;<br /> getter Ad（無符號長索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>廣告資產清單</strong>:（2.0無更改）</td> 
   <td><p>介面AdAssetList {<br /> 只讀屬性unsigned long length;<br /> GetterAdAsset（無符號長索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>:介面AdBannerAsset :廣告資產<br /> { 0}<br /> 只讀屬性int width;<br /> 只讀屬性int height;<br /> 只讀屬性DomString staticUrl;<br /> 只讀屬性DomString高度；<br /> 只讀屬性DomString寬度；<br /> };</p> </td> 
   <td> 2.0中新增</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakTimelineItem / AdTimelineItem {#adbreaktimelineitem-adtimelineitem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>AdBreakTimelineItem</strong>:介面AdBreakTimelineItem :時間軸項{ <br /> 只讀屬性AdBreak adBreak; <br /> 只讀屬性AdTimelineItemList項； <br /> }; </p> </td> 
   <td> （2.0的新增內容）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimeline項</strong>:介面AdTimelineItem :時間軸項{ <br /> 只讀屬性AdBreak adBreak; <br /> 只讀屬性Ad; <br /> }; </p> </td> 
   <td> （2.0的新增內容）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>:介面AdBreakTimelineItemList { <br /> 只讀屬性unsigned long length; <br /> GetterAdBreakTimelineItem（未簽名的long索引）; <br /> };</p> </td> 
   <td> （2.0的新增內容）</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakStatedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AdBreakPolicy {<br /> 只讀屬性short AD_BREAK_POLICY_SKIP;<br /> 只讀屬性short AD_BREAK_POLICY_PLAY;<br /> 只讀屬性short AD_BREAK_POLICY_REMOVE;<br /> 只讀屬性short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> 介面AdPolicyConstants {<br /> 只讀屬性short AD_BREAK_POLICY_SKIP;<br /> 只讀屬性short AD_BREAK_POLICY_PLAY;<br /> 只讀屬性short AD_BREAK_POLICY_REMOVE;<br /> 只讀屬性short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> 介面AdBreakStaedPolicy {<br /> 只讀屬性short AD_BREAK_AS_STATER_ON_BEGIN;<br /> 只讀屬性short AD_BREAK_AS_STAYD_ON_END;<br /> 只讀屬性short AD_BREAK_AS_STAYD_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> 只讀屬性short AD_BREAK_AS_STATER_ON_BEGIN;<br /> 只讀屬性short AD_BREAK_AS_STAYD_ON_END;<br /> 只讀屬性short AD_BREAK_AS_STAYD_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面AdPolicy {<br /> 只讀屬性short AD_POLICY_PLAY;<br /> 只讀屬性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> 只讀屬性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;只讀屬性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> 只讀屬性short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> 只讀屬性short AD_POLICY_PLAY;<br /> 只讀屬性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> 只讀屬性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> 只讀屬性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> 只讀屬性short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面AdPolicyMode {<br /> 只讀屬性short AD_POLICY_MODE_PLAY;<br /> 只讀屬性short AD_POLICY_MODE_SEEK;<br /> 只讀屬性short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly屬性short AD_POLICY_MODE_PLAY;<br /> 只讀屬性short AD_POLICY_MODE_SEEK;<br /> 只讀屬性short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面AdPolicyInfo {<br /> 只讀屬性AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> 只讀屬性AdTimelineItem adTimelineItem;<br /> 只讀屬性雙currentTime;<br /> 只讀屬性雙seekToTime;<br /> 只讀屬性雙速率；<br /> 只讀屬性短模式；//AdPolicyMode<br /> };</p> </td> 
   <td><p>介面AdPolicyInfo {<br /> 只讀屬性AdBreakPlacementList <br /> adBreakPlacements;<br /> 只讀屬性Ad;<br /> 只讀屬性雙currentTime;<br /> 只讀屬性雙seekToTime;<br /> 只讀屬性雙速率；<br /> 只讀屬性短模式；//AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 屬性Object selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 屬性對象selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> 屬性Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakStatedPolicy selectStatedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 屬性對象selectStatedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>介面AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 屬性對象selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 屬性對象selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> 屬性對象selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectStatedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> 屬性Object selectStatedPolicyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 時間軸操作 {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面TimelineOperation { <br /> 只讀屬性放置； <br /> };</p> </td> 
   <td> （2.0的新增內容）</td> 
  </tr> 
 </tbody> 
</table>

### 廣告中斷放置 {#adbreakplacement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AdBreakPlacement :時間軸操作{<br /> 只讀屬性AdBreak adBreak;<br /> 只讀屬性放置；//從時間軸操作<br /> 只讀屬性雙時間；<br /> 只讀屬性雙持續時間；<br /> };</p> </td> 
   <td><p>介面AdBreakPlacement {<br /> 只讀屬性AdBreak adBreak;<br /> 只讀屬性放置；<br /> 只讀屬性雙時間；<br /> 只讀屬性雙持續時間；<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 音頻設定 {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AuditySettings :廣告元資料{ <br /> 屬性DomString zoneId; <br /> 屬性DomString mediaId; <br /> 屬性DomString defaultMediaId ; <br /> 屬性DomString域； <br /> 屬性對象targettingInfo; <br /> 屬性對象customParameters; <br /> 屬性Boolean creativePackaingEnabled ;<br /> 屬性Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>功能由MetadataKeys::AUDITUDE_METADATA_KEY鍵提供。</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的自定義API元素更改 {#customization-api-element-changes-for}

這些表比較版本1.3和2.0之間的JavaScript TVSDK的自定義API元素。

本主題中的表：

* MediaPlayerItemConfig
* 內容工廠
* 網路配置

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面MediaPlayerItemConfig {<br /> 屬性ContentFactory adFactory;<br /> 屬性StringList subscribeTags;<br /> <br /> 屬性StringList adTags;<br /> <br /> <br /> 屬性AdSignlingMode adSigningMode;<br /> 屬性CustomRangeMetadata customRangeMetadata;<br /> 屬性NetworkConfiguration networkConfiguration;<br /> 屬性AdvertisingMetadata advertisingMetadata;<br /> 屬性Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>介面MediaPlayerConfig {<br /> <br /> <br /> <br /> 屬性StringList adTags;<br /> 屬性StringList subscripedTags;<br /> 屬性MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 內容工廠 {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem項);<br /> */<br /> 屬性Object retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>介面MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem項);<br /> */<br /> 屬性Object retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 網路配置 {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面網路配置<br /> { 0}<br /> 屬性boolean forceNativeNetworking;<br /> 屬性布爾useRedirectedUrl;<br /> 屬性Object CookieHeader;<br /> 屬性boolean readSetCookieHeader;<br /> 屬性int masterUpdateInterval; <br /> 屬性boolean useCookieHeaderForAllRequests;<br /> 屬性int readLimit;<br /> };</p> </td> 
   <td>在1.3中， MetadataKeys提供了某些功能</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的DRM API元素更改 {#drm-api-element-changes-for}

這些表比較1.3版和2.0版之間JavaScript TVSDK的DRM API元素。

本主題中的表：

* DRM工作流初始化
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicense域
* DRMPolicy
* DRManager

### DRM工作流初始化 {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td>應用程式需要調用AdobePSDK.initiateDRMWorkflow以啟動DRM工作流。 沒有此呼叫，DRM視頻將無法播放。<p>介面AdobePSDK<br /> { 0}<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> 布爾隱私模式On);<br /> };</p> </td> 
   <td>初始化在內部完成，不需要顯式調用。</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API | 1.3個API |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| 2.0沒有更改。 | 枚舉DRMAcquireLicenseSettings <br>{ 0}<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthentication方法** |  |
| 2.0沒有更改。 | 枚舉DRMAuthenticationMethod <br>{ 0}<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td>2.0沒有更改。</td> 
   <td><p>介面DRMMetadata<br /> { 0}<br /> 只讀屬性DomString serverUrl;<br /> 只讀屬性DomString licenseId;<br /> 只讀屬性DRMPolicyArray策略； <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面DRMPlaybackTimeWindow {<br /> 只讀屬性int playbackPeriodInSeconds;<br /> 只讀屬性long playbackStartDate;<br /> 只讀屬性long playbackEndDate;<br /> };</p> </td> 
   <td><p>介面DRMPlaybackTimeWindow {<br /> 只讀屬性int periodInSeconds;<br /> 只讀屬性int startDate;<br /> 只讀屬性int endDate;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td>2.0沒有更改。</td> 
   <td><p>介面DRMLicense {<br /> 只讀屬性Uint8Array位元組；<br /> 只讀屬性Date licenseStartDate;<br /> 只讀屬性Date licenseEndDate;<br /> 只讀屬性Date offlineStorageStartDate;<br /> 只讀屬性Date offlineStorageEndDate; <br /> 只讀屬性DomString serverUrl;<br /> 只讀屬性DomString licenseID;<br /> 只讀屬性DomString策略ID;<br /> 只讀屬性DRMPlaybackTimeWindow playbackTimeWindow;<br /> 只讀屬性對象customProperties;<br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense域 {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面DRMLicenseDomain {<br /> 只讀屬性DomString authenticationDomain;<br /> 只讀屬性DRMAuthenticationMethod authenticationMethod; <br /> 只讀屬性DomString serverUrl;<br /> };</p> </td> 
   <td><p>介面DRMLicenseDomain {<br /> 只讀屬性DomString authDomain;<br /> 只讀屬性DRMAuthenticationMethod authMethod; <br /> 只讀屬性DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPolicy {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面DRMPolicy<br /> { 0}<br /> 只讀屬性DomString authenticationDomain;<br /> 只讀屬性DRMAuthenticationMethod authenticationMethod;<br /> <br /> 只讀屬性DomString displayName;<br /> 只讀屬性DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>介面DRMPolicy<br /> { 0}<br /> 只讀屬性DomString authDomain;<br /> 只讀屬性DRMAuthenticationMethod authMethod;<br /> 只讀屬性DomString dispName;<br /> 只讀屬性DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面DRMManager :事件目標{<br /> void acquireLicense(DRMMetadata元資料， <br /> DRMAcquireLicenseSettings設定， <br /> DRMAquireLicenseListener監聽器);<br /> void acquirePreviewLicense(DRMMetadata元資料， <br /> DRMAquireLicenseListener監聽器);<br /> void authenticate(DRMMetadata元資料， <br /> DomString URL,<br /> &amp;DomString AuthenticationDomain, <br /> DomString用戶， <br /> DomString密碼， <br /> DRMAuthenticateListener監聽器);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array陣列、DRMErrorListener偵聽器);<br /> void initialize（DRMOperationCompleteListener偵聽器）;<br /> 屬性long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> 布爾型forceRefresh, <br /> DRMOperationCompleteListener監聽器);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener監聽器);<br /> <br /> void resetDRM（DRMOperationCompleteListener監聽器）;<br /> void returnLicense(DomString serverURL, <br /> DomString許可證ID, <br /> DomString策略ID, <br /> boolean commitImmited,<br /> DRMReturnLicenseListener監聽器);<br /> void setAuthenticationToken(<br /> DRM元資料， <br /> DomString authenticationDomain, <br /> Uint8Array標籤， <br /> DRMOperationCompleteListener監聽器);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener監聽器);<br /> };</p> </td> 
   <td><p>介面DRMManager :事件目標{<br /> void acquireLicense(DRMMetadata元資料， <br /> DRMAcquireLicenseSettings設定， <br /> EventContext eventContext);<br /> void acquirePreviewLicense(DRMMetadata元資料， <br /> EventContext eventContext);<br /> void authenticate(DRMMetadata元資料， <br /> DomString URL,<br /> &amp;DomString AuthenticationDomain, <br /> DomString用戶， <br /> DomString密碼， <br /> EventContext eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array陣列、EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> 屬性long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> 布爾型forceRefresh, <br /> EventContext eventContext);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString許可證ID,<br /> DomString策略ID, <br /> boolean commitImmited,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> DRM元資料， <br /> DomString authenticationDomain, <br /> Uint8Array標籤， <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>類DRMErrorListener : <br /> 公共psdkutils::PSDKInterfaceWithUserData {<br /> 公共：<br /> virtual void onDRMError（uint32_t主要） <br /> uint32_t小調， <br /> const psdkutils:PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl)= 0;<br /> <br /> 受保護：<br /> 虛擬~DRMErrorListener(){}<br /> }</p> </td> 
   <td>事件/介面/說明 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>當在DRMManger的非同步方法之一期間出現錯誤時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類DRMOperationCompleteListener : <br /> 公共DRMErrorListener {<br /> 公共：<br /> virtual void onDRMOperationComplete()= 0;<br /> <br /> 受保護：<br /> 虛擬~DRMOperationCompleteListener(){}<br /> };</p> </td> 
   <td>事件/介面/說明 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>完成DRM初始化時。</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>JoinLicenseDomain()操作成功完成時。</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>LeaveLicenseDomain()操作成功完成。</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>當resetDRM()操作成功完成時。</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>setAuthenticationTokenSet()操作成功完成時。</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>當storeLicenseBytes()操作成功完成時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類DRMAuthenticateListener : <br /> 公共DRMErrorListener {<br /> 公共：<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken)= 0;<br /> <br /> 受保護：<br /> 虛擬~DRMAuthenticateListener(){}<br /> }</p> </td> 
   <td>事件/介面/說明 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>當DRMManager::authenticate方法調用成功時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類DRMAquireLicenseListener: <br /> 公共DRMErrorListener {<br /> 公共：<br /> virtual void onLicenseAcpired(const DRMLicense*)= 0;<br /> <br /> 受保護：<br /> 虛擬~DRMAquireLicenseListener(){}<br /> };</p> </td> 
   <td>事件/介面/說明 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>當DRMManager::acquirePreviewLicense方法調用成功時。</p> </li> 
     <li>kEventDRMLicenseCapived<p>/ DRMLicenseAcquiredEvent</p> <p>當DRMManager::acquireLicense方法調用成功時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類DRMReturnLicenseListener: <br /> 公共DRMErrorListener {<br /> 公共：<br /> virtual void onLicenseReturnComplete(uint32_t numReturned)= 0;<br /> <br /> 受保護：<br /> 虛擬~DRMReturnLicenseListener(){}<br /> };</p> </td> 
   <td>事件/介面/說明 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>當DRMManager::returnLicense方法調用成功時。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0的一般回放API元素更改 {#generic-playback-api-element-changes-for}

這些表比較JavaScript TVSDK 1.3和2.0之間的通用回放API元素。

本主題中的表：

* 媒體資源
* 媒體播放器
* ABRControlParameters
* BufferControlParameters
* 文本格式
* MediaPlayerItemLoader

### 媒體資源 {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面MediaResource {<br /> 屬性DomString url; <br /> 屬性unsigned short type;<br /> 屬性對象元資料；<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>介面MediaResource {<br /> 屬性DomString url;<br /> 屬性DomString類型；<br /> 屬性對象元資料；<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 媒體播放器 {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面MediaPlayer :事件目標<br /> { 0}<br /> void prepareToPlay（雙位）;<br /> void play();<br /> void pause();<br /> void seek（雙位）;<br /> void seekToLocal（雙位）;<br /> void reset();<br /> void release();<br /> void replaceCurrentItem（MediaPlayerItem項）;<br /> void replaceCurrentResource(MediaResource), <br /> MediaPlayerItemConfig配置); <br /> void suspend();<br /> void restore();<br /> void notifyClick();<br /> <br /> 只讀屬性TimeRange playbackRange;<br /> 只讀屬性TimeRange seekableRange;<br /> 只讀屬性雙currentTime;<br /> 只讀屬性double localTime;<br /> 只讀屬性TimeRange bufferedRange;<br /> 只讀屬性DRManager drmManager;<br /> 只讀屬性MediaPlayerItem currentItem;<br /> <br /> //播放器狀態<br /> <br /> <br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PUASED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> <br /> 只讀屬性unsigned short狀態；<br /> <br /> 屬性unsigned short volume;<br /> 屬性ABRControlParameters abrControlParameters;<br /> 屬性BufferControlParameters bufferControlParameters;<br /> <br /> const unsigned short VISIBLE;//對於CC可見性<br /> const無符號短不可見；//對於CC可見性<br /> attribute unsigned short ccVisibility;<br /> 屬性TextFormat樣式；<br /> 只讀屬性PlaybackMetrics playbackMetrics;<br /> <br /> 屬性雙倍率；<br /> 屬性MediaPlayerView視圖；<br /> 只讀屬性時間軸時間軸；<br /> 屬性double currentTimeUpdateInterval; <br /> //設定2.0不支援<br /> };</p> </td> 
   <td><p>介面MediaPlayer :事件目標<br /> { 0}<br /> void prepareToPlay（int位置）;<br /> void play();<br /> void pause();<br /> void seek（int位置）;<br /> void seekToLocalTime（int位置）;<br /> void reset();<br /> void release();<br /> void replaceCurrentItem（MediaResource源）;<br /> <br /> <br /> <br /> <br /> <br /> <br /> 只讀屬性TimeRange playbackRange;<br /> 只讀屬性TimeRange seekableRange;<br /> 只讀屬性雙currentTime;<br /> 只讀屬性double localTime;<br /> 只讀屬性TimeRange bufferedRange;<br /> 只讀屬性DRManager drmManager;<br /> 只讀屬性MediaPlayerItem currentItem;<br /> <br /> //播放器狀態<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PUASED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> 只讀屬性unsigned short狀態；<br /> <br /> 屬性unsigned short volume;<br /> 屬性ABRControlParameters abrControlParameters;<br /> 屬性BufferControlParameters bufferControlParameters;<br /> <br /> 只讀未簽名的SHORT VISIBLE;//對於CC可見性<br /> 只讀未簽名的短不可見；//對於CC可見性<br /> attribute unsigned short ccVisibility;<br /> 屬性TextFormat樣式；<br /> 只讀屬性PlaybackMetrics playbackMetrics;<br /> 屬性MediaPlayerConfig mediaPlayerConfig;<br /> 屬性雙倍率；<br /> 屬性MediaPlayerView視圖；<br /> 只讀屬性時間軸時間軸；<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面MediaPlayerStatus<br /> { 0}<br /> //播放器狀態<br /> const unsigned short PLAYER_STATUS_IDLE;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PUASED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>（2.0的新增內容）</td> 
  </tr> 
 </tbody> 
</table>

#### MediaPlayer支援的事件 {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0事件名稱</th> 
   <th>2.0介面</th> 
   <th> </th> 
   <th>1.3事件名稱</th> 
   <th>1.3介面</th> 
  </tr> 
  <tr> 
   <td><p>（已刪除2.0）</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>制</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td><p>項目已更新</p> <p>更新媒體播放器項目時。</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>更新</p> <p>媒體播放器成功更新媒體時。</p> </td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>Ttmed元資料</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>時間軸已更新</td> 
   <td>事件</td> 
   <td> </td> 
   <td>TtmelineUpdated</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>在2.0中刪除</td> 
   <td> </td> 
   <td> </td> 
   <td>playStart（播放開始）</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>已刪除2.0</td> 
   <td> </td> 
   <td> </td> 
   <td>播放完成</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>狀態已更改</td> 
   <td>狀態事件</td> 
   <td> </td> 
   <td>狀態已更改</td> 
   <td>狀態事件</td> 
  </tr> 
  <tr> 
   <td>大小可用</td> 
   <td>大小事件</td> 
   <td> </td> 
   <td>大小</td> 
   <td>大小事件</td> 
  </tr> 
  <tr> 
   <td>adBreakStarted</td> 
   <td>AdBreak事件</td> 
   <td> </td> 
   <td>adBreakStart</td> 
   <td>AdBreak事件</td> 
  </tr> 
  <tr> 
   <td>已啟動</td> 
   <td>廣告事件</td> 
   <td> </td> 
   <td>adStart</td> 
   <td>廣告事件</td> 
  </tr> 
  <tr> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
   <td> </td> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
  </tr> 
  <tr> 
   <td>已完成</td> 
   <td>廣告事件</td> 
   <td> </td> 
   <td>adComplete</td> 
   <td>廣告事件</td> 
  </tr> 
  <tr> 
   <td>adBreakCompleted</td> 
   <td>AdBreak事件</td> 
   <td> </td> 
   <td>adBreakComplete</td> 
   <td>AdBreak事件</td> 
  </tr> 
  <tr> 
   <td>時間更改</td> 
   <td>時間事件</td> 
   <td> </td> 
   <td>進度</td> 
   <td>進度事件</td> 
  </tr> 
  <tr> 
   <td>緩衝開始</td> 
   <td>事件</td> 
   <td> </td> 
   <td>緩衝</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>緩衝結束</td> 
   <td>事件</td> 
   <td> </td> 
   <td>bufferComplete</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>seekBegin</td> 
   <td>查找事件</td> 
   <td> </td> 
   <td>seekStart</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>查找結束</td> 
   <td>查找事件</td> 
   <td> </td> 
   <td>seekComplete</td> 
   <td>時間事件</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>載入資訊事件</td> 
   <td> </td> 
   <td>載入資訊</td> 
   <td>載入資訊事件</td> 
  </tr> 
  <tr> 
   <td>操作失敗</td> 
   <td>通知事件</td> 
   <td> </td> 
   <td>操作失敗</td> 
   <td>錯誤事件</td> 
  </tr> 
  <tr> 
   <td>drm元資料資訊可用</td> 
   <td>DRMMetadataEvent</td> 
   <td> </td> 
   <td>DRM元資料</td> 
   <td>DRMMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>已達保留</td> 
   <td>保留事件</td> 
   <td> </td> 
   <td>時間軸HolderTearned</td> 
   <td>時間軸保持器事件</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>比特率已更改</td> 
   <td>比特率更改事件</td> 
  </tr> 
  <tr> 
   <td>選定率</td> 
   <td>播放速率事件</td> 
   <td> </td> 
   <td>選定率</td> 
   <td>播放速率事件</td> 
  </tr> 
  <tr> 
   <td>播放率</td> 
   <td>播放速率事件</td> 
   <td> </td> 
   <td>播放率</td> 
   <td>播放速率事件</td> 
  </tr> 
  <tr> 
   <td>adBreakSkpited</td> 
   <td>AdBreak事件</td> 
   <td> </td> 
   <td>adBreakSkpited</td> 
   <td>AdBreak事件</td> 
  </tr> 
  <tr> 
   <td>已按一下ad<br /> 當用戶按一下廣告時。</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>2.0中新增</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>配置檔案已更改<br /> 播放配置檔案更改時。</td> 
   <td>配置檔案事件</td> 
   <td> </td> 
   <td><p>2.0中新增</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdjusted<br /> 查找位置因內部或外部規則而調整時。</td> 
   <td>查找事件</td> 
   <td> </td> 
   <td><p>2.0中新增</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>音頻已更新<br /> 更新媒體播放器項目時。 對於包含僅在播放時可檢測的音頻軌道的某些流，當有新的音頻軌道可用時，將觸發此事件。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中新增</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>字幕已更新 <br /> 更新媒體播放器項目時。 對於即時/線性流，客戶端必須定期刷新媒體資源以檢測新的可用內容。 當這種情況發生時，某些介質特性可能會發生變化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中新增</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>主更新 <br /> 更新媒體播放器項目時。 對於即時/線性流，客戶端必須定期刷新媒體資源以檢測新的可用內容。 當這種情況發生時，某些介質特性可能會發生變化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中新增</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> 更新媒體播放器項目時。 對於即時/線性流，客戶端必須定期刷新媒體資源以檢測新的可用內容。 當這種情況發生時，某些介質特性可能會發生變化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中新增</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> 生成定時事件時發送。</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>2.0中新增</p> </td> 
  </tr> 
 </tbody> 
</table>

### ABRControlParameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面ABRControlParameters<br /> { 0}<br /> const unsigned short ABR_POLICY_CONSERVACY = 0;<br /> const unsigned short ABR_POLICY_MEODE = 1;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2;<br /> <br /> attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> 屬性unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>介面ABRControlParameters<br /> { 0}<br /> const unsigned short ABR_POLICY_CONSERVACY = 0;<br /> const unsigned short ABR_POLICY_MEODE = 1;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2;<br /> <br /> attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> 屬性unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### BufferControlParameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面BufferControlParameters<br /> { 0}<br /> 屬性double initialBufferTime;<br /> 屬性double playBufferTime;<br /> 控制雙DEFAULT_INITIAL_BUFFER_TIME;<br /> 控制雙DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>介面BufferControlParameters<br /> { 0}<br /> 屬性double initialBufferTime;<br /> 屬性double playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 文本格式 {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td>2.0無更改</td> 
   <td><p>介面文本格式<br /> { 0}<br /> //顏色<br /> const unsigned short COLOR_DEFAULT = 0;<br /> const unsigned short COLOR_BLACK = 1;<br /> const unsigned short COLOR_GRAY = 2;<br /> const unsigned short COLOR_WHITE = 3;<br /> const unsigned short COLOR_BRIGHT_WHITE = 4;<br /> const unsigned short COLOR_DARK_RED = 5;<br /> const unsigned short COLOR_RED = 6;<br /> const unsigned short COLOR_BRIGHT_RED = 7;<br /> const unsigned short COLOR_DARK_GREEN = 8;<br /> const unsigned short COLOR_GREEN = 9;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10;<br /> const unsigned short COLOR_DARK_BLUE = 11;<br /> const unsigned short COLOR_BLUE = 12;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13;<br /> const unsigned short COLOR_DARK_YELLOW = 14;<br /> const unsigned short COLOR_YELLOW = 15;<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16;<br /> const unsigned short COLOR_DARK_MAGENTA = 17;<br /> const unsigned short COLOR_MAGENTA = 18;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19;<br /> const unsigned short COLOR_DARK_CYAN = 20;<br /> const unsigned short COLOR_CYAN = 21;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22;<br /> <br /> 只讀屬性unsigned short fontColor;<br /> 只讀屬性unsigned short backgroundColor;<br /> 只讀屬性unsigned short fillColor;<br /> 只讀屬性unsigned short edgeColor;<br /> <br /> //大小<br /> const unsigned short SIZE_DEFAULT = 0;<br /> const unsigned short SIZE_SMALL = 1;<br /> const unsigned short SIZE_MEDIUM = 2;<br /> const unsigned short SIZE_LARGE = 3;<br /> <br /> 只讀屬性unsigned short size;<br /> <br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0;<br /> const unsigned short FONT_EDGE_NONE = 1;<br /> const unsigned short FONT_EDGE_ROURGED = 2;<br /> const unsigned short FONT_EDGE_DESCREPT = 3;<br /> const unsigned short FONT_EDGE_UNIFORM = 4;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6;<br /> 只讀屬性unsigned short fontEdge;<br /> <br /> //字型<br /> const unsigned short FONT_DEFAULT = 0;<br /> const無符號短FONT_MONOSECD_WITH_SERIFS = 1;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2;<br /> const無符號短FONT_MONSECD_WITHOUT_SERIFS = 3;<br /> const unsigned short FONT_CAUSAL = 4;<br /> const unsigned short FONT_CURSIVE = 5;<br /> const unsigned short FONT_SMALL_CAPPARTS = 6;<br /> 只讀屬性unsigned short font;<br /> 只讀屬性unsigned short fontOpacity;<br /> 只讀屬性unsigned short backgroundOpaced;<br /> 只讀屬性unsigned short fillOpaces;<br /> 只讀屬性unsigned short DEFAULT_OPACYTE;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面MediaPlayerItemLoader:<br /> { 0}<br /> void load(MediaResource資源，long resourceId,<br /> ItemLoaderListener監聽器， <br /> MediaPlayerItemConfig配置);<br /> void cancel();<br /> 只讀屬性MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>介面ItemLoaderListener<br /> { 0}<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的媒體特性API元素更改 {#media-characteristics-api-element-changes-for}

這些表比較C++ TVSDK的媒體特性API元素，這些元素位於版本1.3和2.0之間。

本主題中的表：

* 媒體播放器項
* 曲目、AudioTrack、ClosedCaptionsTrack
* 配置檔案
* DRMMetadataInfo

### 媒體播放器項 {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面MediaPlayerItem {<br /> 只讀屬性MediaResource資源；<br /> 只讀屬性long resourceId;<br /> 只讀屬性布爾live<br /> <br /> 只讀屬性booleanhasAlternateAudio;<br /> 只讀屬性AudioTrackList audioTracks;<br /> 只讀屬性AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack); <br /> <br /> 只讀屬性boolean有ClosedCaptions;<br /> 只讀屬性ClosedCaptionsTrackList closedCaptionsTracks;<br /> 只讀屬性ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTrack軌道); <br /> <br /> readonly屬性booleanhasTimedMetadata;<br /> 只讀屬性TimedMetadataList timedMetadata;<br /> 只讀屬性布爾動態；<br /> <br /> 只讀屬性boolean isProtected;<br /> 只讀屬性DRMMetadataInfoList drmMetadataInfos;<br /> 只讀屬性ProfileList配置檔案；<br /> 只讀屬性Profile selectedProfile;<br /> <br /> 只讀屬性布爾tricPlaySupported;<br /> 只讀屬性FloatArray availablePlaybackRates;<br /> 只讀屬性float selectedPlaybackRate;<br /> <br /> <br /> 只讀屬性MediaPlayer mediaPlayer;<br /> 只讀屬性MediaPlayerItemConfig;<br /> };</p> </td> 
   <td><p>介面MediaPlayerItem {<br /> 只讀屬性MediaResource資源；<br /> 只讀屬性long resourceId;<br /> 只讀屬性布爾live<br /> <br /> 只讀屬性booleanhasAlternateAudio;<br /> 只讀屬性AudioTrackList audioTracks;<br /> 屬性AudioTrack selectedAudioTrack;<br /> <br /> <br /> 只讀屬性boolean有ClosedCaptions;<br /> 只讀屬性ClosedCaptionsTrackListCtracks;<br /> 屬性ClosedCaptionsTrack selectCCTrack;<br /> <br /> <br /> <br /> readonly屬性booleanhasTimedMetadata;<br /> 只讀屬性TimedMetadataList timedMetadata;<br /> 只讀屬性布爾動態；<br /> <br /> 只讀屬性boolean isProtected;<br /> 只讀屬性DRMMetadataInfoList drmMetadataInfos;<br /> 只讀屬性ProfileList配置檔案；<br /> <br /> <br /> 只讀屬性布爾tricPlaySupported;<br /> 只讀屬性Int32Array availablePlaybackRates;<br /> <br /> 只讀屬性StringList adTags;<br /> <br /> 只讀屬性MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 曲目/音頻曲目/ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面跟蹤<br /> { 0}<br /> 只讀屬性DomString名稱；<br /> 只讀屬性DomString語言；<br /> 只讀屬性布爾型預設值<br /> 只讀屬性布爾自動選擇；<br /> }; </p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>介面AudioTrack :跟蹤<br /> { 0}<br /> 只讀屬性DomString名稱；//FromTrack<br /> 只讀屬性DomString語言；//FromTrack<br /> 只讀屬性布爾型預設值//從跟蹤<br /> 只讀屬性布爾自動選擇；//FromTrack<br /> <br /> 只讀屬性unsigned int pid;<br /> };</p> </td> 
   <td><p>介面AudioTrack<br /> { 0}<br /> 只讀屬性DomString名稱；<br /> 只讀屬性DomString語言； <br /> 只讀屬性布爾型預設值<br /> 只讀屬性布爾自動選擇；<br /> 只讀屬性布爾型強制；<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0無更改</td> 
   <td><p>介面AudioTrackList<br /> { 0}<br /> 只讀屬性unsigned long length;<br /> GetterAudioTrack（無符號長索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面ClosedCaptionsTrack :跟蹤<br /> { 0}<br /> 只讀屬性DomString名稱；//FromTrack<br /> 只讀屬性DomString語言；//FromTrack<br /> 只讀屬性布爾型預設值// FromTrack<br /> 只讀屬性布爾自動選擇；//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> 只讀屬性unsigned short serviceType;<br /> 只讀屬性布爾型強制；<br /> };</p> </td> 
   <td><p>介面ClosedCaptionsTrack<br /> { 0}<br /> 只讀屬性DomString名稱；<br /> 只讀屬性DomString語言；<br /> 只讀屬性布爾型預設值<br /> <br /> <br /> 只讀屬性布爾活動；<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0無更改</td> 
   <td><p>介面ClosedCaptionsTrackList<br /> { 0}<br /> 只讀屬性unsigned long length;<br /> GetterClosedCaptionsTrack（無符號長索引）;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 配置檔案 {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td>配置檔案：2.0無更改</td> 
   <td><p>介面配置檔案<br /> { 0}<br /> 只讀屬性unsigned int width;<br /> 只讀屬性unsigned int height;<br /> 只讀屬性unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>配置檔案清單：2.0無更改</td> 
   <td><p>介面配置檔案清單<br /> { 0}<br /> 只讀屬性unsigned long length;<br /> getter配置檔案（無符號長索引）;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>:2.0無更改</td> 
   <td><p>介面DRMMetadataInfo<br /> { 0} <br /> 只讀屬性DRMetadata元資料；<br /> 只讀屬性long prefetchTimestamp;<br /> 只讀屬性TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>:2.0無更改</td> 
   <td><p>介面DRMMetadataInfoList<br /> { 0}<br /> 只讀屬性unsigned long length;<br /> GETTERetadataInfo(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 將C++錯誤映射到不同語言的異常 {#mapping-c-errors-to-exceptions-in-different-languages}

可以將C++錯誤代碼映射到不同語言的異常。

C++ PSDK的API有「無拋送」策略。 大多數API方法都返回PSDKErrorCode值，以指示是否成功執行了該方法。 非同步錯誤通過錯誤事件通知。

ActionScript和JAVA PSDK有不同的策略。 大多數錯誤都會引發ArgumentError或IllegalStateException，以指示無法執行方法的同步部分。 不會捕獲這些異常，應用程式碼負責處理異常。 它們通常提供方法調用失敗原因的有用資訊。 例如，如果以無效狀態調用prepareToPlay命令，則會引發以下異常：

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

ActionScript/JAVA還會從建構子中引發異常，以指示某些內部對象建立不正確。 這些例外是在內部處理的，不會傳播到應用程式。 例外將包含在發送到應用程式的警告通知中

例如，如果找不到接收的廣告響應的有效媒體檔案，則無法建立有效的廣告資產對象或廣告。 因此，時間線上不會放置任何廣告，並會調度NotificationEvent.OperationFailed通知。

從Adobe視頻引擎(AVE)非同步接收的錯誤或警告代碼作為正常事件分派給應用程式。 通知事件包含所有接收的錯誤代碼和任何附加元資料，如URL、資源標識符、句柄等。 如果錯誤嚴重且當前媒體的播放無法繼續，則MediaPlayer將轉換為ERROR狀態，並調度onStatusChanged回調或MediaPlayerStatusChanged.STATUS_CHANGED事件。 如果播放可以繼續，則會調度正常通知事件。

<table> 
 <tbody> 
  <tr> 
   <th>C++錯誤（PSDKError代碼）</th> 
   <th> </th> 
   <th>爪哇</th> 
   <th>ActionScript</th> 
   <th>JavaScript</th> 
  </tr> 
  <tr> 
   <td>kECInvalidArgument</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>參數錯誤</td> 
   <td>代碼為1的異常，說明= "INVALID_ARGUMENT"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>參數錯誤</td> 
   <td>代碼為2的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>代碼為3的異常，說明= "ILLEGAL_STATE"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>未找到ECInterface</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為4的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreation失敗</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為5的異常，說明= "CREATION_FAILED"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為5的異常，說明= "CREATION_FAILED"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為7的異常，說明= "DATA_NOT_AVAILABLE"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeek錯誤</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為8的異常，說明= "SEEK_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupported功能</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為9的異常，說明為"UNSUPPORTED_FEATURE"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為10的異常，說明= "RANGE_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為11，說明為"CODEC_NOT_SUPPORTED"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMedia錯誤</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為12的異常，說明= "MEDIA_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為13的異常，說明= "NETWORK_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGeneric錯誤</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error或MediaPlayerNotification.Warning</td> 
   <td>MediaError或NotificationEvent</td> 
   <td>代碼為14的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為15的異常，說明= "INVALID_SEEK_TIME"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為16的異常，說明= "AUDIO_TRACK_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>線程錯誤</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為17的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>未找到kECElement</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為18的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNot已實施</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為19的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為200的異常，說明= "PLAYBACK_OPERATION_FAILED"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>通知事件</td> 
   <td>代碼為201的異常，說明= "NATIVE_WARNING"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAdResolver失敗</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>代碼為202的異常，說明= "AD_RESOLVER_FAILED"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的實用程式和Helper API元素更改 {#utility-and-helper-api-element-changes-for}

這些表比較JavaScript TVSDK的Utility和Helper API元素在版本1.3和2.0之間。

本主題中的表：

* 版本
* 時間範圍
* QOSProvider
* 設備資訊
* 載入資訊
* 視圖
* 播放資訊

### 版本 {#version}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面版本<br /> { 0}<br /> 只讀屬性DomString版本；<br /> 只讀屬性DomString描述；<br /> 只讀屬性long major;<br /> 只讀屬性long minor;<br /> 只讀屬性長修訂版；<br /> 只讀屬性long apiVersion;<br /> };</p> </td> 
   <td><p>介面版本<br /> { 0}<br /> 只讀屬性DomString版本；<br /> 只讀屬性DomString描述；<br /> 只讀屬性DomString主；<br /> 只讀屬性DomString次要；<br /> 只讀屬性DomString修訂版；<br /> 只讀屬性DomString apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 時間範圍 {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td>2.0無更改</td> 
   <td><p>介面時間範圍<br /> { 0}<br /> 只讀屬性unsigned long begin;<br /> 只讀屬性unsigned long end;<br /> 只讀屬性unsigned long duration;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td>2.0無更改</td> 
   <td><p>介面QOSProvider<br /> { 0}<br /> void attachMediaPlayer(MediaPlayer);<br /> void detachMediaPlayer();<br /> <br /> 只讀屬性DeviceInformation deviceInformation;<br /> 只讀屬性PlaybackInformation playbackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 設備資訊 {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面設備資訊<br /> { 0}<br /> 只讀屬性DomString os;<br /> <br /> <br /> <br /> 只讀屬性DomString id;<br /> 只讀屬性int densityDPI;<br /> 只讀屬性int heightPixels;<br /> 只讀屬性int widthPixels;<br /> 只讀屬性布爾seekToKeyFrame;<br /> };</p> </td> 
   <td><p>介面設備資訊<br /> { 0}<br /> 只讀屬性DomString os;<br /> 只讀屬性int sdk;<br /> 只讀屬性DomString模型；<br /> 只讀屬性DomString製造商；<br /> 只讀屬性DomString id;<br /> 只讀屬性int densityDPI;<br /> 只讀屬性int heightPixels;<br /> 只讀屬性int widthPixels;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 載入資訊 {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td>2.0無更改</td> 
   <td><p>介面LoadInfo<br /> { 0}<br /> 只讀屬性DomString url;<br /> 只讀屬性整型；<br /> 只讀屬性雙下載持續時間；<br /> 只讀屬性int periodIndex;<br /> 只讀屬性雙媒體持續時間；<br /> 只讀屬性short TRACK_TYPE_FRAGMENT;<br /> 只讀屬性short TRACK_TYPE_TRACK;<br /> 只讀屬性short TRACK_TYPE_MANIFEST;<br /> 只讀屬性短類型；<br /> 只讀屬性DomString trackName;<br /> 只讀屬性DomString trackType;<br /> 只讀屬性int trackIndex;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 視圖 {#view}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td>2.0無更改</td> 
   <td><p>介面視圖<br /> { 0}<br /> 只讀屬性unsigned short x;<br /> 只讀屬性unsigned short y<br /> 只讀屬性unsigned short width;<br /> 只讀屬性unsigned short height;<br /> <br /> void setSize（無符號短寬，無符號短高）;<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### 播放資訊 {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3個API</th> 
  </tr> 
  <tr> 
   <td><p>介面回放資訊<br /> { 0}<br /> 只讀屬性雙timeToFirstByte;<br /> 只讀屬性double timeToLoad;<br /> 只讀屬性double timeToStart;<br /> 只讀屬性double timeToFail;<br /> 只讀屬性int totalSecondsPlayed;<br /> 只讀屬性int totalSecondsBusded;<br /> 只讀屬性雙frameRate;<br /> 只讀屬性int droppedFrameCount;<br /> 只讀屬性int evencedBandwidth;<br /> 只讀屬性int位速率；<br /> 只讀屬性雙bufferTime;<br /> 只讀屬性int bufferLength;<br /> 只讀屬性int emptyBufferCount;<br /> 只讀屬性雙緩衝時間；<br /> };</p> </td> 
   <td><p>介面回放資訊<br /> { 0}<br /> 只讀屬性雙timeToFirstByte;<br /> 只讀屬性double timeToLoad;<br /> 只讀屬性double timeToStart;<br /> 只讀屬性double timeToFail;<br /> 只讀屬性int totalSecondsPlayed;<br /> 只讀屬性int totalSecondsBusded;<br /> 只讀屬性雙frameRate;<br /> 只讀屬性int droppedFrameCount;<br /> <br /> 只讀屬性int位速率；<br /> 只讀屬性雙bufferTime;<br /> 只讀屬性int bufferLength;<br /> 只讀屬性int emptyBufferCount;<br /> 只讀屬性雙緩衝時間；<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 有用的資源 {#helpful-resources}

* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://helpx.adobe.com/support/primetime.html) 的子菜單。
