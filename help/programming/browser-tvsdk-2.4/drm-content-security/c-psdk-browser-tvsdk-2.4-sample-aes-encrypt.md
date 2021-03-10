---
description: AES-128加密方法對包括標頭的整個傳輸流(TS)容器進行加密，而SAMPLE-AES加密僅對音頻和部分視頻資料進行加密。
title: AES加密的HLS串流範例
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# 範例AES加密的HLS串流{#sample-aes-encrypted-hls-streams}

AES-128加密方法對包括標頭的整個傳輸流(TS)容器進行加密，而SAMPLE-AES加密僅對音頻和部分視頻資料進行加密。

在加密流中，標識保護塊，其上完成保護過程。 H.264視頻保護塊是網路適配層(NAL)單元的類型1和類型5的主體。 受保護的音訊區塊是音訊影格，音訊必須採用AAC格式。

>[!IMPORTANT]
>
>您必須有索引鍵和初始化向量(IV)。 瀏覽器TVSDK使用金鑰和IV來解密串流，再播放它。

每個受保護區塊包含16位元組區塊的整數，這些區塊使用AES-128密碼區塊鏈結(CBC)模式加密，而不需填補。 CBC發生在每個受保護的塊中，而在每個新保護塊的開頭，IV必須重置為其原始值。

支援下列轉碼器：

* 視訊支援H.264。
* 對於音訊，僅AAC支援sample-AES。

