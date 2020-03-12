---
description: 'null'
seo-description: 'null'
seo-title: 在您的播放器中設定XSTS Token
title: 在您的播放器中設定XSTS Token
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b

---


# 在您的播放器中設定XSTS Token{#set-the-xsts-token-in-your-player}

在Xbox360中，您會以非同步方式設定代號，以回應 `MediaPlayer.RequestKeyAttribute` 事件。

設定XSTS Token。

軟體隨附的範例應用程式說明如何在您的播放器中設定XSTS Token。 以下是範例播放器中的相關程式碼片段：

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

