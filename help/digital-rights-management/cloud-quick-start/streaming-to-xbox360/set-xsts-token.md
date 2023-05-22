---
title: 在播放器中設定XSTS令牌
description: 在播放器中設定XSTS令牌
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# 在播放器中設定XSTS令牌{#set-the-xsts-token-in-your-player}

在Xbox360中，您非同步設定令牌以響應 `MediaPlayer.RequestKeyAttribute` 的子菜單。

設定XSTS令牌。

與軟體捆綁的示例應用說明如何在播放器中設定XSTS令牌。 下面是示例播放器中的相關代碼段：

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

