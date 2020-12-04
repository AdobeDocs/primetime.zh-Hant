---
description: 以下加密選項是在封裝時選取的，在取得授權時無法修改。
seo-description: 以下加密選項是在封裝時選取的，在取得授權時無法修改。
seo-title: 鍵旋轉
title: 鍵旋轉
uuid: 6ee47c06-9981-4281-b10b-343f8b1e55b7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 鍵旋轉{#key-rotation}

以下加密選項是在封裝時選取的，在取得授權時無法修改。

在打包期間，通常使用內容加密密鑰(CEK)加密內容，並且客戶端獲得包含CEK的許可證以使用內容。 啟用密鑰旋轉時，旋轉密鑰用於加密內容，密鑰可以更改，因此每個旋轉密鑰僅用於加密內容的一部分。 旋轉金鑰使用內容加密金鑰加以保護，而用戶端仍取得包含CEK的單一授權，以使用內容。 封裝器實作可控制使用的內容加密金鑰和旋轉金鑰，以及旋轉金鑰變更的頻率。

使用索引鍵旋轉封裝的內容只能在Adobe Access 3.0版及更新版本的用戶端上播放。 較舊的客戶需要升級才能播放此內容。
