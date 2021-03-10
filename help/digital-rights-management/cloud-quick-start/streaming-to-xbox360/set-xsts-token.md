---
title: 在您的播放器中設定XSTS Token
description: 在您的播放器中設定XSTS Token
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# 在您的播放器中設定XSTS Token{#set-the-xsts-token-in-your-player}

在Xbox360中，您會以非同步方式設定Token，以回應`MediaPlayer.RequestKeyAttribute`事件。

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

