---
title: TVSDK轉換 — JavaScript適用的1.3至2.0
description: 許多方法簽章和API元素名稱已針對2.0變更。檢閱這些表格以檢視所有API變更詳細資訊。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---

# TVSDK轉換 — JavaScript適用的1.3至2.0 {#tvsdk-conversion-to-for-javascript}

許多方法簽章和API元素名稱已針對2.0變更。檢閱這些表格以檢視所有API變更詳細資訊。

## 在JavaScript中實作回呼函式 {#implement-callback-functions-in-javascript}

方法檔案中的註解會建議您需要實作的回呼簽名。

JavaScript的API語法是根據Web ID。 若是TVSDK介面，則會呼叫方法名稱 *方法名稱*()。 對於要由應用程式實作的方法，會有一個名為的讀取/寫入屬性， *方法名稱* CallbackFunc已新增至介面，您的應用程式應將其設定為指向實作方法的函式。 例如：

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

## 2.0的Advertising工作流程API元素變更 {#advertising-workflow-api-element-changes-for}

下表比較1.3版和2.0版之間JavaScript TVSDK的廣告工作流程API元素。

此主題中的表格：

* TimedMetadata
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* 刊登
* 商機
* 預訂
* 時間軸/時間軸專案/時間軸標籤
* 廣告插播
* Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* 時間表操作
* AdBreakPlacement
* Auditudesettings

### TimedMetadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMetadata</strong>：介面TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ； <br /> const unsigned short METADATA_TYPE_ID3 = 1 ； <br /> readonly attribute unsigned short type； <br /> readonly attribute long time；<br /> 唯讀屬性DomString ID；<br /> 唯讀屬性DomString名稱；<br /> 唯讀屬性DomString內容； <br /> 唯讀屬性物件中繼資料；<br /> }； </p> </td> 
   <td><p>介面TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ；<br /> const unsigned short METADATA_TYPE_ID3 = 1 ；<br /> 唯讀屬性（不帶正負號的短metadataType）；<br /> readonly attribute long time；<br /> 唯讀屬性長ID；<br /> 唯讀屬性DomString名稱；<br /> <br /> 唯讀屬性物件中繼資料；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>：（2.0版無變更）</td> 
   <td><p>介面TimedMetadataList {<br /> readonly attribute unsigned long length；<br /> getter TimedMetadata (unsigned long index)；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdSignalingMode {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AdSigningMode { <br /> const unsigned short MODE_DEFAULT， <br /> const unsigned short MODE_MANIFEST_CUE ， <br /> const unsigned short MODE_SERVER_MAP ， <br /> const unsigned short MODE_CUSTOM_RANGES <br /> }；</p> </td> 
   <td>這會取代MetadataKeys：：MANIFEST_CUE索引鍵。</td> 
  </tr> 
 </tbody> 
</table>

### AdvertisingMetadata {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AdvertisingMetadata { <br /> 屬性AdSignalingMode模式； <br /> 屬性AdBreakWatchedPolicy adBreakAsWatched； <br /> 屬性布林值livePreroll； <br /> 屬性布林值delayAdLoading ； <br /> }；</p> </td> 
   <td>此功能由提供<p>中繼資料索引鍵：：ADVERTISING_METADATA</p> 機碼。</td> 
  </tr> 
 </tbody> 
</table>

### CustomRangeMetadata {#customrangemetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE； <br /> const unsigned short TYPE_DELETE_RANGE； <br /> const unsigned short TYPE_REPLACE_RANGE； <br /> 屬性不帶正負號的短型別； <br /> 屬性布林值adjustSeekPosition； <br /> 屬性TimeRangeList timeRangeList； <br /> }；</p> </td> 
   <td>（2.0的新功能）</td> 
  </tr> 
 </tbody> 
</table>

### ReplaceTimeRange {#replacetimerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面ReplaceTimeRange { <br /> 屬性無符號long begin； <br /> readonly attribute unsigned long end； <br /> 屬性無簽署的完整期間； <br /> 屬性unsigned long replaceDuration； <br /> }；</p> </td> 
   <td>（2.0的新功能）</td> 
  </tr> 
 </tbody> 
</table>

### 刊登 {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面位置{ <br /> const unsigned short TYPE_MID_ROLL； <br /> const unsigned short TYPE_PRE_ROLL； <br /> const unsigned short TYPE_POST_ROLL； <br /> const unsigned short TYPE_SERVER_MAP； <br /> const unsigned short TYPE_CUSTOM_RANGE；<br /> readonly attribute unsigned short type； <br /> readonly attribute long time； <br /> 唯讀屬性長持續時間； <br /> const unsigned short MODE_DEFAULT； <br /> const unsigned short MODE_INSERT； <br /> const unsigned short MODE_REPLACE； <br /> const unsigned short MODE_DELETE； <br /> const unsigned short MODE_MARK； <br /> const unsigned short MODE_FREE_REPLACE； <br /> readonly attribute unsigned short mode； <br /> 唯讀屬性TimeRange； <br /> }；</p> </td> 
   <td>（2.0的新功能）</td> 
  </tr> 
 </tbody> 
</table>

### 商機 {#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面商機{ <br /> 唯讀屬性DomString ID； <br /> 唯讀屬性放置位置； <br /> 唯讀屬性Object設定； <br /> 唯讀屬性Object customParameters； <br /> }； </p> </td> 
   <td>（2.0的新功能）</td> 
  </tr> 
 </tbody> 
</table>

### 預訂 {#reservation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面預訂{ <br /> 唯讀屬性TimeRange； <br /> 唯讀屬性長保留； <br /> }； </p> </td> 
   <td> （2.0的新功能）</td> 
  </tr> 
 </tbody> 
</table>

### 時間軸/時間軸專案/時間軸標籤 {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p><strong>時間表</strong>：介面時間軸 <br /> { readonly attribute TimelineMarkerList timelineMargers； <br /> 唯讀屬性TimelineItemList timelineItems； <br /> double convertToLocalTime( double time)； <br /> double convertToVirtualTime( double time)； <br /> }；</p> </td> 
   <td><p>介面時間軸{<br /> 唯讀屬性TimelineMarkerList timelineMargers；<br /> <br /> <br /> <br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>時間軸專案</strong>：介面時間軸專案：<br /> 時間軸標籤{<br /> 唯讀屬性長ID； <br /> 唯讀屬性TimeRange virtualRange； <br /> 唯讀屬性TimeRange localRange； <br /> 唯讀屬性布林值watched； <br /> 唯讀屬性布林值暫時； <br /> }； </p> </td> 
   <td>（2.0的新功能）</td> 
  </tr> 
  <tr> 
   <td><strong>時間軸標籤</strong>：（2.0版無變更）</td> 
   <td><p>介面時間軸標籤{<br /> 唯讀屬性雙倍時間；<br /> 唯讀屬性雙倍持續時間；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### 廣告插播 {#adbreak}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面廣告插播{<br /> <br /> <br /> <br /> 唯讀屬性雙倍持續時間；<br /> 唯讀屬性AdList廣告；<br /> <br /> <br /> 唯讀屬性AdInsertionType insertionType；<br /> }； </p> </td> 
   <td><p>介面廣告插播{<br /> 唯讀屬性雙倍時間；<br /> 唯讀屬性double replaceDuration；<br /> <br /> 唯讀屬性雙倍持續時間；<br /> 唯讀屬性AdList adList；<br /> <br /> 唯讀屬性DomString資料；<br /> <br /> }； </p> </td> 
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
   <td><p> <strong>廣告</strong>：介面廣告{<br /> 唯讀屬性AdAsset primaryAsset；<br /> 唯讀屬性AdAssetList companionAssets；<br /> <br /> 唯讀屬性雙倍持續時間；<br /> 唯讀屬性DomString ID；<br /> const不帶正負號的短ADTYPE_LINEAR = 0 ；<br /> const不帶正負號的短ADTYPE_NONLINEAR = 1 ；<br /> <br /> 唯讀屬性（不帶正負號的短adType）；<br /> 唯讀屬性AdInsertionType adInsertionType； <br /> <br /> 唯讀屬性布林值可點選； <br /> 唯讀屬性布林值isCustomAdMarker；<br /> }； </p> </td> 
   <td><p>介面廣告{<br /> 唯讀屬性AdAsset primaryAsset；<br /> 唯讀屬性AdAssetList companionAssets；<br /> <br /> 唯讀屬性雙倍持續時間；<br /> 唯讀屬性DomString ID；<br /> const不帶正負號的短ADTYPE_LINEAR = 0 ；<br /> const不帶正負號的短ADTYPE_NONLINEAR = 1 ；<br /> <br /> readonly attribute unsigned short type；<br /> 唯讀屬性AdInsertionType insertionType； <br /> 唯讀屬性物件追蹤器；<br /> <br /> <br /> }； </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>：（2.0版無變更）</td> 
   <td><p>介面AdAsset {<br /> 唯讀屬性DomString ID；<br /> 唯讀屬性雙倍持續時間；<br /> 唯讀屬性MediaResource；<br /> 唯讀屬性AdClick adClick；<br /> 唯讀屬性物件中繼資料；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>：（2.0版無變更）</td> 
   <td><p>介面AdClick {<br /> 唯讀屬性DomString ID；<br /> 唯讀屬性DomString title；<br /> 唯讀屬性DomString url；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>：（2.0版無變更）</td> 
   <td><p>介面廣告清單{<br /> readonly attribute unsigned long length；<br /> getter Ad (unsigned long index)；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>：（2.0版無變更）</td> 
   <td><p>介面AdAssetList {<br /> readonly attribute unsigned long length；<br /> getter AdAsset (unsigned long index)；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>：介面AdBannerAsset ： AdAsset<br /> {<br /> 唯讀屬性int寬度；<br /> 唯讀屬性int高度；<br /> 唯讀屬性DomString staticUrl；<br /> 唯讀屬性DomString高度；<br /> 唯讀屬性DomString寬度；<br /> }；</p> </td> 
   <td> 2.0的新增功能</td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>：介面AdBreakTimelineItem ：TimelineItem { <br /> 唯讀屬性AdBreak adBreak； <br /> 唯讀屬性AdTimelineItemList專案； <br /> }； </p> </td> 
   <td> （2.0的新功能）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>：介面AdTimelineItem ： TimelineItem { <br /> 唯讀屬性AdBreak adBreak； <br /> 唯讀屬性廣告廣告； <br /> }； </p> </td> 
   <td> （2.0的新功能）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>：介面AdBreakTimelineItemList { <br /> readonly attribute unsigned long length； <br /> getter AdBreakTimelineItem （未簽署的記錄檔索引）； <br /> }；</p> </td> 
   <td> （2.0的新功能）</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AdBreakPolicy {<br /> 唯讀屬性短AD_BREAK_POLICY_SKIP；<br /> 唯讀屬性短AD_BREAK_POLICY_PLAY；<br /> 唯讀屬性短AD_BREAK_POLICY_REMOVE；<br /> 唯讀屬性短AD_BREAK_POLICY_REMOVE_AFTER_PLAY；<br /> }；</p> </td> 
   <td><p> 介面AdPolicyConstants {<br /> 唯讀屬性短AD_BREAK_POLICY_SKIP；<br /> 唯讀屬性短AD_BREAK_POLICY_PLAY；<br /> 唯讀屬性短AD_BREAK_POLICY_REMOVE；<br /> 唯讀屬性短AD_BREAK_POLICY_REMOVE_AFTER_PLAY；}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> 介面AdBreakWatchedPolicy {<br /> 唯讀屬性短AD_BREAK_AS_WATCHED_ON_BEGIN；<br /> 唯讀屬性短AD_BREAK_AS_WATCHED_ON_END；<br /> 唯讀屬性短AD_BREAK_AS_WATCHED_NEVER；<br /> }； </p> </td> 
   <td><p> ...<br /> 唯讀屬性短AD_BREAK_AS_WATCHED_ON_BEGIN；<br /> 唯讀屬性短AD_BREAK_AS_WATCHED_ON_END；<br /> 唯讀屬性短AD_BREAK_AS_WATCHED_NEVER；<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面AdPolicy {<br /> 唯讀屬性短AD_POLICY_PLAY；<br /> 唯讀屬性短AD_POLICY_PLAY_FROM_AD_BEGIN；<br /> 唯讀屬性短AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN；唯讀屬性短AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK；<br /> <br /> 唯讀屬性短AD_POLICY_SKIP_AD_BREAK；<br /> }；</p> </td> 
   <td><p> ... <br /> 唯讀屬性短AD_POLICY_PLAY；<br /> 唯讀屬性短AD_POLICY_PLAY_FROM_AD_BEGIN；<br /> 唯讀屬性短AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN；<br /> 唯讀屬性短AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK；<br /> 唯讀屬性短AD_POLICY_SKIP_AD_BREAK；<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面AdPolicyMode {<br /> 唯讀屬性短AD_POLICY_MODE_PLAY；<br /> 唯讀屬性短AD_POLICY_MODE_SEEK；<br /> 唯讀屬性短AD_POLICY_MODE_TRICKPLAY；<br /> }；</p> </td> 
   <td><p> ...<br /> {readonly屬性短AD_POLICY_MODE_PLAY；<br /> 唯讀屬性短AD_POLICY_MODE_SEEK；<br /> 唯讀屬性短AD_POLICY_MODE_TRICKPLAY；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面AdPolicyInfo {<br /> 唯讀屬性AdBreakTimelineItemList <br /> adBreakTimelineItems；<br /> 唯讀屬性AdTimelineItem adTimelineItem；<br /> 唯讀屬性double currentTime；<br /> 唯讀屬性double seekToTime；<br /> 唯讀屬性雙倍速率；<br /> 唯讀屬性短模式； //AdPolicyMode<br /> }；</p> </td> 
   <td><p>介面AdPolicyInfo {<br /> 唯讀屬性AdBreakPlacementList <br /> adBreakPlacement；<br /> 唯讀屬性廣告廣告；<br /> 唯讀屬性double currentTime；<br /> 唯讀屬性double seekToTime；<br /> 唯讀屬性雙倍速率；<br /> 唯讀屬性短模式； //AdPolicyMode<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 屬性物件selectPolicyForAdBreakCallbackFunc；<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 屬性物件selectAdBreaksToPlayCallbackFunc；<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo)；<br /> */<br /> 屬性物件selectPolicyForSeekIntoAdCallbackFunc； <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 屬性物件selectWatchedPolicyForAdBreakCallbackFunc；<br /> }；</p> </td> 
   <td><p>介面AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 屬性物件selectPolicyForAdBreakFuncCallback；<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 屬性物件selectAdBreaksToPlayCallback；<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo)；<br /> */<br /> 屬性物件selectPolicyForSeekIntoAdCallback； <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 屬性物件selectWatchedPolicyForAdBreakCallback；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### 時間表操作 {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面時間軸操作{ <br /> 唯讀屬性放置位置； <br /> }；</p> </td> 
   <td> （2.0的新功能）</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPlacement {#adbreakplacement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AdBreakPlacement ：時間軸操作{<br /> 唯讀屬性AdBreak adBreak；<br /> 唯讀屬性Placement placement； //從TimelineOperation<br /> 唯讀屬性雙倍時間；<br /> 唯讀屬性雙倍持續時間；<br /> }；</p> </td> 
   <td><p>介面AdBreakPlacement {<br /> 唯讀屬性AdBreak adBreak；<br /> 唯讀屬性放置位置；<br /> 唯讀屬性雙倍時間；<br /> 唯讀屬性雙倍持續時間；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### Auditudesettings {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AuditudeSettings ： AdvertisingMetadata { <br /> 屬性DomString zoneId； <br /> 屬性DomString mediaId； <br /> 屬性DomString defaultMediaId ； <br /> 屬性DomString網域； <br /> 屬性Object targetingInfo ； <br /> 屬性Object customParameters ； <br /> 屬性Boolean creativePackingEnabled ；<br /> 屬性布林值showStaticBanners ；<br /> }；</p> </td> 
   <td>功能由MetadataKeys：：AUDITUDE_METADATA_KEY鍵提供。</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的自訂API元素變更 {#customization-api-element-changes-for}

下表比較1.3和2.0版之間JavaScript TVSDK的自訂API元素。

此主題中的表格：

* MediaPlayerItemConfig
* contentfactory
* 網路組態

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面MediaPlayerItemConfig {<br /> 屬性ContentFactory adFactory；<br /> 屬性StringList subscribeTags；<br /> <br /> 屬性StringList adTags；<br /> <br /> <br /> 屬性AdSignalingMode adSignalingMode；<br /> 屬性CustomRangeMetadata customRangeMetadata；<br /> 屬性NetworkConfiguration networkConfiguration；<br /> 屬性AdvertisingMetadata advertisingMetadata；<br /> 屬性布林值useHardwareDecoder；<br /> }；</p> </td> 
   <td><p>介面MediaPlayerConfig {<br /> <br /> <br /> <br /> 屬性StringList adTags；<br /> 屬性StringList subscribedTags；<br /> 屬性MediaPlayerClientFactory clientFactory；<br /> <br /> <br /> <br /> <br /> <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### contentfactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem)；<br /> */<br /> 屬性Object retrieveAdPolicySelectorCallbackFunc；<br /> }；</p> </td> 
   <td><p>介面MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem)；<br /> */<br /> 屬性Object retrieveAdPolicySelectorFunc；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### 網路組態 {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面網路組態<br /> {<br /> 屬性布林值forceNativeNetworking；<br /> 屬性布林值useRedirectedUrl；<br /> 屬性Object cookieHeader；<br /> 屬性布林值readSetCookieHeader；<br /> 屬性int masterUpdateInterval； <br /> 屬性布林值useCookieHeaderForAllRequests；<br /> 屬性int readLimit；<br /> }；</p> </td> 
   <td>在1.3中，部分此功能由MetadataKeys提供</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的DRM API元素變更 {#drm-api-element-changes-for}

這些表格會比較1.3和2.0版之間JavaScript TVSDK的DRM API元素。

此主題中的表格：

* DRM工作流程初始化
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindows
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRManager

### DRM工作流程初始化 {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>應用程式需要呼叫AdobePSDK.initiateDRMWorkflow來起始DRM工作流程。 如果沒有這個呼叫，DRM視訊將無法播放。<p>介面AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath， <br /> DomString publisherId， <br /> DomString appId， <br /> DomString appVersion， <br /> 布林值privacyModeOn)；<br /> }；</p> </td> 
   <td>初始化已在內部完成，不需要明確呼叫。</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API | 1.3 API |
|--- |--- |
| **DRMAquireLicenseSettings** |  |
| 2.0版沒有變更。 | 列舉DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0；<br> const unsigned int LOCAL_ONLY = 1；<br> const unsigned int ALLOW_SERVER = 2；<br> }； |
| **DRMAuthenticationMethod** |  |
| 2.0版沒有變更。 | 列舉DRMAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0；<br> const unsigned int ANONYMOUS = 1；<br> const unsigned int USERNAME_AND_PASSWORD = 2；<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0版沒有變更。</td> 
   <td><p>介面DRM中繼資料<br /> {<br /> readonly屬性DomString serverUrl；<br /> 唯讀屬性DomString licenseId；<br /> 唯讀屬性DRMPolicyArray原則； <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindows {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面DRMPlaybackTimeWindow {<br /> 唯讀屬性int playbackPeriodInSeconds；<br /> 唯讀屬性long playbackStartDate；<br /> 唯讀屬性long playbackEndDate；<br /> }；</p> </td> 
   <td><p>介面DRMPlaybackTimeWindow {<br /> 唯讀屬性int periodInSeconds；<br /> 唯讀屬性int startDate；<br /> readonly attribute int endDate；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0版沒有變更。</td> 
   <td><p>介面DRMLicense {<br /> 唯讀屬性Uint8Array位元組；<br /> 唯讀屬性Date licenseStartDate；<br /> 唯讀屬性Date licenseEndDate；<br /> 唯讀屬性Date offlineStorageStartDate；<br /> 唯讀屬性Date offlineStorageEndDate； <br /> readonly屬性DomString serverUrl；<br /> 唯讀屬性DomString licenseID；<br /> 唯讀屬性DomString policyID；<br /> 唯讀屬性DRMPlaybackTimeWindow playbackTimeWindow；<br /> 唯讀屬性Object customProperties；<br /> }； </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicenseDomain {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面DRMLicenseDomain {<br /> 唯讀屬性DomString authenticationDomain；<br /> 唯讀屬性DRMAuthenticationMethod authenticationMethod； <br /> readonly屬性DomString serverUrl；<br /> }；</p> </td> 
   <td><p>介面DRMLicenseDomain {<br /> 唯讀屬性DomString authDomain；<br /> 唯讀屬性DRMAuthenticationMethod authMethod； <br /> readonly屬性DomString serverURL；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPolicy {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面DRMPolicy<br /> {<br /> 唯讀屬性DomString authenticationDomain；<br /> 唯讀屬性DRMAuthenticationMethod authenticationMethod；<br /> <br /> 唯讀屬性DomString displayName；<br /> 唯讀屬性DRMLicenseDomain licenseDomain；<br /> }；</p> </td> 
   <td><p>介面DRMPolicy<br /> {<br /> 唯讀屬性DomString authDomain；<br /> 唯讀屬性DRMAuthenticationMethod authMethod；<br /> 唯讀屬性DomString dispName；<br /> 唯讀屬性DRMLicenseDomain licenseDomain；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面DRManager ：事件目標{<br /> 無效acquireLicense(DRMMetadata中繼資料， <br /> DRMAquireLicenseSettings設定， <br /> DRMAquireLicenseListener)；<br /> 無效acquirePreviewLicense(DRMMetadata中繼資料， <br /> DRMAquireLicenseListener)；<br /> 無效驗證(DRMMetadata中繼資料， <br /> DomString url、<br /> DomString &amp;authenticationDomain， <br /> DomString使用者， <br /> DomString密碼， <br /> DRMAuthenticateListener)；<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array陣列、DRMErrorListener)；<br /> void initialize(DRMOperationCompleteListener)；<br /> 屬性long maxOperationTime；<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> 布林值forceRefresh， <br /> DRMOperationCompleteListener)；<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> DRMOperationCompleteListener)；<br /> <br /> void resetDRM(DRMOperationCompleteListener)；<br /> 無效returnLicense(DomString serverURL， <br /> DomString licenseID、 <br /> DomString policyID， <br /> 布林值commitImmediately，<br /> DRMReturnLicenseListener)；<br /> void setAuthenticationToken(<br /> DRM中繼資料， <br /> DomString authenticationDomain， <br /> Uint8Array權杖， <br /> DRMOperationCompleteListener)；<br /> void storeLicenseBytes(Uint8Array licenseBytes， <br /> DRMOperationCompleteListener)；<br /> }；</p> </td> 
   <td><p>介面DRManager ：事件目標{<br /> 無效acquireLicense(DRMMetadata中繼資料， <br /> DRMAquireLicenseSettings設定， <br /> EventContext eventContext)；<br /> 無效acquirePreviewLicense(DRMMetadata中繼資料， <br /> EventContext eventContext)；<br /> 無效驗證(DRMMetadata中繼資料， <br /> DomString url、<br /> DomString &amp;authenticationDomain， <br /> DomString使用者， <br /> DomString密碼， <br /> EventContext eventContext)；<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array陣列、EventContext eventContext)；<br /> void initialize(EventContext eventContext)；<br /> 屬性long maxOperationTime；<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> 布林值forceRefresh， <br /> EventContext eventContext)；<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> EventContext eventContext)；<br /> <br /> 無效resetDRM(EventContext eventContext)；<br /> 無效returnLicense(DomString serverURL， <br /> DomString licenseID、<br /> DomString policyID， <br /> 布林值commitImmediately，<br /> EventContext eventContext)；<br /> void setAuthenticationToken(<br /> DRM中繼資料， <br /> DomString authenticationDomain， <br /> Uint8Array權杖， <br /> EventContext eventContext)；<br /> void storeLicenseBytes(Uint8Array licenseBytes， <br /> EventContext eventContext)；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p>類別DRMErrorListener ： <br /> public psdkutils：：PSDKInterfaceWithUserData {<br /> 公用：<br /> virtual void onDRMError(uint32_t major， <br /> uint32_t次要， <br /> 常數psdkutils：： PSDKString&amp; errorString， <br /> const psdkutils：：PSDKString&amp; errorServerUrl) = 0；<br /> <br /> 受保護：<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>事件/介面/說明 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>當DRMManger的其中一個非同步方法發生錯誤時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類別DRMOperationCompleteListener ： <br /> 公用DRMErrorListener {<br /> 公用：<br /> virtual void onDRMOperationComplete() = 0；<br /> <br /> 受保護：<br /> virtual ~DRMOperationCompleteListener() {}<br /> }；</p> </td> 
   <td>事件/介面/說明 
    <ul> 
     <li>kEventDRMIinitializationComplete<p>/ PSDKEvent</p> <p>DRM初始化完成時。</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>當joinLicenseDomain()動作成功完成時。</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>當leaveLicenseDomain()動作成功完成時。</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>當resetDRM()動作成功完成時。</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>當setAuthenticationTokenSet()動作成功完成時。</p> </li> 
     <li>kEventDRMLicenseStore<p>/ PSDKEvent</p> <p>當storeLicenseBytes()動作成功完成時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類別DRMAuthenticateListener ： <br /> 公用DRMErrorListener {<br /> 公用：<br /> virtual void onAuthenticationComplete(<br /> psdkutils：：PSDKImmutableByteArray* <br /> authenticationToken) = 0；<br /> <br /> 受保護：<br /> virtual ~DRMAuthenticateListener() {}<br /> }</p> </td> 
   <td>事件/介面/說明 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>當DRMManager：：authenticate方法呼叫成功時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類別DRMAquireLicenseListener： <br /> 公用DRMErrorListener {<br /> 公用：<br /> virtual void onLicenseAcquired(const DRMLicense*) = 0；<br /> <br /> 受保護：<br /> virtual ~DRMAquireLicenseListener() {}<br /> }；</p> </td> 
   <td>事件/介面/說明 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>當DRMManager：：acquirePreviewLicense方法呼叫成功時。</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>當DRMManager：：acquireLicense方法呼叫成功時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類別DRMReturnLicenseListener： <br /> 公用DRMErrorListener {<br /> 公用：<br /> virtual void onLicenseReturnComplete(uint32_t numReturned ) = 0；<br /> <br /> 受保護：<br /> virtual ~DRMReturnLicenseListener() {}<br /> }；</p> </td> 
   <td>事件/介面/說明 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>當DRMManager：：returnLicense方法呼叫成功時。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0的一般播放API元素變更 {#generic-playback-api-element-changes-for}

下表比較JavaScript TVSDK 1.3和2.0之間的一般播放API元素。

此主題中的表格：

* MediaResource
* MediaPlayer
* Abrcontrolparameters
* BufferControlParameters
* 文字格式
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面MediaResource {<br /> 屬性DomString url； <br /> 屬性不帶正負號的短型別；<br /> 屬性物件中繼資料；<br /> const unsigned short TYPE_HLS；<br /> const unsigned short TYPE_HDS；<br /> const unsigned short TYPE_DASH；<br /> const unsigned short TYPE_CUSTOM；<br /> const unsigned short TYPE_UNKNOWN；<br /> }；</p> </td> 
   <td><p>介面MediaResource {<br /> 屬性DomString url；<br /> 屬性DomString型別；<br /> 屬性物件中繼資料；<br /> <br /> <br /> <br /> <br /> <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayer {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面MediaPlayer ： EventTarget<br /> {<br /> void prepareToPlay( double position)；<br /> void play()；<br /> void pause()；<br /> void seek( double position)；<br /> void seekToLocal( double position)；<br /> void reset()；<br /> void release()；<br /> void replaceCurrentItem(MediaPlayerItem item)；<br /> 無效replaceCurrentResource(MediaResource資源， <br /> MediaPlayerItemConfig)； <br /> void suspend()；<br /> void restore()；<br /> 無效notifyClick()；<br /> <br /> 唯讀屬性TimeRange playbackRange；<br /> 唯讀屬性TimeRange seekableRange；<br /> 唯讀屬性double currentTime；<br /> 唯讀屬性double localTime；<br /> 唯讀屬性TimeRange bufferedRange；<br /> 唯讀屬性DRMManager drmManager；<br /> 唯讀屬性MediaPlayerItem currentItem；<br /> <br /> //播放器狀態<br /> <br /> <br /> const unsigned short PLAYER_STATUS_INITIALIZED；<br /> const unsigned short PLAYER_STATUS_PREPARING；<br /> const unsigned short PLAYER_STATUS_PREPARED；<br /> const unsigned short PLAYER_STATUS_PLAYING；<br /> const unsigned short PLAYER_STATUS_PAUSED；<br /> const unsigned short PLAYER_STATUS_SEEKING；<br /> const unsigned short PLAYER_STATUS_COMPLETE；<br /> const unsigned short PLAYER_STATUS_ERROR；<br /> const unsigned short PLAYER_STATUS_RELEASED；<br /> <br /> 唯讀屬性（不帶正負號的短狀態）；<br /> <br /> 屬性無符號短磁碟區；<br /> 屬性ABRControlParameters abrControlParameters；<br /> 屬性BufferControlParameters bufferControlParameters；<br /> <br /> const unsigned short VISIBLE； //For CC visibility<br /> const unsigned short INVISIBLE； //For CC visibility<br /> 屬性不帶正負號的shortVisibility；<br /> 屬性TextFormat ccStyle；<br /> 唯讀屬性PlaybackMetrics playbackMetrics；<br /> <br /> 屬性雙倍率；<br /> 屬性MediaPlayerView；<br /> 唯讀屬性時間軸；<br /> 屬性雙currentTimeUpdateInterval； <br /> //設定2.0將不支援此設定<br /> }；</p> </td> 
   <td><p>介面MediaPlayer ： EventTarget<br /> {<br /> void prepareToPlay( int position)；<br /> void play()；<br /> void pause()；<br /> void seek( int position)；<br /> void seekToLocalTime( int position)；<br /> void reset()；<br /> void release()；<br /> 無效replaceCurrentItem（MediaResource來源）；<br /> <br /> <br /> <br /> <br /> <br /> <br /> 唯讀屬性TimeRange playbackRange；<br /> 唯讀屬性TimeRange seekableRange；<br /> 唯讀屬性double currentTime；<br /> 唯讀屬性double localTime；<br /> 唯讀屬性TimeRange bufferedRange；<br /> 唯讀屬性DRMManager drmManager；<br /> 唯讀屬性MediaPlayerItem currentItem；<br /> <br /> //播放器狀態<br /> const unsigned short PLAYER_STATE_IDLE；<br /> const unsigned short PLAYER_STATE_INITIALIZING；<br /> const unsigned short PLAYER_STATE_INITIALIZED；<br /> const unsigned short PLAYER_STATE_PREPARING；<br /> const unsigned short PLAYER_STATE_PREPARED；<br /> const unsigned short PLAYER_STATE_PLAYING；<br /> const unsigned short PLAYER_STATE_PAUSED；<br /> const unsigned short PLAYER_STATE_SEEKING；<br /> const unsigned short PLAYER_STATE_COMPLETE；<br /> const unsigned short PLAYER_STATE_ERROR；<br /> const unsigned short PLAYER_STATE_RELEASED；<br /> const unsigned short PLAYER_STATUS_SUSPENDED；<br /> readonly attribute unsigned short state；<br /> <br /> 屬性無符號短磁碟區；<br /> 屬性ABRControlParameters abrControlParameters；<br /> 屬性BufferControlParameters bufferControlParameters；<br /> <br /> 唯讀無符號短VISIBLE； //For CC visibility<br /> 唯讀無符號SHORT INVISIBLE； //用於CC可見性<br /> 屬性不帶正負號的shortVisibility；<br /> 屬性TextFormat ccStyle；<br /> 唯讀屬性PlaybackMetrics playbackMetrics；<br /> 屬性MediaPlayerConfig mediaPlayerConfig；<br /> 屬性雙倍率；<br /> 屬性MediaPlayerView；<br /> 唯讀屬性時間軸；<br /> <br /> <br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面MediaPlayerStatus<br /> {<br /> //播放器狀態<br /> const unsigned short PLAYER_STATUS_IDLE；<br /> const unsigned short PLAYER_STATUS_INITIALIZING；<br /> const unsigned short PLAYER_STATUS_INITIALIZED；<br /> const unsigned short PLAYER_STATUS_PREPARING；<br /> const unsigned short PLAYER_STATUS_PREPARED；<br /> const unsigned short PLAYER_STATUS_PLAYING；<br /> const unsigned short PLAYER_STATUS_PAUSED；<br /> const unsigned short PLAYER_STATUS_SEEKING；<br /> const unsigned short PLAYER_STATUS_COMPLETE；<br /> const unsigned short PLAYER_STATUS_ERROR；<br /> const unsigned short PLAYER_STATUS_RELEASED；<br /> const unsigned short PLAYER_STATUS_SUSPENDED；<br /> }；</p> </td> 
   <td>（2.0的新功能）</td> 
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
   <td><p>（2.0版本已刪除）</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>已準備</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdates</p> <p>媒體播放器專案更新時。</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>已更新</p> <p>媒體播放器已成功更新媒體時。</p> </td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>TtmedMetadata</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>時間軸已更新</td> 
   <td>事件</td> 
   <td> </td> 
   <td>時間線已更新</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>在2.0中刪除</td> 
   <td> </td> 
   <td> </td> 
   <td>playstart</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>2.0版本已刪除</td> 
   <td> </td> 
   <td> </td> 
   <td>playComplete</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>statusChanged</td> 
   <td>StatusEvent</td> 
   <td> </td> 
   <td>stateChanged</td> 
   <td>StateEvent</td> 
  </tr> 
  <tr> 
   <td>sizeAvailable</td> 
   <td>大小事件</td> 
   <td> </td> 
   <td>大小</td> 
   <td>大小事件</td> 
  </tr> 
  <tr> 
   <td>adbreakstarted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adbreakstart</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adstarted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adstart</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
   <td> </td> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
  </tr> 
  <tr> 
   <td>adCompleted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adComplete</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakCompleted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakComplete</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>timeChanged</td> 
   <td>時間事件</td> 
   <td> </td> 
   <td>進度</td> 
   <td>ProgressEvent</td> 
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
   <td>搜尋事件</td> 
   <td> </td> 
   <td>seekStart</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>seekEnd</td> 
   <td>搜尋事件</td> 
   <td> </td> 
   <td>seekComplete</td> 
   <td>時間事件</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>LoadInformationevent</td> 
   <td> </td> 
   <td>loadInfo</td> 
   <td>LoadInfoEvent</td> 
  </tr> 
  <tr> 
   <td>operationfailed</td> 
   <td>通知事件</td> 
   <td> </td> 
   <td>operationfailed</td> 
   <td>錯誤事件</td> 
  </tr> 
  <tr> 
   <td>drmMetadataInfoAvailable</td> 
   <td>DRMetadataEvent</td> 
   <td> </td> 
   <td>drmMetadata</td> 
   <td>DRMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>reservationReceived</td> 
   <td>Reservationevent</td> 
   <td> </td> 
   <td>timelineHolderReached</td> 
   <td>時間軸持有人事件</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>bitrateChanged</td> 
   <td>BitrateChangedEvent</td> 
  </tr> 
  <tr> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adclicked<br /> 當使用者點選廣告時。</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>2.0的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> 當播放設定檔變更時。</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>2.0的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdjusted<br /> 當搜尋位置因內部或外部規則而調整時。</td> 
   <td>搜尋事件</td> 
   <td> </td> 
   <td><p>2.0的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>音訊已更新<br /> 媒體播放器專案更新時。 對於包含只有在播放時才能偵測到之音訊曲目的特定串流，此事件會在有新音訊曲目可用時引發。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>註解已更新 <br /> 媒體播放器專案更新時。 對於即時/線性資料流，使用者端必須定期重新整理媒體資源，以偵測新的可用內容。 發生此情況時，某些媒體特性可能會變更。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdates <br /> 媒體播放器專案更新時。 對於即時/線性資料流，使用者端必須定期重新整理媒體資源，以偵測新的可用內容。 發生此情況時，某些媒體特性可能會變更。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> 媒體播放器專案更新時。 對於即時/線性資料流，使用者端必須定期重新整理媒體資源，以偵測新的可用內容。 發生此情況時，某些媒體特性可能會變更。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> 產生計時事件時傳送。</td> 
   <td>Timedevent</td> 
   <td> </td> 
   <td><p>2.0的新增功能</p> </td> 
  </tr> 
 </tbody> 
</table>

### Abrcontrolparameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ；<br /> const unsigned short ABR_POLICY_MODERATE = 1 ；<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ；<br /> <br /> 屬性未簽署的短abrPolicy；<br /> 屬性不帶正負號的int initialBitRate；<br /> 屬性不帶正負號的int minBitRate；<br /> 屬性（不帶正負號）int maxBitRate；<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE；<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE；<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE；<br /> 常數ABRPolicy DEFAULT_ABR_POLICY；<br /> }；</p> </td> 
   <td><p>介面ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ；<br /> const unsigned short ABR_POLICY_MODERATE = 1 ；<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ；<br /> <br /> 屬性未簽署的短abrPolicy；<br /> 屬性不帶正負號的int initialBitRate；<br /> 屬性不帶正負號的int minBitRate；<br /> 屬性（不帶正負號）int maxBitRate；<br /> <br /> <br /> <br /> <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### BufferControlParameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面BufferControlParameters<br /> {<br /> 屬性雙重initialBufferTime；<br /> 屬性double playBufferTime；<br /> 常數雙DEFAULT_INITIAL_BUFFER_TIME；<br /> 持續雙重DEFAULT_PLAY_BUFFER_TIME；<br /> }；</p> </td> 
   <td><p>介面BufferControlParameters<br /> {<br /> 屬性雙重initialBufferTime；<br /> 屬性double playBufferTime；<br /> <br /> <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### 文字格式 {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0無變更</td> 
   <td><p>介面文字格式<br /> {<br /> //色彩<br /> const unsigned short COLOR_DEFAULT = 0 ；<br /> const unsigned short COLOR_BLACK = 1 ；<br /> const unsigned short COLOR_GRAY = 2 ；<br /> const unsigned short COLOR_WHITE = 3 ；<br /> const unsigned short COLOR_BRIGHT_WHITE = 4 ；<br /> const unsigned short COLOR_DARK_RED = 5 ；<br /> const unsigned short COLOR_RED = 6 ；<br /> const unsigned short COLOR_BRIGHT_RED = 7 ；<br /> const unsigned short COLOR_DARK_GREEN = 8 ；<br /> const unsigned short COLOR_GREEN = 9 ；<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ；<br /> const unsigned short COLOR_DARK_BLUE = 11 ；<br /> const unsigned short COLOR_BLUE = 12 ；<br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ；<br /> const unsigned short COLOR_DARK_YELLOW = 14 ；<br /> const unsigned short COLOR_YELLOW = 15 ；<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16 ；<br /> const unsigned short COLOR_DARK_MAGENTA = 17 ；<br /> const unsigned short COLOR_MAGENTA = 18 ；<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19 ；<br /> const unsigned short COLOR_DARK_CYAN = 20 ；<br /> const unsigned short COLOR_CYAN = 21 ；<br /> const unsigned short COLOR_BRIGHT_CYAN = 22 ；<br /> <br /> readonly attribute unsigned short fontColor；<br /> readonly屬性（不帶正負號的short backgroundColor）；<br /> 唯讀屬性（不帶正負號的短fillColor）；<br /> 唯讀屬性（不帶正負號的短edgeColor）；<br /> <br /> //大小<br /> const unsigned short SIZE_DEFAULT = 0 ；<br /> const unsigned short SIZE_SMALL = 1 ；<br /> const unsigned short SIZE_MEDIUM = 2 ；<br /> const unsigned short SIZE_LARGE = 3 ；<br /> <br /> 唯讀屬性（不帶正負號的短大小）；<br /> <br /> //字型邊緣<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ；<br /> const unsigned short FONT_EDGE_NONE = 1 ；<br /> const unsigned short FONT_EDGE_RAULED = 2 ；<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ；<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ；<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ；<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ；<br /> readonly attribute unsigned short fontEdge；<br /> <br /> //字型<br /> const unsigned short FONT_DEFAULT = 0 ；<br /> const unsigned short FONT_MONOSPACE_WITH_SERIFS = 1 ；<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ；<br /> const unsigned short FONT_MONSPACE_WITHOUT_SERIFS = 3 ；<br /> const unsigned short FONT_CASUAL = 4 ；<br /> const unsigned short FONT_CURSIVE = 5 ；<br /> const unsigned short FONT_SMALL_CAPTINGS = 6 ；<br /> 唯讀屬性不帶符號的短字型；<br /> 唯讀屬性（不帶正負號的短字型不透明度）；<br /> readonly屬性（不帶正負號的short backgroundOpacity）；<br /> 唯讀屬性（不帶正負號的短填色不透明度）；<br /> 唯讀屬性（不帶正負號的短DEFAULT_OPACITY）；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面MediaPlayerItemLoader：<br /> {<br /> void load(MediaResource resource， long resourceId，<br /> ItemLoaderListener接聽程式， <br /> MediaPlayerItemConfig) ；<br /> void cancel()；<br /> 唯讀屬性MediaPlayerItem currentItem；<br /> }；</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>介面ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc；<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc；<br /> }</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的媒體特性API元素變更 {#media-characteristics-api-element-changes-for}

下表比較1.3和2.0版之間C++ TVSDK的媒體特性API元素。

此主題中的表格：

* MediaPlayerItem
* Track、AudioTrack、ClosedCaptionsTrack
* 個人資料
* DRMMetadataInfo

### MediaPlayerItem {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面MediaPlayerItem {<br /> 唯讀屬性MediaResource；<br /> readonly屬性long resourceId；<br /> readonly attribute boolean live；<br /> <br /> 唯讀屬性布林值hasAlternateAudio；<br /> 唯讀屬性AudioTrackList audioTracks；<br /> 唯讀屬性AudioTrack selectedAudioTrack；<br /> void selectAudioTrack(AudioTrack track)； <br /> <br /> 唯讀屬性布林值hasClosedCaptions；<br /> 唯讀屬性ClosedCaptionsTrackList closedCaptionsTracks；<br /> 唯讀屬性ClosedCaptionsTrack selectedClosedCaptionsTrack；<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTrack)； <br /> <br /> 唯讀屬性布林值hasTimedMetadata；<br /> 唯讀屬性TimedMetadataList timedMetadata；<br /> 唯讀屬性布林值動態；<br /> <br /> 唯讀屬性布林值isProtected；<br /> 唯讀屬性DRMMetadataInfoList drmMetadataInfos；<br /> 唯讀屬性ProfileList設定檔；<br /> 唯讀屬性Profile selectedProfile；<br /> <br /> 唯讀屬性布林值trickPlaySupported；<br /> 唯讀屬性FloatArray availablePlaybackRates；<br /> 唯讀屬性float selectedPlaybackRate；<br /> <br /> <br /> 唯讀屬性MediaPlayer mediaPlayer；<br /> 唯讀屬性MediaPlayerItemConfig；<br /> }；</p> </td> 
   <td><p>介面MediaPlayerItem {<br /> 唯讀屬性MediaResource；<br /> readonly屬性long resourceId；<br /> readonly attribute boolean live；<br /> <br /> 唯讀屬性布林值hasAlternateAudio；<br /> 唯讀屬性AudioTrackList audioTracks；<br /> 屬性AudioTrack selectedAudioTrack；<br /> <br /> <br /> 唯讀屬性布林值hasClosedCaptions；<br /> 唯讀屬性ClosedCaptionsTrackList ccTracks；<br /> 屬性ClosedCaptionsTrack selectedCCTrack；<br /> <br /> <br /> <br /> 唯讀屬性布林值hasTimedMetadata；<br /> 唯讀屬性TimedMetadataList timedMetadata；<br /> 唯讀屬性布林值動態；<br /> <br /> 唯讀屬性布林值isProtected；<br /> 唯讀屬性DRMMetadataInfoList drmMetadataInfos；<br /> 唯讀屬性ProfileList設定檔；<br /> <br /> <br /> 唯讀屬性布林值trickPlaySupported；<br /> 唯讀屬性Int32Array availablePlaybackRates；<br /> <br /> 唯讀屬性StringList adTags；<br /> <br /> 唯讀屬性MediaPlayer mediaPlayer；<br /> <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### Track / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面追蹤<br /> {<br /> 唯讀屬性DomString名稱；<br /> 唯讀屬性DomString語言；<br /> 唯讀屬性布林值預設；<br /> 唯讀屬性布林值autoSelect；<br /> }； </p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack ： Track<br /> {<br /> 唯讀屬性DomString名稱； //FromTrack<br /> 唯讀屬性DomString language；//FromTrack<br /> 唯讀屬性布林值預設；//從追蹤<br /> 唯讀屬性布林值autoSelect；//FromTrack<br /> <br /> 唯讀屬性（不帶正負號的int pid）；<br /> }；</p> </td> 
   <td><p>介面AudioTrack<br /> {<br /> 唯讀屬性DomString名稱；<br /> 唯讀屬性DomString語言； <br /> 唯讀屬性布林值預設；<br /> 唯讀屬性布林值autoSelect；<br /> 強制的唯讀屬性布林值；<br /> <br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td>2.0無變更</td> 
   <td><p>介面AudioTrackList<br /> {<br /> readonly attribute unsigned long length；<br /> getter AudioTrack （不帶正負號的長索引）；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p>介面ClosedCaptionsTrack ： Track<br /> {<br /> 唯讀屬性DomString名稱； //FromTrack<br /> 唯讀屬性DomString language；//FromTrack<br /> 唯讀屬性布林值預設；// FromTrack<br /> 唯讀屬性布林值autoSelect；//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0；<br /> const unsigned short SERVICE_708_CAPTIONS = 1；<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2；<br /> 唯讀屬性（不帶正負號的短serviceType）；<br /> 強制的唯讀屬性布林值；<br /> }；</p> </td> 
   <td><p>介面ClosedCaptionsTrack<br /> {<br /> 唯讀屬性DomString名稱；<br /> 唯讀屬性DomString語言；<br /> 唯讀屬性布林值預設；<br /> <br /> <br /> 啟用唯讀屬性布林值；<br /> <br /> <br /> <br /> <br /> <br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td>2.0無變更</td> 
   <td><p>介面ClosedCaptionsTrackList<br /> {<br /> readonly attribute unsigned long length；<br /> getter ClosedCaptionsTrack(unsigned long index)；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### 個人資料 {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>設定檔： 2.0無變更</td> 
   <td><p>介面設定檔<br /> {<br /> readonly屬性（不帶正負號的int寬度）；<br /> 唯讀屬性（不帶正負號的int高度）；<br /> 唯讀屬性（不帶正負號的int bitRate）；<br /> }； </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList： 2.0無變更</td> 
   <td><p>介面設定檔清單<br /> {<br /> readonly attribute unsigned long length；<br /> getter設定檔（無符號長索引）；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>：2.0版沒有變更</td> 
   <td><p>介面DRMMetadataInfo<br /> { <br /> 唯讀屬性DRMMetadata中繼資料；<br /> 唯讀屬性long prefetchTimestamp；<br /> 唯讀屬性TimeRange timeRange；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>：2.0版沒有變更</td> 
   <td><p>介面DRMMetadataInfoList<br /> {<br /> readonly attribute unsigned long length；<br /> getter DRMMetadataInfo （無符號長索引）；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

## 將C++錯誤對應至不同語言的例外 {#mapping-c-errors-to-exceptions-in-different-languages}

您可以將C++錯誤碼對應至不同語言的例外。

C++ PSDK的API具有「禁止擲回」原則。 大部分的API方法會傳回PSDKErrorCode值，指出方法是否已成功執行。 系統會透過錯誤事件通知非同步錯誤。

ActionScript和JAVA PSDK有不同的原則。 大部分的錯誤都會擲回ArgumentError或IllegalStateException，指出無法執行方法的同步部分。 系統不會攔截到這些例外狀況，而應用程式程式碼會負責處理例外狀況。 它們通常包含方法呼叫失敗之原因的有用資訊。 例如，如果以無效狀態呼叫prepareToPlay命令，則會擲回下列例外狀況：

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

ActionScript/JAVA也會從建構函式擲回例外狀況，以表示某些內部物件未正確建立。 這些例外狀況會在內部處理，而不會傳播至應用程式。 例外會包含在傳送給應用程式的警告通知中

例如，如果針對收到的廣告回應找不到有效的媒體檔案，則無法建立有效的廣告資產物件或廣告。 因此，時間軸上不會放置任何廣告，且會傳送NotificationEvent.OperationFailed通知。

非同步從Adobe Video Engine (AVE)收到的錯誤或警告程式碼會以一般事件的形式傳送到應用程式。 通知事件包含所有收到的錯誤代碼和任何其他中繼資料，例如URL、資源識別碼、控制代碼等。 如果錯誤嚴重且無法繼續播放目前的媒體，MediaPlayer會轉換為ERROR狀態並傳送onStatusChanged回呼或MediaPlayerStatusChanged.STATUS_CHANGED事件。 如果可以繼續播放，則會傳送一般通知事件。

<table> 
 <tbody> 
  <tr> 
   <th>C++錯誤（PSDKError程式碼）</th> 
   <th> </th> 
   <th>Java</th> 
   <th>ActionScript</th> 
   <th>JavaScript</th> 
  </tr> 
  <tr> 
   <td>kECInvalidArgument</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>引數錯誤</td> 
   <td>例外狀況代碼= 1，說明= "INVALID_ARGUMENT"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>Kecnullpointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>引數錯誤</td> 
   <td>例外狀況代碼= 2，說明= "GENERIC_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>例外狀況代碼= 3，說明= "ILLEGAL_STATE"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 4，說明= "GENERIC_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 5，說明= "CREATION_FAILED"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 5，說明= "CREATION_FAILED"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 7，說明= "DATA_NOT_AVAILABLE"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 8，說明= "SEEK_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 9，說明= "UNSUPPORTED_FEATURE"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 10，說明= "RANGE_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 11，說明= "CODEC_NOT_SUPPORTED"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMmediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 12，說明= "MEDIA_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 13，說明= "NETWORK_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error或MediaPlayerNotification.Warning</td> 
   <td>MediaError或通知事件</td> 
   <td>例外狀況代碼= 14，說明= "GENERIC_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 15，說明= "INVALID_SEEK_TIME"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 16，說明= "AUDIO_TRACK_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>執行緒錯誤</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 17，說明= "GENERIC_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 18，說明= "GENERIC_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNotImplements</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 19，說明= "GENERIC_ERROR"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外狀況代碼= 200，說明= "PLAYBACK_OPERATION_FAILED"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>通知事件</td> 
   <td>例外狀況代碼= 201，說明= "NATIVE_WARNING"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>例外狀況代碼= 202，說明= "AD_RESOLVER_FAILED"及additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的公用程式和Helper API元素變更 {#utility-and-helper-api-element-changes-for}

下表比較1.3和2.0版之間JavaScript TVSDK的公用程式和Helper API元素。

此主題中的表格：

* 版本
* 時間範圍
* QOSProvider
* 裝置資訊
* LoadInfo
* 檢視
* 播放資訊

### 版本 {#version}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面版本<br /> {<br /> 唯讀屬性DomString版本；<br /> 唯讀屬性DomString說明；<br /> 唯讀屬性長主要；<br /> 唯讀屬性long minor；<br /> 唯讀屬性長修訂；<br /> readonly屬性long apiVersion；<br /> }；</p> </td> 
   <td><p>介面版本<br /> {<br /> 唯讀屬性DomString版本；<br /> 唯讀屬性DomString說明；<br /> 唯讀屬性DomString major；<br /> 唯讀屬性DomString minor；<br /> 唯讀屬性DomString修訂版本；<br /> 唯讀屬性DomString apiVersion；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### 時間範圍 {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0無變更</td> 
   <td><p>介面TimeRange<br /> {<br /> readonly attribute unsigned long begin；<br /> readonly attribute unsigned long end；<br /> 唯讀屬性無符號長持續時間；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0無變更</td> 
   <td><p>介面QOSProvider<br /> {<br /> 無效attachMediaPlayer（MediaPlayer播放器）；<br /> 無效detachMediaPlayer()；<br /> <br /> 唯讀屬性DeviceInformation deviceInformation；<br /> 唯讀屬性PlaybackInformation playbackInformation；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### 裝置資訊 {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面裝置資訊<br /> {<br /> 唯讀屬性DomString os；<br /> <br /> <br /> <br /> 唯讀屬性DomString ID；<br /> 唯讀屬性int densityDPI；<br /> 唯讀屬性int heightPixels；<br /> 唯讀屬性int widthPixels；<br /> 唯讀屬性布林值seekToKeyFrame；<br /> }；</p> </td> 
   <td><p>介面裝置資訊<br /> {<br /> 唯讀屬性DomString os；<br /> 唯讀屬性int sdk；<br /> 唯讀屬性DomString模型；<br /> 唯讀屬性DomString製造商；<br /> 唯讀屬性DomString ID；<br /> 唯讀屬性int densityDPI；<br /> 唯讀屬性int heightPixels；<br /> 唯讀屬性int widthPixels；<br /> <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### LoadInfo {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0無變更</td> 
   <td><p>介面載入資訊<br /> {<br /> 唯讀屬性DomString url；<br /> 唯讀屬性int大小；<br /> 唯讀屬性double downloadDuration；<br /> 唯讀屬性int periodIndex；<br /> 唯讀屬性double mediaDuration；<br /> 唯讀屬性短TRACK_TYPE_FRAGMENT；<br /> 唯讀屬性簡短TRACK_TYPE_TRACK；<br /> 唯讀屬性簡短TRACK_TYPE_MANIFEST；<br /> 唯讀屬性短型別；<br /> 唯讀屬性DomString trackName；<br /> 唯讀屬性DomString trackType；<br /> 唯讀屬性int trackIndex；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### 檢視 {#view}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0無變更</td> 
   <td><p>介面檢視<br /> {<br /> 唯讀屬性（不帶正負號的短x）；<br /> 唯讀屬性（不帶正負號的短y）；<br /> 唯讀屬性不帶正負號的短寬度；<br /> 唯讀屬性不帶正負號的短高度；<br /> <br /> void setSize（無符號短寬度，無符號短高度）；<br /> void setPos(unsigned short x， unsigned short y)；<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### 播放資訊 {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面播放資訊<br /> {<br /> 唯讀屬性double timeToFirstByte；<br /> 唯讀屬性double timeToLoad；<br /> 唯讀屬性double timeToStart；<br /> 唯讀屬性double timeToFail；<br /> 唯讀屬性int totalSecondsPlayed；<br /> 唯讀屬性int totalSecondsSpent；<br /> 唯讀屬性double frameRate；<br /> 唯讀屬性int droppedFrameCount；<br /> readonly attribute int esceptedBandwidth；<br /> readonly attribute int bitrate；<br /> 唯讀屬性double bufferTime；<br /> readonly attribute int bufferLength；<br /> 唯讀屬性int emptyBufferCount；<br /> 唯讀屬性double bufferingTime；<br /> }；</p> </td> 
   <td><p>介面播放資訊<br /> {<br /> 唯讀屬性double timeToFirstByte；<br /> 唯讀屬性double timeToLoad；<br /> 唯讀屬性double timeToStart；<br /> 唯讀屬性double timeToFail；<br /> 唯讀屬性int totalSecondsPlayed；<br /> 唯讀屬性int totalSecondsSpent；<br /> 唯讀屬性double frameRate；<br /> 唯讀屬性int droppedFrameCount；<br /> <br /> readonly attribute int bitrate；<br /> 唯讀屬性double bufferTime；<br /> readonly attribute int bufferLength；<br /> 唯讀屬性int emptyBufferCount；<br /> 唯讀屬性double bufferingTime；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html) 頁面。
