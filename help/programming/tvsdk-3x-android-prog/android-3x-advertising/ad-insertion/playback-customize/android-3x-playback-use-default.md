---
description: 您可以選擇使用預設廣告行為。
seo-description: 您可以選擇使用預設廣告行為。
seo-title: 使用預設播放行為
title: 使用預設播放行為
uuid: 36f76c42-4c6c-4620-9b47-ec97519a642a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 使用預設播放行為 {#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

1. 若要使用預設行為，請完成下列任一項工作：

   * 如果您實作自己的 `AdvertisingFactory` 類，請傳回null `createAdPolicySelector`。

   * 如果您沒有類別的自訂實作，TVSDK `AdvertisingFactory` 會使用預設廣告原則選擇器。

## 設定自訂播放 {#set-up-customized-playback}

您可以自訂或覆寫廣告行為。

在自訂或覆寫廣告行為之前，請先註冊廣告原則例項。
若要自訂廣告行為，請執行下列其中一項作業：

* 實作介 `AdPolicySelector` 面及其所有方法。

   如果您需要覆寫所有預設廣告 **行為** ，建議使用此選項。

* 擴充類 `DefaultAdPolicySelector` 別，並僅針對需要自訂的行為提供實作。

   如果您只需要覆寫部分預設行 **為** ，建議使用此選項。

若要自訂廣告行為：

1. 實作介 `AdPolicySelector` 面及其所有方法。
1. 指派TVSDK透過廣告廠使用的原則例項。

>[!NOTE]
>classCustomContentFactory擴充ContentFactory {
>...
>@Override
>publicAdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem){
>傳回新的CustomAdPolicySelector(mediaPlayerItem);
>}
>...
>}
>//向媒體播放器註冊自訂內容工廠
>MediaPlayerItemConfig = new MediaPlayerItemConfig();
>config.setAdvertisingFactory(new CustomContentFactory());
>// this config will belled passed while loading >resource
>mediaPlayer.replaceCurrentResource(resource, config);

1. 實作您的自訂。