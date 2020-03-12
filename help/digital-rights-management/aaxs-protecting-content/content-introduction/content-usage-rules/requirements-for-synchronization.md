---
seo-title: 同步要求
title: 同步要求
uuid: 976a0ae1-bece-437e-b95b-6cd222525d13
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 同步要求{#requirements-for-synchronization}

指定客戶端將與伺服器同步其狀態的頻率。 如果客戶端已獲得帶外許可證（未聯繫許可證伺服器），使用規則可能會指定客戶端必須向伺服器發送同步消息，以便同步客戶端的安全時間並向伺服器報告客戶端狀態。

同步行為使用以下參數定義：

* 開始間隔— 指定上次成功同步後等待多久的時間以啟動另一個同步請求。
* 硬停止間隔— （可選）。 如果未在指定的時間長度內成功同步，則不允許播放。
* 強制同步概率— （可選）。 客戶端在下一個啟動間隔之前發送同步消息的概率。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>此使用規則受Adobe Access用戶端3.0版及更新版本支援。 舊客戶端的行為取決於許可證伺服器支援的最低客戶端版本。 請參閱「 [最低客戶端版本](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md)」。

