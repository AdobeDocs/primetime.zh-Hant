---
title: Adobe PrimetimeAd Insertion公告
description: 關於Primetime最新功能發佈及其他相關新聞的公告Ad Insertion
translation-type: tm+mt
source-git-commit: d8fde0d03bea85b3fefcfa5dcbfddee76b17de03
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# PrimetimeAd Insertion公告

## 透過廣告解析逾時減少程式化廣告錯誤

發佈日期：2020年12月1日

Adobe的重點在於協助PrimetimeAd Insertion客戶將廣告庫存的獲利提升到最大。 我們特別注意降低滿足程式化需求的複雜性，根據eMarketer的資料，程式化需求佔美國數位視訊廣告支出的四分之三以上。 程式化銷售可讓出版業者將廣告庫存需求最大化，進而提高填滿率和收益。 但是，它也會增加廣告錯誤的曝光度，例如格式錯誤的VAST回應、HTTP錯誤，以及可能導致收入損失和／或檢視器體驗不佳的其他錯誤。

一個常見問題是程式化合作夥伴的反應緩慢。 程式化廣告交易通常以毫秒為單位進行。 然而，有時單一需求來源可能需要過長的時間才能回應。 來自單一提供者的延遲可能會影響整個廣告履約程式，造成檢視器暫時空白畫面、未填入廣告位置，或在極端情況下重新啟動視訊串流的需要。 不幸的是，識別和繞過緩慢的需求來源是一個重大挑戰。

為解決此問題，Adobe在PrimetimeAd Insertion中新增了新工具，讓客戶可以設定廣告解決時間限制。 設定這些規則會自動略過緩慢的需求來源，以確保視訊播放器及時收到廣告回應。 這可讓出版業者大幅限制需求來源不暢造成的中斷，協助他們將庫存填滿率提升到最大，並提供不間斷的電視品質觀賞體驗。

若要在PrimetimeAd Insertion中啟用廣告解析逾時，請修改您的引導API，以包含ptadtimeout參數（持續時間，以毫秒為單位）。  在逾時期間之前未完成的任何廣告請求將不會銜接（任何後援廣告都會處理）。