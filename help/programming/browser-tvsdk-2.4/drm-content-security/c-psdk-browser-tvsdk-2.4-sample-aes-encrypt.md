---
description: AES-128加密方法加密包括報頭的整個傳輸流(TS)容器，而SAMPLE-AES加密僅加密音頻和部分視頻資料。
title: 示例AES加密的HLS流
exl-id: 04bda50f-5ca4-4a00-bb5a-97259a2cb005
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# 示例AES加密的HLS流{#sample-aes-encrypted-hls-streams}

AES-128加密方法加密包括報頭的整個傳輸流(TS)容器，而SAMPLE-AES加密僅加密音頻和部分視頻資料。

在加密流中，標識保護塊，在該塊上完成保護過程。 H.264視頻保護塊是網路適配層(NAL)單元類型1和類型5的主體。 受保護的音頻塊是音頻幀，音頻必須為AAC格式。

>[!IMPORTANT]
>
>必須具有鍵和初始化向量(IV)。 瀏覽器TVSDK在播放流之前使用密鑰和IV解密流。

每個受保護塊包含16位元組的塊的整數，這些塊使用AES-128密碼塊連結(CBC)模式進行加密，而不用填充。 CBC發生在每個受保護塊中，並且在每個新受保護塊的開始時，必須將IV重置為其原始值。

支援以下編解碼器：

* 對於視頻，支援H.264。
* 對於音頻，僅AAC支援sample-AES。
