---
description: Adobe為不希望開發和維護自己的Mignishe DRM許可證伺服器的Adobe PrimetimeDRM客戶提供雲DRM服務。 通過利用此服務，客戶可以降低DRM許可證頒發的操作和開發複雜性。 黃金時段雲DRM可向所有能夠運行支援黃金時段瀏覽器TVSDK的視頻應用程式的設備(如iOS、Android、台式機和Xbox360)發放DRM許可。 此DRM服務由Adobe托管和維護，全天候運行。
title: 背景
exl-id: bb5ad080-5b1d-43a6-8d0e-9b5735c82d96
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# 背景 {#background}

Adobe為不希望開發和維護自己的Mignishe DRM許可證伺服器的Adobe PrimetimeDRM客戶提供雲DRM服務。 通過利用此服務，客戶可以降低DRM許可證頒發的操作和開發複雜性。 黃金時段雲DRM可向所有能夠運行支援黃金時段瀏覽器TVSDK的視頻應用程式的設備(如iOS、Android、台式機和Xbox360)發放DRM許可。 此DRM服務由Adobe托管和維護，全天候運行。

>[!NOTE]
>
>Adobe PrimetimeDRM以前叫做Adobe訪問，在之前叫Flash Access。

## 黃金時段雲DRM包括什麼 {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* 自定義身份驗證/權利模組以及有關如何針對您的內容進行自定義身份驗證的說明。 有關詳細文檔，請參閱 [!DNL Custom Authentication Entitlement] 的子菜單。
* 雲DRM特定的許可證伺服器證書( [!DNL .pem/.cer/.der])

* 特定於雲DRM的許可證伺服器傳輸證書( [!DNL .pem/.cer/.der])

* 黃金時段Java離線打包器
* 打包的DRM策略示例

   * **policy_24hr**  — 磁碟上的許可證快取24小時。 24小時後，必須獲得新許可證才能查看內容。 此工具包中的所有其他策略也具有24小時許可證快取。
   * **策略_ios_remotekeyserver**  — 在iOS設備上，將從雲DRM獲得DRM許可。 此外，客戶端將從雲DRM獲取所有AES解密密鑰。 在越獄的iOS設備上不允許播放。

   * **策略_ios_localkeyserver**  — 在iOS設備上，將從雲DRM獲得DRM許可。 此外，客戶端將從本地HTTP伺服器而不是雲DRM獲取所有HLS AES解密密鑰。 在越獄的iOS設備上不允許播放。

   * **policy_adobePass**  — 客戶端必須首先使用(以前稱為Adobe Pass)進行身份驗證，否則許可證將被拒絕。

* Adobe策略管理器工具以建立其他DRM策略
* 用於打包的視頻內容示例
