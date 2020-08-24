---
title: TVSDK轉換——針對JavaScript 1.3至2.0
seo-title: TVSDK轉換——針對JavaScript 1.3至2.0
description: 2.0版中，許多方法簽名和API元素名稱已變更。請檢閱這些表格，以檢視所有API變更詳細資訊。
seo-description: 2.0版中，許多方法簽名和API元素名稱已變更。請檢閱這些表格，以檢視所有API變更詳細資訊。
uuid: d2d1742d-c90c-43f5-94fc-8c4a57cb8ed4
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: c732f54d-116c-43f3-bec4-5e71af208426
translation-type: tm+mt
source-git-commit: cfd6da49e85e13e29e8458ee98231a8b476867db
workflow-type: tm+mt
source-wordcount: '5058'
ht-degree: 0%

---


# TVSDK轉換——針對JavaScript 1.3至2.0 {#tvsdk-conversion-to-for-javascript}

2.0版中，許多方法簽名和API元素名稱已變更。請檢閱這些表格，以檢視所有API變更詳細資訊。

## 在JavaScript中實作回呼函式 {#implement-callback-functions-in-javascript}

方法檔案中的注釋建議您需要實施的回呼簽名。

對於JavaScript,API語法是以網頁ID為基礎。 對於TVSDK介面，方法名稱稱為 *methodName*()。 對於應用程式要實現的方法，將向介面添加名為 ** methodNameCallbackFunc的讀／寫屬性，而您的應用程式應將其設定為指向實現該方法的函式。 例如：

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

## 2.0的廣告工作流程API元素變更 {#advertising-workflow-api-element-changes-for}

這些表格會比較1.3版和2.0版之間JavaScript TVSDK的廣告工作流程API元素。

本主題中的表：

* TimedMetadata
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* 位置
* 機會
* 保留
* 時間軸／時間軸項目／時間軸標籤
* AdBreak
* 廣告/ AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* 時間軸操作
* AdBreakPlacement
* AuditudeSettings

### TimedMetadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMetadata</strong>:interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0; <br /> const unsigned short metadata_TYPE_ID3 = 1; <br /> 只讀屬性無符號短類型； <br /> 只讀屬性時間長；<br /> readonly屬性DomString id;<br /> readonly屬性DomString名稱；<br /> readonly屬性DomString內容； <br /> 唯讀屬性物件中繼資料；<br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0;<br /> const unsigned short metadata_TYPE_ID3 = 1;<br /> readonly屬性unsigned short metadataType;<br /> 只讀屬性時間長；<br /> 只讀屬性long id;<br /> readonly屬性DomString名稱；<br /><br /> 唯讀屬性物件中繼資料；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>:（2.0版無變更）</td> 
   <td><p>interface TimedMetadataList {<br /> readonly attribute unsigned long length;<br /> getterTimedMetadata(unsigned long index);<br /> };</p> </td> 
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
   <td><p>介面AdSignlingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CLEASS, <br /> const unsigned short MODE_SERVER_MAP, <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>這會取代MetadataKeys::MANIFEST_CEAS索引鍵。</td> 
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
   <td><p>Interface AdvertisingMetadata { <br /> attribute AdSignalingMode模式； <br /> 屬性AdBreakWatchedPolicy adBreakAsWatched; <br /> 屬性boolean livePreroll; <br /> 屬性布林delayAdLoading; <br /> };</p> </td> 
   <td>此功能由<p>中繼資料索引鍵：:ADVERTISING_METADATA</p> key.</td> 
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
   <td><p>Interface CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> 不帶符號的短TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> 屬性無符號短類型； <br /> 屬性布林adjustSeekPosition; <br /> 屬性TimeRangeList timeRangeList; <br /> };</p> </td> 
   <td>（2.0的新增功能）</td> 
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
   <td><p>interface ReplaceTimeRange { <br /> attribute unsigned long begin; <br /> 只讀屬性無符號長端； <br /> 屬性無符號長期； <br /> attribute unsigned long replaceDuration; <br /> };</p> </td> 
   <td>（2.0的新增功能）</td> 
  </tr> 
 </tbody> 
</table>

### 位置 {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>Interface Placement { <br /> const unsigned short TYPE_MID_ROLL; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> 只讀屬性無符號短類型； <br /> 只讀屬性時間長； <br /> 只讀屬性長持續時間； <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> 只讀屬性無符號短模式； <br /> 只讀屬性TimeRange範圍； <br /> };</p> </td> 
   <td>（2.0的新增功能）</td> 
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
   <td><p>interface Opportunity { <br /> readonly屬性DomString id; <br /> 唯讀屬性位置； <br /> 只讀屬性對象設定； <br /> readonly屬性對象customParameters; <br /> }; </p> </td> 
   <td>（2.0的新增功能）</td> 
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
   <td><p>介面保留{ <br /> readonly attribute TimeRange range; <br /> 只讀屬性長持有； <br /> }; </p> </td> 
   <td> （2.0的新增功能）</td> 
  </tr> 
 </tbody> 
</table>

### 時間軸／時間軸項目／時間軸標籤 {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p><strong>時間軸</strong>:interface timeline <br /> { readonly attribute TimelineMarkerList timelineMarkers; <br /> readonly屬性timelineItemList timelineItems; <br /> double convertToLocalTime(double time); <br /> double convertToVirtualTime(double time); <br /> };</p> </td> 
   <td><p>interface timeline {<br /> readonly attribute TimelineMarkerList timelineMarkers;<br /><br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>時間軸項目</strong>:interface TimelineItem :<br /> TimelineMarker {<br /> readeronly屬性long id; <br /> 只讀屬性TimeRange virtualRange; <br /> readonly屬性TimeRange localRange; <br /> 只讀屬性布林掛接； <br /> 只讀屬性布爾型臨時； <br /> }; </p> </td> 
   <td>（2.0的新增功能）</td> 
  </tr> 
  <tr> 
   <td><strong>TimelineMarker</strong>:（2.0版無變更）</td> 
   <td><p>interface TimelineMarker {<br /> readonly attribute double time;<br /> 只讀屬性雙持續時間；<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdBreak {#adbreak}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreak {<br /> readonly <br /> attribute <br /><br /> double duration;<br /> 唯讀屬性AdList廣告；<br /><br /> <br /> readonly屬性AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>interface AdBreak {<br /> readonly attribute double time;<br /> readonly屬性double replaceDuration;<br /><br /> 只讀屬性雙持續時間；<br /> readonly屬性AdList adList;<br /><br /> readonly屬性DomString資料；<br /><br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### 廣告/ AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>廣告</strong>:interface Ad {<br /> readonly attribute AdAsset primaryAsset;<br /> readonly屬性AdAssetList companionAssets;<br /><br /> 只讀屬性雙持續時間；<br /> readonly屬性DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0;<br /> const unsigned short ADTYPE_NONLINEAR = 1;<br /><br /> readonly屬性unsigned short adType;<br /> readonly屬性AdInsertionType adInsertionType; <br /> <br /> 只讀屬性布爾可點選； <br /> readonly屬性boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>interface Ad {<br /> readonly attribute AdAsset primaryAsset;<br /> readonly屬性AdAssetList companionAssets;<br /><br /> 只讀屬性雙持續時間；<br /> readonly屬性DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0;<br /> const unsigned short ADTYPE_NONLINEAR = 1;<br /><br /> 只讀屬性無符號短類型；<br /> readonly屬性AdInsertionType insertionType; <br /> 只讀屬性對象跟蹤器；<br /><br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>:（2.0版無變更）</td> 
   <td><p>interface AdAsset {<br /> readonly attribute DomString id;<br /> 只讀屬性雙持續時間；<br /> 只讀屬性MediaResource資源；<br /> readonly屬性AdClick adClick;<br /> 唯讀屬性物件中繼資料；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>:（2.0版無變更）</td> 
   <td><p>interface AdClick {<br /> readonly attribute DomString id;<br /> readonly屬性DomString標題；<br /> readonly屬性DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>:（2.0版無變更）</td> 
   <td><p>interface AdList {<br /> readonly attribute unsigned long length;<br /> getter Ad（無號長索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>:（2.0版無變更）</td> 
   <td><p>interface AdAssetList {<br /> readonly attribute unsigned long length;<br /> getterAdAsset(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>:interface AdBannerAsset:AdAsset<br /> {<br /> readonly attribute int width;<br /> 唯讀屬性int height;<br /> readonly屬性DomString staticUrl;<br /> readonly屬性DomString height;<br /> readonly屬性DomString width;<br /> };</p> </td> 
   <td> 2.0的新功能</td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>:interface AdBreakTimelineItem:TimelineItem { <br /> readonly屬性AdBreak adBreak; <br /> readonly屬性AdTimelineItemList項目； <br /> }; </p> </td> 
   <td> （2.0的新增功能）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>:interface AdTimelineItem:TimelineItem { <br /> readonly屬性AdBreak adBreak; <br /> 唯讀屬性廣告； <br /> }; </p> </td> 
   <td> （2.0的新增功能）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>:interface AdBreakTimelineItemList { <br /> readonly attribute unsigned long length; <br /> getterAdBreakTimelineItem(unsigned long index); <br /> };</p> </td> 
   <td> （2.0的新增功能）</td> 
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
   <td><p>interface AdBreakPolicy {<br /> readonly attribute short AD_BREAK_POLICY_SKIP;<br /> readonly屬性short AD_BREAK_POLICY_PLAY;<br /> readonly屬性short AD_BREAK_POLICY_REMOVE;<br /> readonly屬性short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> readeronly屬性short AD_BREAK_POLICY_SKIP;<br /> readonly屬性short AD_BREAK_POLICY_PLAY;<br /> readonly屬性short AD_BREAK_POLICY_REMOVE;<br /> readonly屬性short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakWatchedPolicy {<br /> readeronly屬性short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> readonly屬性short AD_BREAK_AS_WATCHED_ON_END;<br /> readonly屬性short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> readonly屬性short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> readonly屬性short AD_BREAK_AS_WATCHED_ON_END;<br /> readonly屬性short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> readeronly屬性short AD_POLICY_PLAY;<br /> readonly屬性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> readonly屬性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;readonly屬性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /><br /> readonly屬性short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> readonly屬性short AD_POLICY_PLAY;<br /> readonly屬性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> readonly屬性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> readonly屬性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> readonly屬性short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly屬性short AD_POLICY_MODE_SEEK;<br /> readonly屬性short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly屬性short AD_POLICY_MODE_SEEK;<br /> readonly屬性short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {readonly attribute<br /> AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> readonly屬性AdTimelineItem adTimelineItem;<br /> readonly屬性double currentTime;<br /> readonly屬性double seekToTime;<br /> 只讀屬性雙速率；<br /> 只讀屬性短模式；//AdPolicyMode<br /> };</p> </td> 
   <td><p>interfaceAdPolicyInfo {readonly<br /> attribute AdBreakPlacementList <br /> adBreakLactions;<br /> 唯讀屬性廣告；<br /> readonly屬性double currentTime;<br /> readonly屬性double seekToTime;<br /> 只讀屬性雙速率；<br /> 只讀屬性短模式；//AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaceAdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute object selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyPolicyInfo);<br /> */<br /> attribute object selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyPolicyInfo);<br /> */<br /> attribute object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyPolicyInfo);<br /> */<br /> attribute object selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaceAdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute object selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute object selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyPolicyInfo);<br /> */<br /> attribute object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyPolicyInfo);<br /> */<br /> attribute object selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
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
   <td><p>interface TimelineOperation { <br /> readonly屬性位置； <br /> };</p> </td> 
   <td> （2.0的新增功能）</td> 
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
   <td><p>介面AdBreakPlacement:TimelineOperation {<br /> readonly attribute AdBreak adBreak;<br /> 唯讀屬性位置；// From TimelineOperation<br /> readonly attribute double time;<br /> 只讀屬性雙持續時間；<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {<br /> readonly attribute AdBreak adBreak;<br /> 唯讀屬性位置；<br /> 只讀屬性加倍時間；<br /> 只讀屬性雙持續時間；<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AuditudeSettings {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面AuditudeSettings:AdvertisingMetadata { <br /> attribute DomString zoneId; <br /> 屬性DomString mediaId; <br /> 屬性DomString defaultMediaId ; <br /> 屬性DomString域； <br /> 屬性物件targettingInfo; <br /> attribute Object customParameters; <br /> 屬性Boolean creativePackaingEnabled ;<br /> 屬性Boolean showStaticBanners;<br /> };</p> </td> 
   <td>功能由MetadataKeys::AUDITUDE_METADATA_KEY金鑰提供。</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的自訂API元素變更 {#customization-api-element-changes-for}

這些表格會比較1.3版和2.0版之間JavaScript TVSDK的自訂API元素。

本主題中的表：

* MediaPlayerItemConfig
* ContentFactory
* 網路配置

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemConfig {<br /> attribute ContentFactory adFactory;<br /> attribute StringList subscribeTags;<br /><br /> attribute StringList adTags;<br /><br /> <br /> 屬性AdSigningMode adSigningMode;<br /> attribute CustomRangeMetadata customRangeMetadata;<br /> 屬性NetworkConfiguration networkConfiguration;<br /> 屬性AdvertisingMetadata advertisingMetadata;<br /> 屬性Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interface MediaPlayerConfig {<br /> attribute <br /> StringList <br /><br /> adTags;<br /> attribute StringList subscribedTags;<br /> 屬性MediaPlayerClientFactory clientFactory;<br /><br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ContentFactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem項目);<br /> */<br /> attrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem項目);<br /> */<br /> attrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 網路配置 {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface NetworkConfiguration<br /> {<br /> attribute boolean forceNativeNetworking;<br /> 屬性boolean useRedirectedUrl;<br /> 屬性物件cookieHeader;<br /> 屬性boolean readSetCookieHeader;<br /> attribute int masterUpdateInterval; <br /> 屬性boolean useCookieHeaderForAllRequests;<br /> attribute int readLimit;<br /> };</p> </td> 
   <td>在1.3中，其中部分功能是由MetadataKeys提供</td> 
  </tr> 
 </tbody> 
</table>

## 2.0版的DRM API元素變更 {#drm-api-element-changes-for}

這些表格會比較1.3版和2.0版之間JavaScript TVSDK的DRM API元素。

本主題中的表：

* DRM工作流初始化
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRMManager

### DRM工作流初始化 {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>應用程式需要呼叫AdobePSDK.initiateDRMWorkflow以啟動DRM工作流程。 沒有此呼叫，DRM影片將無法播放。<p>interface AdobePSDK<br /> {void initiateDRMWorkFlow(<br /> DomString appStoratePath,<br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /><br /> Boolean privacyModeOn);<br /> };</p> </td> 
   <td>初始化是在內部完成的，不需要明確呼叫。</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API | 1.3 API |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| 2.0版沒有變更。 | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| 2.0版沒有變更。 | ENUM DRMAuthenticationMethod <br><br> {const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0版沒有變更。</td> 
   <td><p>interface DRMMetadata<br /> {<br /> readonly attribute DomString serverUrl;<br /> readonly屬性DomString licenseId;<br /> readonly屬性DRMPolicyArray策略； <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> readonly attribute int playbackPeriodInSeconds;<br /> readonly屬性long playbackStartDate;<br /> readonly屬性long playbackEndDate;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> readonly attribute int periodInSeconds;<br /> readonly attribute int startDate;<br /> readonly attribute int endDate;<br /> };</p> </td> 
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
   <td><p>interface DRMLicense {<br /> readonly attribute Uint8Array位元組；<br /> readonly屬性Date licenseStartDate;<br /> readonly屬性Date licenseEndDate;<br /> readonly屬性Date offlineStorageStartDate;<br /> readonly屬性Date offlineStorageEndDate; <br /> readonly屬性DomString serverUrl;<br /> readonly屬性DomString licenseID;<br /> readonly屬性DomString policyID;<br /> readonly屬性DRMPlaybackTimeWindow playbackTimeWindow;<br /> readonly屬性對象customProperties;<br /> }; </p> </td> 
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
   <td><p>interface DRMLicenseDomain {<br /> readonly屬性DomString authenticationDomain;<br /> readonly屬性DRMAuthenticationMethod authenticationMethod; <br /> readonly屬性DomString serverUrl;<br /> };</p> </td> 
   <td><p>interface DRMLicenseDomain {<br /> readonly屬性DomString authDomain;<br /> readonly屬性DRMAuthenticationMethod authMethod; <br /> readonly屬性DomString serverURL;<br /> };</p> </td> 
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
   <td><p>interface DRMPolicy<br /><br /> {readonly attribute DomString authenticationDomain;<br /> readonly屬性DRMAuthenticationMethod authenticationMethod;<br /><br /> readonly屬性DomString displayName;<br /> readonly屬性DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interface DRMPolicy<br /> {readonly<br /> attribute DomString authDomain;<br /> readonly屬性DRMAuthenticationMethod authMethod;<br /> readonly屬性DomString dispName;<br /> readonly屬性DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>介面DRMManager :EventTarget {<br /> void acquireLicense(DRMMetadata中繼資料， <br /> DRMAcquireLicenseSettings設定， <br /> DRMAquireLicenseListener);<br /> void acquirePreviewLicense(DRMMetadata中繼資料， <br /> DRMAquireLicenseListener);<br /> void authenticate(DRMMetadata中繼資料， <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString使用者， <br /> DomString密碼， <br /> DRMAuthenticateListener);<br /><br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array陣列， DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener);<br /> 屬性long maxOperationTime;<br /><br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain，布林值 <br /> forceRefresh, <br /> DRMOperationCompleteListener);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener);<br /><br /> void resetDRM(DRMOperationCompleteListener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID，布林 <br /> commitImmediated,<br /> DRMReturnLicenseListener);<br /> void setAuthenticationToken(<br /> DRMMetadata中繼資料， <br /> DomString authenticationDomain, <br /> Uint8Array token, <br /> DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener);<br /> };</p> </td> 
   <td><p>介面DRMManager :EventTarget {<br /> void acquireLicense(DRMMetadata中繼資料， <br /> DRMAcquireLicenseSettings設定， <br /> EventContext eventContext);<br /> void acquirePreviewLicense(DRMMetadata中繼資料， <br /> EventContext eventContext);<br /> void authenticate(DRMMetadata中繼資料， <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString使用者， <br /> DomString密碼， <br /> EventContext eventContext);<br /><br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array陣列， EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> 屬性long maxOperationTime;<br /><br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain，布林值 <br /> forceRefresh, <br /> EventContext eventContext);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /><br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID，布林commitImmediated, <br /><br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> DRMMetadata中繼資料， <br /> DomString authenticationDomain, <br /> Uint8Array token, <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>類DRMErrorListener : <br /> public psdkutils::PSDKIinterfaceWithUserData {public<br /> :<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils:PSDKString&amp;errorString, <br /> const psdkutils::PSDKString&amp;errorServerUrl)= 0;<br /><br /> 受保護：<br /> virtual ~DRMErrorListener(){}<br /> }</p> </td> 
   <td>事件／介面／說明 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>當DRMManger的其中一個非同步方法發生錯誤時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類DRMOperationCompleteListener : <br /> public DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete()= 0;<br /><br /> 受保護：<br /> virtual ~DRMOperationCompleteListener(){}<br /> };</p> </td> 
   <td>事件／介面／說明 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>完成DRM初始化時。</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>joinLicenseDomain()動作成功完成時。</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>leaveLicenseDomain()動作成功完成。</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>resetDRM()動作成功完成時。</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>setAuthenticationTokenSet()動作成功完成時。</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>storeLicenseBytes()動作成功完成時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類DRMAuthenticateListener : <br /> public DRMErrorListener {<br /> public:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken)= 0;<br /><br /> 受保護：<br /> virtual ~DRMAuthenticateListener(){}<br /> }</p> </td> 
   <td>事件／介面／說明 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>當DRMManager::authenticate方法調用成功時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類DRMAquireLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseAppired(const DRMLicense*)= 0;<br /><br /> 受保護：<br /> virtual ~DRMAquireLicenseListener(){}<br /> };</p> </td> 
   <td>事件／介面／說明 
    <ul> 
     <li>kEventDRMPreviewLicenseAppored<p>/ DRMLicenseAppiredEvent</p> <p>當DRMManager::acquirePreviewLicense方法調用成功時。</p> </li> 
     <li>kEventDRMLicenseApporied<p>/ DRMLicenseAppiredEvent</p> <p>當DRMManager::acquireLicense方法調用成功時。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>類DRMReturnLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturned)= 0;<br /><br /> 受保護：<br /> virtual ~DRMReturnLicenseListener(){}<br /> };</p> </td> 
   <td>事件／介面／說明 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>當DRMManager::returnLicense方法調用成功時。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0的一般播放API元素變更 {#generic-playback-api-element-changes-for}

這些表格會比較JavaScript TVSDK 1.3和2.0之間的一般播放API元素。

本主題中的表：

* MediaResource
* MediaPlayer
* ABRControlParameters
* BufferControlParameters
* TextFormat
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br /> attribute DomString url; <br /> 屬性無符號短類型；<br /> 屬性對象元資料；<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br /> attribute DomString url;<br /> 屬性DomString類型；<br /> 屬性對象元資料；<br /><br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>介面MediaPlayer:EventTarget<br /><br /> {void prepareToPlay(double position);<br /> void play();<br /> void pause();<br /> void seek(double position);<br /> void seekToLocal(double position);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem（MediaPlayerItem項目）;<br /> void replaceCurrentResource(MediaResource rsource、 <br /> MediaPlayerItemConfig); <br /> void suspend();<br /> void restore();<br /> void notifyClick();<br /><br /> readonly屬性TimeRange playbackRange;<br /> readonly屬性TimeRange seekableRange;<br /> readonly屬性double currentTime;<br /> readonly屬性double localTime;<br /> readonly屬性TimeRange bufferedRange;<br /> 只讀屬性DRMManager drmManager;<br /> readonly屬性MediaPlayerItem currentItem;<br /><br /> // PlayerStatus<br /> const unsigned <br /><br /> short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /><br /> 只讀屬性未簽名短狀態；<br /><br /> 屬性無符號短卷；<br /> attribute ABRControlParametersabrControlParameters;<br /> attribute BufferControlParameters bufferControlParameters;<br /><br /> const unsigned short VISIBLE;//For CC visibility<br /> const unsigned short INVISIBLE;//For CC visibility<br /> attribute unsigned short ccVisibility;<br /> 屬性TextFormat ccStyle;<br /> readonly屬性PlaybackMetrics playbackMetrics;<br /><br /> 屬性雙倍率；<br /> 屬性MediaPlayerView檢視；<br /> 只讀屬性時間軸；<br /> 屬性double currentTimeUpdateInterval; <br /> // setting this not be supported for 2.0<br /> };</p> </td> 
   <td><p>介面MediaPlayer:EventTarget<br /><br /> {void prepareToPlay(int position);<br /> void play();<br /> void pause();<br /> void seek(int position);<br /> void seekToLocalTime（int位置）;<br /> void reset();<br /> void release();<br /> void replaceCurrentItem（MediaResource來源）;<br /><br /> <br /> <br /> <br /> <br /> <br /> readonly屬性TimeRange playbackRange;<br /> readonly屬性TimeRange seekableRange;<br /> readonly屬性double currentTime;<br /> readonly屬性double localTime;<br /> readonly屬性TimeRange bufferedRange;<br /> 只讀屬性DRMManager drmManager;<br /> readonly屬性MediaPlayerItem currentItem;<br /><br /> // PlayerState<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> 只讀屬性無符號短狀態；<br /><br /> 屬性無符號短卷；<br /> attribute ABRControlParametersabrControlParameters;<br /> attribute BufferControlParameters bufferControlParameters;<br /><br /> 只讀未簽名的短VISIBLE;//For CC visibility<br /> readonly unsigned short INVISIBLE;//For CC visibility<br /> attribute unsigned short ccVisibility;<br /> 屬性TextFormat ccStyle;<br /> readonly屬性PlaybackMetrics playbackMetrics;<br /> 屬性MediaPlayerConfig mediaPlayerConfig;<br /> 屬性雙倍率；<br /> 屬性MediaPlayerView檢視；<br /> 只讀屬性時間軸；<br /><br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const unsigned short PLAYER_STATUS_IDLE;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>（2.0的新增功能）</td> 
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
   <td><p>（已針對2.0刪除）</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>準備</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>更新媒體播放器項目時。</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>更新</p> <p>當媒體播放器成功更新媒體時。</p> </td> 
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
   <td>timelineUpdated</td> 
   <td>事件</td> 
   <td> </td> 
   <td>TtmelineUpdated</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>在2.0中刪除</td> 
   <td> </td> 
   <td> </td> 
   <td>playStart</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>已刪除2.0版</td> 
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
   <td>SizeEvent</td> 
   <td> </td> 
   <td>大小</td> 
   <td>SizeEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakStarted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakStart</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adStarted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adStart</td> 
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
   <td>TimeEvent</td> 
   <td> </td> 
   <td>進度</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>bufferingBegin</td> 
   <td>事件</td> 
   <td> </td> 
   <td>緩衝</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>bufferingEnd</td> 
   <td>事件</td> 
   <td> </td> 
   <td>bufferComplete</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>seekBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekStart</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>seekEnd</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekComplete</td> 
   <td>TimeEvent</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>LoadInformationEvent</td> 
   <td> </td> 
   <td>loadInfo</td> 
   <td>LoadInfoEvent</td> 
  </tr> 
  <tr> 
   <td>operationFailed</td> 
   <td>NotificationEvent</td> 
   <td> </td> 
   <td>operationFailed</td> 
   <td>ErrorEvent</td> 
  </tr> 
  <tr> 
   <td>drmMetadataInfoAvailable</td> 
   <td>DRMMetadataEvent</td> 
   <td> </td> 
   <td>drmMetadata</td> 
   <td>DRMMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>reservationReached</td> 
   <td>ReservationEvent</td> 
   <td> </td> 
   <td>timelineHolderReached</td> 
   <td>TimelineHolderEvent</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>位元速率已變更</td> 
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
   <td>adBreakKlipted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakKlipted</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adClicked<br /> 當使用者點按廣告時。</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>2.0的新功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> When the playback profile changed.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>2.0的新功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdjusted<br /> 當搜尋位置因內部或外部規則而調整時。</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>2.0的新功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> 當媒體播放器項目更新時。 對於某些包含僅在播放時可偵測的音軌的串流，當有新的音軌時，就會引發此事件。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0的新功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>標題更 <br /> 新當媒體播放器項目更新時。 對於即時／線性串流，用戶端必須定期重新整理媒體資源，以偵測新的可用內容。 發生此情況時，某些媒體特性可能會改變。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0的新功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br /> 當媒體播放器項目更新時。 對於即時／線性串流，用戶端必須定期重新整理媒體資源，以偵測新的可用內容。 發生此情況時，某些媒體特性可能會改變。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0的新功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> 當媒體播放器項目更新時。 對於即時／線性串流，用戶端必須定期重新整理媒體資源，以偵測新的可用內容。 發生此情況時，某些媒體特性可能會改變。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0的新功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> Sent when timed events are generated.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>2.0的新功能</p> </td> 
  </tr> 
 </tbody> 
</table>

### ABRControlParameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface ABRControlParameters<br /><br /> {const unsigned short ABR_POLICY_CONSERVACY = 0;<br /> const unsigned short ABR_POLICY_MODERATE = 1;<br /> const unsigned short ABR_POLICY_AGGRESSIVE = 2;<br /><br /> attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interface ABRControlParameters<br /><br /> {const unsigned short ABR_POLICY_CONSERVACY = 0;<br /> const unsigned short ABR_POLICY_MODERATE = 1;<br /> const unsigned short ABR_POLICY_AGGRESSIVE = 2;<br /><br /> attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /><br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /><br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TextFormat {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0版無變更</td> 
   <td><p>interfaceTextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0;<br /> const unsigned short COLOR_BLACK = 1;<br /> const unsigned short COLOR_GRAY = 2;<br /> const unsigned short COLOR_WHITE = 3;<br /> const unsigned short COLOR_BRIGHT_WHITE = 4;<br /> const unsigned short COLOR_DARK_RED = 5;<br /> const unsigned short COLOR_RED = 6;<br /> const unsigned short COLOR_BRIGHT_RED = 7;<br /> const unsigned short COLOR_DARK_GREEN = 8;<br /> const unsigned short COLOR_GREEN = 9;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10;<br /> const unsigned short COLOR_DARK_BLUE = 11;<br /> const unsigned short COLOR_BLUE = 12;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13;<br /> const unsigned short COLOR_DARK_YELLOW = 14;<br /> const unsigned short COLOR_YELLOW = 15;<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16;<br /> const unsigned short COLOR_DARK_MAGENTA = 17;<br /> const unsigned short COLOR_MAGENTA = 18;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19;<br /> 不帶正負號的短色COLOR_DARK_CYAN = 20;<br /> const unsigned short COLOR_CYAN = 21;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22;<br /><br /> readonly屬性unsigned short fontColor;<br /> readonly屬性unsigned short backgroundColor;<br /> readonly屬性unsigned short fillColor;<br /> readonly屬性unsigned short edgeColor;<br /><br /> // Size<br /> const unsigned short SIZE_DEFAULT = 0;<br /> const unsigned short SIZE_SMALL = 1;<br /> const unsigned short SIZE_MEDIUM = 2;<br /> const unsigned short SIZE_LARGE = 3;<br /><br /> 只讀屬性無符號短大小；<br /><br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0;<br /> const unsigned short FONT_EDGE_NONE = 1;<br /> 不帶正負號的短字FONT_EDGE_ROUSED = 2;<br /> const unsigned short FONT_EDGE_DOSCREPT = 3;<br /> const unsigned short FONT_EDGE_UNIFORM = 4;<br /> 不帶正負號的短字型FONT_EDGE_DROP_SHADOW_LEFT = 5;<br /> 不帶正負號的短字型FONT_EDGE_DROP_SHADOW_RIGHT = 6;<br /> readonly屬性unsigned short fontEdge;<br /><br /> // Font<br /> const unsigned short FONT_DEFAULT = 0;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1;<br /> const unsigned short FONT_PORTIONAL_WITH_SERIFS = 2;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3;<br /> const unsigned short FONT_CASUAL = 4;<br /> 不帶正負號的短字型_草書= 5;<br /> 不帶正負號的短字型SMALL_CAPPALITES = 6;<br /> 只讀屬性無符號短字型；<br /> readonly屬性unsigned short fontOpacity;<br /> readonly屬性unsigned short backgroundOpacity;<br /> readonly屬性unsigned short fillOpacity;<br /> readonly屬性unsigned short DEFAULT_OPACITY;<br /> };</p> </td> 
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
   <td><p>介面MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource資源， long resourceId,<br /> ItemLoaderListener, <br /> MediaPlayerItemConfig組態);<br /> void cancel();<br /> readonly屬性MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>2.0的新功能</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>2.0的新功能</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的媒體特性API元素變更 {#media-characteristics-api-element-changes-for}

這些表格比較C++ TVSDK 1.3版和2.0版的媒體特性API元素。

本主題中的表：

* MediaPlayerItem
* Track、AudioTrack、ClosedCaptionsTrack
* 描述檔
* DRMMetadataInfo

### MediaPlayerItem {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItem {readonly<br /> attribute MediaResource資源；<br /> readonly屬性long resourceId;<br /> 只讀屬性布爾live;<br /><br /> readonly屬性boolean hasAlternateAudio;<br /> readonly屬性AudioTrackList audioTracks;<br /> readonly屬性AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack); <br /> <br /> readonly屬性boolean hasClosedCaptions;<br /> readonly屬性ClosedCaptionsTrackList closedCaptionsTracks;<br /> readonly屬性ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTracktrack); <br /> <br /> readonly屬性布林值hasTimedMetadata;<br /> readonly屬性TimedMetadataList timedMetadata;<br /> 只讀屬性布爾動態；<br /><br /> readonly屬性boolean isProtected;<br /> readonly屬性DRMMetadataInfoList drmMetadataInfos;<br /> readonly attribute ProfileList描述檔；<br /> readonly attribute profile selectedProfile;<br /><br /> readonly屬性boolean trickPlaySupported;<br /> readonly屬性floatArray availablePlaybackRates;<br /> readonly屬性float selectedPlaybackRate;<br /><br /> <br /> readonly屬性MediaPlayer mediaPlayer;<br /> readonly屬性MediaPlayerItemConfig;<br /> };</p> </td> 
   <td><p>interface MediaPlayerItem {readonly<br /> attribute MediaResource資源；<br /> readonly屬性long resourceId;<br /> 只讀屬性布爾live;<br /><br /> readonly屬性boolean hasAlternateAudio;<br /> readonly屬性AudioTrackList audioTracks;<br /> attribute AudioTrack selectedAudioTrack;<br /><br /> <br /> readonly屬性boolean hasClosedCaptions;<br /> readonly屬性ClosedCaptionsTrackList ccTracks;<br /> 屬性ClosedCaptionsTrack selectedCCTrack;<br /><br /> <br /> <br /> readonly屬性布林值hasTimedMetadata;<br /> readonly屬性TimedMetadataList timedMetadata;<br /> 只讀屬性布爾動態；<br /><br /> readonly屬性boolean isProtected;<br /> readonly屬性DRMMetadataInfoList drmMetadataInfos;<br /> readonly attribute ProfileList描述檔；<br /><br /> <br /> readonly屬性boolean trickPlaySupported;<br /> readonly屬性Int32Array availablePlaybackRates;<br /><br /> readonly屬性StringList adTags;<br /><br /> readonly屬性MediaPlayer mediaPlayer;<br /><br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 音軌／音軌/ ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {readonly<br /> attribute DomString name;<br /> readonly屬性DomString語言；<br /> 只讀屬性布爾型預設值；<br /> readonly attribute boolean autoSelect;<br /> }; </p> </td> 
   <td>2.0的新功能</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack:Track<br /> {readonly<br /> attribute DomString name;//FromTrack<br /> readonly屬性DomString語言；//FromTrack<br /> readonly屬性布林值預設值；// From Track<br /> readonly attribute boolean autoSelect;//FromTrack<br /><br /> readonly attribute unsigned int pid;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {readonly<br /> attribute DomString name;<br /> readonly屬性DomString語言； <br /> 只讀屬性布爾型預設值；<br /> readonly attribute boolean autoSelect;<br /> 只讀屬性布爾強制；<br /><br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0版無變更</td> 
   <td><p>interface AudioTrackList<br /> {<br /> readonly attribute unsigned long length;<br /> getterAudioTrack（未簽署的長索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack:Track<br /> {readonly<br /> attribute DomString name;//FromTrack<br /> readonly屬性DomString語言；//FromTrack<br /> readonly屬性布林值預設值；// FromTrack<br /> readonly屬性boolean autoSelect;//FromTrack<br /> <br /><br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> readonly attribute unsigned short serviceType;<br /> 只讀屬性布爾強制；<br /> };</p> </td> 
   <td><p>interfaceClosedCaptionsTrack<br /> {<br /> readonly屬性DomString名稱；<br /> readonly屬性DomString語言；<br /> 只讀屬性布爾型預設值；<br /><br /> <br /> 只讀屬性布爾活動；<br /><br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0版無變更</td> 
   <td><p>interfaceClosedCaptionsTrackList<br /> {<br /> readonly attribute unsigned longlength;<br /> getterClosedCaptionsTrack(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 描述檔 {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>設定檔：2.0版無變更</td> 
   <td><p>interface Profile<br /> {<br /> readonly attribute unsigned int width;<br /> int height的只讀屬性；<br /> readonly attribute unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList:2.0版無變更</td> 
   <td><p>interface ProfileList<br /> {<br /> readonly attribute unsigned long length;<br /> getter描述檔（無符號長索引）;<br /> };</p> </td> 
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
   <td><strong>DRMMetadataInfo</strong>:2.0版無變更</td> 
   <td><p>interface DRMMetadataInfo<br /> { <br /> readonly屬性DRMMetadata中繼資料；<br /> readonly屬性long prefetchTimestamp;<br /> 只讀屬性TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>:2.0版無變更</td> 
   <td><p>interface DRMMetadataInfoList<br /> {<br /> readonly attribute unsigned long length;<br /> getter DRMMetadataInfo(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 將C++錯誤映射到不同語言的異常 {#mapping-c-errors-to-exceptions-in-different-languages}

您可以將C++錯誤代碼映射到不同語言的異常。

C++ PSDK的API有「不扔」原則。 大部分的API方法會傳回PSDKErrorCode值，以指出方法是否成功執行。 非同步錯誤會透過錯誤事件通知。

ActionScript和JAVA PSDK有不同的原則。 大部分錯誤都會擲出ArgumentError或IllegalStateException，以指出無法執行方法的同步部分。 這些例外不會被捕獲，應用程式碼負責處理例外。 它們通常會提供方法呼叫失敗的有用資訊。 例如，如果prepareToPlay命令被調用為無效狀態，則會拋出以下異常：

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

ActionScript/JAVA也會從建構函式中拋出例外，以指出某些內部物件建立錯誤。 這些例外是內部處理的，不會傳播到應用程式。 例外情況將包含在發送給應用程式的警告通知中

例如，如果未找到收到的廣告回應的有效媒體檔案，則無法建立有效的廣告資產物件或廣告。 因此，時間軸上不會放置任何廣告，並會傳送NotificationEvent.OperationFailed通知。

從Adobe視訊引擎(AVE)非同步收到的錯誤或警告代碼會以一般事件傳送至應用程式。 通知事件包含所有收到的錯誤碼和任何其他中繼資料，例如URL、資源識別碼、控制代碼等。 如果錯誤嚴重且無法繼續播放目前的媒體，MediaPlayer會轉換為ERROR狀態，並傳送onStatusChanged回呼或MediaPlayerStatusChanged.STATUS_CHANGED事件。 如果播放可繼續，則會傳送一般通知事件。

<table> 
 <tbody> 
  <tr> 
   <th>C++錯誤（PSDKError代碼）</th> 
   <th> </th> 
   <th>Java</th> 
   <th>ActionScript</th> 
   <th>JavaScript</th> 
  </tr> 
  <tr> 
   <td>kECInvalidArgument</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>參數錯誤</td> 
   <td>代碼= 1的異常，說明= "INVALID_ARGUMENT"和additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>參數錯誤</td> 
   <td>代碼= 2的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>代碼為3的異常，說明= "ILLEGAL_STATE"和additionalInfo= &lt;拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>KECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼= 4的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為5的異常，說明= "CREATION_FAILED"和additionalInfo= &lt;按拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>kECUnsupported運行</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為5的異常，說明= "CREATION_FAILED"和additionalInfo= &lt;按拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼= 7的例外，說明= "DATA_NOT_AVAILABLE"和additionalInfo= &lt;拋出此例外的方法傳遞的方式&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為8的異常，說明= "SEEK_ERROR"和additionalInfo= &lt;拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>kECUnsupported功能</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為9的異常，說明= "UNSUPPORTED_FEATURE"和additionalInfo= &lt;拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼= 10的例外，說明= "RANGE_ERROR"和附加Info= &lt;拋出此例外的方法傳遞的例外</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼= 11的例外情況，說明= "CODEC_NOT_SUPPORTED"和additionalInfo= &lt;拋出此例外的方法傳遞的方式&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為12的例外，說明= "MEDIA_ERROR"和additionalInfo= &lt;拋出此例外的方法傳遞的方式&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為13的異常，說明= "NETWORK_ERROR"和additionalInfo= &lt;拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error或MediaPlayerNotification.Warning</td> 
   <td>MediaError或NotificationEvent</td> 
   <td>代碼為14的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼= 15的例外，說明= "INVALID_SEEK_TIME"和additionalInfo= &lt;拋出此例外的方法傳遞的方式&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼= 16的例外，說明= "AUDIO_TRACK_ERROR"和additionalInfo= &lt;拋出此例外的方法傳遞的方式&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>線程錯誤</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為17的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼= 18的例外，說明= "GENERIC_ERROR"和附加Info= &lt;，由拋出此例外的方法傳遞</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼為19的異常，說明= "GENERIC_ERROR"和additionalInfo= &lt;拋出此異常的方法傳遞的'</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代碼= 200的例外，說明= "PLAYBACK_OPERATION_FAILED"和additionalInfo= &lt;通過拋出此例外的方法傳遞的方式&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>代碼為201的例外，說明= "NATIVE_WARNING"和附加Info= &lt;拋出此例外的方法傳遞的例外</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>代碼= 202的例外，說明= "AD_RESOLVER_FAILED"和additionalInfo= &lt;拋出此例外的方法傳遞的方式&gt;</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的公用程式和Helper API元素變更 {#utility-and-helper-api-element-changes-for}

這些表格會比較1.3版和2.0版之間JavaScript TVSDK的公用程式和Helper API元素。

本主題中的表：

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
   <td><p>interface version<br /> {readonly<br /> attribute DomString version;<br /> readonly屬性DomString說明；<br /> 只讀屬性長主題；<br /> 只讀屬性長副詞；<br /> 只讀屬性長修訂；<br /> readonly屬性long apiVersion;<br /> };</p> </td> 
   <td><p>interface version<br /> {readonly<br /> attribute DomString version;<br /> readonly屬性DomString說明；<br /> readonly屬性DomString主要；<br /> readonly屬性DomString次要；<br /> readonly屬性DomString修訂；<br /> readonly屬性DomString apiVersion;<br /> };</p> </td> 
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
   <td>2.0版無變更</td> 
   <td><p>interface TimeRange<br /> {<br /> readonly attribute unsigned long begin;<br /> 只讀屬性無符號長端；<br /> 只讀屬性未簽名的長持續時間；<br /> };</p> </td> 
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
   <td>2.0版無變更</td> 
   <td><p>介面QOSProvider<br /><br /> {void attachMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /><br /> readonly屬性DeviceInformation deviceInformation;<br /> readonly屬性PlaybackInformation playbackInformation;<br /> };</p> </td> 
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
   <td><p>interfaceDeviceInformation<br /> {readonly<br /> attribute DomString os;<br /><br /> <br /> <br /> readonly屬性DomString id;<br /> 只讀屬性int densityDPI;<br /> readonly attribute int heightPixels;<br /> readonly屬性int widthPixels;<br /> readonly屬性boolean seekToKeyFrame;<br /> };</p> </td> 
   <td><p>interfaceDeviceInformation<br /> {readonly<br /> attribute DomString os;<br /> 唯讀屬性int sdk;<br /> readonly屬性DomString模型；<br /> readonly屬性DomString製造商；<br /> readonly屬性DomString id;<br /> 只讀屬性int densityDPI;<br /> readonly attribute int heightPixels;<br /> readonly屬性int widthPixels;<br /><br /> };</p> </td> 
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
   <td>2.0版無變更</td> 
   <td><p>interface LoadInfo<br /> {<br /> readonly屬性DomString url;<br /> 只讀屬性int大小；<br /> readonly屬性double downloadDuration;<br /> readonly attribute int periodIndex;<br /> readonly屬性double mediaDuration;<br /> readonly屬性short TRACK_TYPE_FRAGMENT;<br /> readonly屬性short TRACK_TYPE_TRACK;<br /> readonly屬性short TRACK_TYPE_MANIFEST;<br /> 只讀屬性短類型；<br /> readonly屬性DomString trackName;<br /> readonly屬性DomString trackType;<br /> readonly attribute int trackIndex;<br /> };</p> </td> 
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
   <td>2.0版無變更</td> 
   <td><p>interface View<br /> {<br /> readonly attribute unsigned short x;<br /> 無符號短y的只讀屬性；<br /> 只讀屬性無符號短寬；<br /> 只讀屬性無符號短高；<br /><br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
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
   <td><p>interface PlaybackInformation<br /> {<br /> readonly attribute double timeToFirstByte;<br /> readonly屬性double timeToLoad;<br /> readonly屬性double timeToStart;<br /> readonly屬性double timeToFail;<br /> readonly attribute int totalSecondsPlayed;<br /> readonly attribute int totalSecondsSpent;<br /> readonly屬性double frameRate;<br /> readonly attribute int droppedFrameCount;<br /> readonly attribute int envericedBandwidth;<br /> 位速率的只讀屬性；<br /> readonly屬性double bufferTime;<br /> readonly attribute int bufferLength;<br /> readonly屬性int emptyBufferCount;<br /> readonly屬性double bufferingTime;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly attribute double timeToFirstByte;<br /> readonly屬性double timeToLoad;<br /> readonly屬性double timeToStart;<br /> readonly屬性double timeToFail;<br /> readonly attribute int totalSecondsPlayed;<br /> readonly attribute int totalSecondsSpent;<br /> readonly屬性double frameRate;<br /> readonly attribute int droppedFrameCount;<br /><br /> 位速率的只讀屬性；<br /> readonly屬性double bufferTime;<br /> readonly attribute int bufferLength;<br /> readonly屬性int emptyBufferCount;<br /> readonly屬性double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 有用的資源 {#helpful-resources}

* 請參閱 [Adobe Primetime學習與支援頁面的完整說明檔案](https://helpx.adobe.com/support/primetime.html) 。
