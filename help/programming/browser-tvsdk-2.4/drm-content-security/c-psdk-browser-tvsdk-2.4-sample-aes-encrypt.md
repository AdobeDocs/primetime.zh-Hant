---
description: 雖然AES-128加密方法會加密整個傳輸資料流(TS)容器（包括標題），但SAMPLE-AES加密只會加密音訊和部分視訊資料。
title: AES加密的HLS資料流範例
exl-id: 04bda50f-5ca4-4a00-bb5a-97259a2cb005
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# AES加密的HLS資料流範例{#sample-aes-encrypted-hls-streams}

雖然AES-128加密方法會加密整個傳輸資料流(TS)容器（包括標題），但SAMPLE-AES加密只會加密音訊和部分視訊資料。

在加密的串流中，會識別完成保護程式的受保護區塊。 H.264視訊保護區塊是網路適用層(NAL)單位型別1和5的主體。 受保護的音訊區塊是音訊框架，音訊必須是AAC格式。

>[!IMPORTANT]
>
>您必須擁有金鑰和初始化向量(IV)。 瀏覽器TVSDK會使用金鑰和IV在播放資料流之前解密資料流。

每個受保護的區塊都包含一個16位元組區塊的整數，這些區塊會使用AES-128 cipher block-chaining (CBC)模式加密，且沒有內距。 CBC會發生在每個受保護的區塊中，並且在每個新的受保護區塊開始時，IV必須重設為原始值。

支援下列轉碼器：

* 視訊支援H.264。
* 若是音訊，僅支援AAC的sample-AES。
