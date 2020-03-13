---
description: 'null'
seo-description: 'null'
seo-title: 使用DRMContentData預載許可證
title: 使用DRMContentData預載許可證
uuid: 5cedd077-0613-4677-8fb0-81237d7ac61a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用DRMContentData預載許可證{#using-drmcontentdata-to-pre-load-licenses}

下列步驟說明使用物件預先載入受保護媒體檔案授權的工作 `DRMContentData` 流程。

1. 取得封裝內容的二進位DRM中繼資料。

   如果使用Primetime DRM Java Reference Implementations Packager，則會自動產生副檔名的中繼資 [!DNL .metadata] 料檔案。 例如，您可以使用類別下載此中繼資 `URLLoader` 料。 如果使用HLS或HDS內容，則中繼資料會參照在內容資訊清單檔案( [!DNL .m3u8] 或 [!DNL .f4m]** )中，或以Base64編碼字串的形式包含在資訊清單檔案中（在使用前必須先Base64解碼）。
1. 建立物 `DRMContentData` 件，將中繼資料傳遞至建構函式函式：

   ```
   var drmData:DRMContentData = new DRMContentData( metadata );
   ```

1. 其餘步驟與「內容保護流程詳細資訊」中描述的 *工作流相同*。

<!--<a id="example_EBEDA8E10F6344CABA4DE31DC342B8F8"></a>-->

```
import flash.events.DRMAuthenticationCompleteEvent; 
import flash.events.DRMAuthenticationErrorEvent; 
import flash.events.DRMErrorEvent; 
import flash.events.DRMStatusEvent; 
import flash.events.NetStatusEvent; 
import flash.net.NetConnection; 
import flash.net.Primetime; 
import flash.net.PrimetimePlayOptions; 
import flash.net.drm.AuthenticationMethod; 
import flash.net.drm.DRMContentData; 
import flash.net.drm.DRMManager; 
import flash.net.drm.LoadVoucherSetting; 
  
public class DRMPreloader extends Sprite  { 
    private var videoURL:String = "app-storage:/video.flv"; 
    private var userName:String = "user"; 
    private var password:String = "password"; 
    private var preloadConnection:NetConnection; 
    private var preloadStream:Primetime; 
    private var drmManager:DRMManager = DRMManager.getDRMManager(); 
 
    private var drmContentData:DRMContentData; 
 
    public function DRMPreloader():void { 
        drmManager.addEventListener(  
          DRMAuthenticationCompleteEvent.AUTHENTICATION_COMPLETE,  
          onAuthenticationComplete 
        ); 
        drmManager.addEventListener( 
          DRMAuthenticationErrorEvent.AUTHENTICATION_ERROR,  
          onAuthenticationError 
        ); 
        drmManager.addEventListener( 
          DRMStatusEvent.DRM_STATUS, onDRMStatus); 
        drmManager.addEventListener( 
          DRMErrorEvent.DRM_ERROR, onDRMError); 
        preloadConnection = new NetConnection(); 
        preloadConnection.addEventListener( 
          NetStatusEvent.NET_STATUS, onConnect); 
        preloadConnection.connect(null);  
    } 
 
    private function onConnect( event:NetStatusEvent ):void {  
        preloadMetadata(); 
    } 
 
    private function preloadMetadata():void {  
        preloadStream = new Primetime( preloadConnection ); 
        preloadStream.client = this; 
        var options:PrimetimePlayOptions = new PrimetimePlayOptions(); 
        options.streamName = videoURL; 
        preloadStream.preloadEmbeddedData( options );  
    }  
 
    public function onDRMContentData( drmMetadata:DRMContentData ):void {  
        drmContentData = drmMetadata; 
        if ( drmMetadata.authenticationMethod ==  
               AuthenticationMethod.USERNAME_AND_PASSWORD ) {  
            authenticateUser(); 
        } 
        else {  
            getVoucher(); 
        } 
    } 
 
    private function getVoucher():void {  
        drmManager.loadVoucher(  
          drmContentData,  
          LoadVoucherSetting.ALLOW_SERVER  
        ); 
    } 
 
    private function authenticateUser():void {  
        drmManager.authenticate(  
          drmContentData.serverURL,  
          drmContentData.domain,  
          userName,  
          password  
        ); 
    } 
 
    private function onAuthenticationError(  
      event:DRMAuthenticationErrorEvent ):void {  
        trace( "Authentication error: " +  
               event.errorID + ", " +  
               event.subErrorID ); 
    } 
 
    private function onAuthenticationComplete(  
      event:DRMAuthenticationCompleteEvent ):void {  
        trace( "Authenticated to: " +  
               event.serverURL + ",  
               domain: " +  
               event.domain ); 
        getVoucher(); 
    } 
 
    private function onDRMStatus( event:DRMStatusEvent ):void { 
        trace( "DRM Status: " + event.detail); 
        trace("--License allows offline playback = " +  
              event.isAvailableOffline ); 
        trace("--License already cached = " +  
              event.isLocal ); 
        trace("--License required authentication = " +  
              !event.isAnonymous ); 
    } 
 
    private function onDRMError( event:DRMErrorEvent ):void { 
        trace( "DRM error event: " +  
               event.errorID + ", " +  
               event.subErrorID + ", " +  
               event.text ); 
    } 
 
    public function onPlayStatus( info:Object ):void { 
        preloadStream.close(); 
    }  
} 
```

